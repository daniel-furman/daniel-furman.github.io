---
title: "BirdCLEF21 Kaggle Competition Write Up."
date: 2021-06-19
katex: true
markup: "mmark"
---

## BirdCLEF21 Kaggle Competition Write Up.
---

The BirdCLEF21 Kaggle competition task was to classify bird calls by their species (397 target classes). These bird call recognition models were aimed at streamlining and semi-automating ecosystem monitoring for bird assemblages.
 
**TLDR**
 
I blended several CNNs taking 7-second spectrogram representations of .ogg bird call files. I employed stripe augmentations and mixup to improve the CNNs’ generalization to out of training domains. For inference, we predict on padded 5 sec snippets and refine the result with a metadata gradient boosting classifier and postprocessing. 

The domain shift from the training set, composed of short bird call recordings (train_short) to the test-set, composed of passively recorded natural soundscapes, resulted in a significant drop off in model performance at inference to the hidden test set. 
 
My solution achieved a top 9% result (solo bronze) and moved up 8 spots from the public LB (f1 = 0.68) to the private LB (f1 = 0.61).

I believe that fully incorporating the underlying ecological constraints at play is essential to accomplish the goal of this data product, namely, generating actionable biodiversity outcomes. 
 
**Validation**
 
There were 4 total sites in the hidden test-set, composed of passively recorded natural soundscapes that were approximately ten minutes long. Robust validation in this competition was difficult for a number of reasons. Firstly, the available sample of test data contained merely 35% of the total data, missed two of the four sites, and contained 3 full songs of nocalls. Secondly, there was a significant domain shift from the training data of short bird call audio files to the testing data of passively recorded natural soundscapes. Thirdly, many of the bird species were underrepresented in the training-set (roughly 1/3 had less than 100 instances), and the test-set likely contained species that were absent from the training set (possibly calling for [self-supervised learning networks](https://www.youtube.com/watch?v=Ag1bw8MfHGQ) for truly robust model performance in the test domain). I believe that self-supervised models capable of predicting out-of-training classes would generate more actionable biodiversity outcomes for model deployment (the main goal of BirdCLEF21 and LifeCLEF). 
 
In an attempt to correct for auto spatial correlation in the survey records, I implemented spatial 5-fold cross validation using the block technique. Because folding is somewhat redundant relative to the true train/test domain shift, I selected the best performing models across different seeds and modeling parameters, resulting in a bagged model with each of the 5 folds represented at least once and at most twice. Despite the redundancies in folding the training set, my cross-validation scheme is preferred to random splitting in respect to spatial auto correlations common to ecological survey data. In addition, model inference in the competition and performance in real-world deployment would be hindered by randomly leaving out 20% of the data, which could easily contain types of calls underrepresented in the data. 
 
The [blockCV](https://cran.r-project.org/web/packages/blockCV/vignettes/BlockCV_for_SDM.html) strategy employed spatially split the data into grids, doing so for each quarter of the year. Due to the density of surveys within the training set, I considered three large areas for the gridding scheme (North America, South America, and Europe), regions which had a high density of recordings, and otherwise randomly assigned folds for regions with a low density of recordings. The geospatial gridding forced the models to learn how to extrapolate in space from training folds to the the validation fold. Furthermore, the temporal splitting into yearly quarters ensured the 80/20 train/test split was preserved across time periods, so that seasonal patterns in the bird calls were captured in a representative manner. 
 
(Figure to come)
 
 
**Code and Data Pipeline**
 
I used `Google Drive` for code storage, `Neptune.ai` for experiment tracking, and `Google Colab` for model fitting in a high-RAM & GPU enabled environment. For the CNNs I used `PyTorch` with Resnest and EfficientNet backbones and for the Metadata classifier I used `Catboost`. Since I used [pre-computed mel-spectrograms](https://www.kaggle.com/kneroma/kkiller-birdclef-2021) for the CNNs there was no need for data versioning (Github for future storage with versioning). Additionally, the spectrograms were cached to memory before training to speed up CNN fitting. I performed the CNN augmentations (mixup, striping) on the GPU per batch to reduce CPU bottlenecking. 
 
**Bird Call CNNs**
  
My models were trained on the train_short clips and evaluated with the Public LB soundscapes. They were all trained on 7-sec crops of the train_short data, with up to ten spectrograms taken at the beginning of the files (35% of the clips had the max ten 7-sec crops). Taking longer 30 second clips would likely have been a better strategy (used by many of the top scorers), because longer snippets are superior among the weakly labeled data (unsure where the bird is calling). To account for the 5sec snippet format of test data, I padded the 5-sec clips at model inference to 7-sec. 
 
Backbones: [resnest50](https://www.kaggle.com/ttahara/resnest50-fast-package) (striping), [efficientnet-B3](https://www.kaggle.com/tunguz/efficientnet-pytorch-071) (mixup). Transfer weights from ImageNet. 
 
Model training in Colab for the resnests was ~2.5 hours (12 epochs), while training for the effnets was ~5.5 hours (55 epochs).
 
(Figure to come)
 
I trained with BCE loss using Adam optimizer and cosine annealing schedule. I saw improvements using the following tricks:
 
* Augmentations. Power transformation (random int between 0.5 and 3) so to randomly vary the contrast of the images for each batch. Striping vertically and horizontally across the images (for 80% of the samples). Mixup between images and updating the labels accordingly, using the standard FB Cifar10 params (for 50-100% of the samples, depending on the run).  
* Label smoothing. I used label smoothing to account for noisy annotations and absence of birds in “unlucky” 7sec crops. I used 0.0025 for zeros, 0.3 for secondary labels, and 0.995 for the primary label. 
* Next time: quality rating as weight on loss, with rating/max(ratings).
* Next time: add background pink noise
* Next time: consider other normalization methods for training. 
 
**Metadata Classifier**
 
In addition to the audio based neural networks, I also trained a gradient boosting learner based only on the metadata associated with each call. I incorporated nine features to predict the primary labels in the training set, leaving out secondary ones (all data used). The features included:

* 3 BioClims pertinent for bird assemblages ([Bender et al., 2017](https://www.nature.com/articles/s41598-019-53409-6)), forest type (categorical), grass cover, datetimes (e.g., 1-365), longitude, latitude, and elevation.
 
To extract these data I used the given coordinates to search for the associated faeture value on their raster surfaces. The BioClim rasters had a 5-arcmin resolution, while the land cover features were aggregated to match the BioClims. The numerical features were then subtracted by their mean and divided by their std so to z-score normalize the features. The Catboost model took approximately 1 hour to complete 1208 iterations on the GPU, with use-best-iteration enabled, yielding a f1 score of 0.18 on the randomly selected 20% validation set.  
 
(Figure to come)
 
For the real-world, a full and accurate incorporation of ecology and biogeography would be essential for the product's stability over time (and domain shift). Postprocessing was then employed to further incorporate these trends, aimed at improving the incorporation of the geospatial constraints (see below).
 
**Ensembling**
 
I bagged the probabilistic inferences to blend the models into an ensemble (predict_proba). Un-weighted averaging was employed for the same type of model in the 5 folds. I then used weighted averaging upon blending multiple models (aka both the stripe and mixup augmentations, as well as the metadata classifier). I could have used hyperparam tuning with hyperopt, but instead I opted for common sense first-guess and then refined from there, based on the public LB. In the end, I blended the metadata classifier at a 0.14 weight relative to the CNNs (with weight 1). 
 
 
**Postprocessing**
 
I then used a threshold to generate the labels from the raw probabilistic inferences. If any label had a prediction above the threshold, then that species was included in the final prediction (multiple label predictions were thus possible). If no labels received a prediction greater than the threshold, it received the nocall label. I used the given “training soundscapes” as the toy test set for tuning the threshold (as well as the public LB). I did this by calculating f1 scores for different thresholds, and plotted the results in matplotlib. I then randomly tested  thresholds on either side of the optimum, recording the public LB stats as they were generated to guide further hyperparam tinkering. 
 
* Next time: Bootstrapping of validation set
* Next time: Geospatial limitations
* Next time: Dynamic thresholding

 
Thanks goes to LifeCLEF, Kaggle, and the competitors. Cites: kkiller, Jan’s paper, 2nd place write up, 11 place write up.
