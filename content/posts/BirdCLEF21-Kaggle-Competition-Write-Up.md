---
title: "BirdCLEF21 Kaggle Competition Write Up."
date: 2021-06-19
katex: true
markup: "mmark"
---

## BirdCLEF21 Kaggle Competition Write Up.
---

The BirdCLEF21 Kaggle challenge tasked competitors to classify bird calls by species, with 397 target bird species as training classes. BirdCLEF21's goal fir bird call recognition AI is to streamline (by semi-automating) the monitoring of bird assemblages in natural settings. The competition's focus on actionable biodiversity outcomes was particularly intriguing to me (fitting into my interestes in [drive-train deployment](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwi0jMKQqKzxAhUDuZ4KHVvtDWQQFjAAegQIBRAD&url=https%3A%2F%2Fwww.oreilly.com%2Fradar%2Fdrivetrain-approach-data-products%2F&usg=AOvVaw2sfgvY74DrpoZ0EhghEGH4)]), and, as a result, I very thoroughly enjoyed the time I put into BirdCLEF21. 
 
**Solution TLDR**

My solution achieved a top 9% result (for solo bronze :)), moving up 8 spots relative to the competition from the public leaderboard (f1 = 0.68) to the private leaderboard (f1 = 0.61).
 
I blended several audio to spectogram CNNs by taking 7-sec spectrogram representations of the bird calls (.ogg files). I employed stripe augmentations and mixup to improve the CNNs’ generalization to out-of-training domains. For inference, I predicted on 5-sec snippets (padded to 7-sec) and refined the result with a metadata gradient boosting classifier, as well as with postprocessing. The shift from the training set, composed of short bird call recordings (train_short), to the test-set, composed of passively recorded natural soundscapes, resulted in a significant drop off in the models' f1 performance. For example, 1st place f1 decreased between the publice and private leaderboards by ~10%, 2nd place decreased by ~14%, and my solution decreased by ~10%. My instincts leads me to believe that deployment to natural settings (beyond the context of Kaggle) may result in even further f1 performance drop offs, a reality which is partially related to the shear number of bird species worldwide ([possibly 20k+](https://www.amnh.org/about/press-center/new-study-doubles-the-estimate-of-bird-species-in-the-world#:~:text=Birds%20are%20traditionally%20thought%20of,and%2010%2C000%20species%20of%20birds.).  
 
**Validation**
 
There were 4 different sites within the hidden test-set of passively recorded natural soundscapes, which were approximately ten minutes long. Robust validation was difficult for a number of reasons. For example, the available sample of test data (training soudscapes) contained merely 35% of the total data, missed two of the four sites, and contained 3 full songs of only nocall. There was also significant domain shifts from the training data (train_short) to the testing data (passively recorded natural soundscapes). In addition, many of the species were underrepresented in the training-set (roughly 1/3 had less than 100 instances), and many locations were lacking in survey density, for both large areas such as Africa and Polynesia and small areas such as several island chains. Deployment to under-represented locations would certainly not be advised. Furthermore, passively recorded natural soundscapes most likely contain species absent from the training set (calling for [self-supervised learning networks](https://www.youtube.com/watch?v=Ag1bw8MfHGQ) for more robust performance). I believe that self-supervised models capable of predicting out-of-training classes would generate more actionable biodiversity outcomes, the main goal of BirdCLEF, and I hope that the next iteration of the competition will include out-of-training species in the task.

To account for spatial correlation in the survey records, I implemented 5-fold cross validation using a block technique. The [blockCV](https://cran.r-project.org/web/packages/blockCV/vignettes/BlockCV_for_SDM.html) strategy I employed split the data into geospatial grids for each quarter of the year. Due to the density of surveys within the training set, I considered three large areas for the gridding scheme (North America, South America, and Europe), the regions which had a high density of recordings, and otherwise randomly assigned folds for the regions with a low density of recordings. This gridding forced the models to learn how to extrapolate in space from training folds to the the validation fold. Furthermore, the temporal splitting into yearly quarters ensured the 80/20 train/test split was preserved across time periods, so that seasonal patterns in the bird calls were captured in a representative manner. 

Because folding is somewhat redundant relative to the train/test shift in BirdCLEF21, I selected the best performing models across different seeds and modeling parameters, resulting in a bagged model with each of the 5 folds represented at least once and at most twice (I should have bagged with more random seeds, tip to myself for next time). Despite the redundancies in folding the training set, my cross-validation scheme was preferred to a random splitting scheme in respect to spatial auto-correlation, biases which are common to ecological survey data.
 
(Figure to come)
 
**Code and Data Pipeline**
 
I used `Google Drive` for code storage, `Neptune.ai` for experiment tracking, and `Google Colab` for model fitting in a high-RAM & GPU enabled environment. For the CNNs I used `PyTorch` with Resnest and EfficientNet backbones and for the Metadata classifier I used `Catboost`. Since I used [pre-computed mel-spectrograms](https://www.kaggle.com/kneroma/kkiller-birdclef-2021) for the CNNs there was no need for data versioning (Github for future storage with versioning). Additionally, the spectrograms were cached to memory before training to speed up CNN fitting. I performed the CNN augmentations (mixup, striping) on the GPU per batch to reduce CPU bottlenecking. 
 
**Bird Call CNNs**
  
My models were trained on the train_short clips and evaluated with the Public LB soundscapes. They were all trained on 7-sec crops of the train_short data, with up to ten spectrograms taken at the beginning of the files (35% of the clips had the max ten 7-sec crops). Taking ~30-sec clips would have been a better strategy (used by many of the top scorers), because longer snippets are superior among the weakly labeled data (unsure where the bird is calling). To account for the 5sec snippet format of test data, I padded the 5-sec clips at model inference to 7-sec. 
 
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

* 3 BioClims pertinent for bird assemblages ([Bender et al., 2017](https://www.nature.com/articles/s41598-019-53409-6)), forest type (categorical), grass cover, datetimes (e.g., 1-365), longitude, latitude, and elevation. ([raw .tif files](https://www.kaggle.com/dryanfurman/geospatialdatabirdclef)). 
 
To extract these data, I used the raster surface value at the given location (long/lat coordinates associated with each bird call instance). The BioClim rasters had a 5-arcmin resolution, while the land cover features were aggregated to match the BioClims. The numerical features were then subtracted by their mean and divided by their std so to z-score normalize the features. The Catboost model took approximately 1 hour to complete 1208 iterations on the GPU, with use-best-iteration enabled, yielding a f1 score of 0.18 on the randomly selected 20% validation set.  
 
(Figure to come)
 
For real-world deployment, an accurate incorporation of the ecology and biogeography would be essential for the product's stability over time (and domain shift). Postprocessing was then employed to further incorporate these trends, aimed at improving the incorporation of the geospatial constraints (see below).
 
**Ensembling**
 
I bagged the probabilistic inferences to blend the models into an ensemble (predict_proba). Un-weighted averaging was employed for the same type of model in the 5 folds. I then used weighted averaging upon blending multiple models (aka both the stripe and mixup augmentations, as well as the metadata classifier). I could have used hyperparam tuning with hyperopt, but instead I opted for common sense first-guess and then refined from there, based on the public LB. In the end, I blended the metadata classifier at a 0.14 weight relative to the CNNs (with weight 1). 
 
 
**Postprocessing**
 
I then used a threshold to generate the labels from the raw probabilistic inferences. If any label had a prediction above the threshold, then that species was included in the final prediction (multiple label predictions were thus possible). If no labels received a prediction greater than the threshold, it received the nocall label. I used the given training soundscapes as the toy test set for tuning the threshold against the public LB performance. I did this by calculating f1 scores for different thresholds, and plotted the results in matplotlib. I then randomly tested thresholds on either side of the maximum. 
 
* Next time: Bootstrapping of validation set
* Next time: Geospatial limitations
* Next time: Dynamic thresholding

 
Thanks goes to LifeCLEF, Kaggle, and the competitors. Cites: kkiller, Jan’s paper, 2nd place write up, 11 place write up.
