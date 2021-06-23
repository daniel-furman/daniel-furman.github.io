---
title: "BirdCLEF21 Kaggle Competition Write Up."
date: 2021-06-19
katex: true
markup: "mmark"
---

## BirdCLEF21 Kaggle Competition Write Up.
---

Bird song recognition with AI has the potential to semi-automate bird assemblage monitoring, equipping scientists, land managers, and policy makers with a better understanding of environmental risks. The BirdCLEF21 Kaggle challenge involved species classification on bird calls, with 397 target species for training classes. The competition's focus on actionable biodiversity outcomes was particularly exciting (given my interest in [drive-train deployment](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwi0jMKQqKzxAhUDuZ4KHVvtDWQQFjAAegQIBRAD&url=https%3A%2F%2Fwww.oreilly.com%2Fradar%2Fdrivetrain-approach-data-products%2F&usg=AOvVaw2sfgvY74DrpoZ0EhghEGH4)). As a result, I very thoroughly enjoyed the time I put into BirdCLEF21. 
 
**Solution TLDR**

My solution achieved a top 9% result (for solo bronze), improving 8 spots between the public (f1 = 0.68) to the private (f1 = 0.61) leaderboards. Not bad for my first go at a feature competition! I blended several audio-based Convolutional Neural Networks (CNNs) by taking up to 10 7-sec spectrograms of the bird calls per audio file (raw .ogg's). I employed striping and mixup to improve the CNNs’ generalization to out-of-training domains. I predicted on 5-sec snippets (padded to 7-sec), refining the results by blending a metadata gradient boosting classifier. The shift from the training set (short bird call recordings, train_short) to the test-set (passively recorded natural soundscapes) resulted in performance decreases upon deployment. 1st place's f1 score decreased (from the public to private leaderboards) by ~10%, 2nd place decreased by ~14%, while my solution decreased by ~10%! My instincts leads me to believe that deployment to natural settings (beyond Kaggle) may result in larger f1 drop off, a reality which is partially related to the shear number of bird species worldwide ([possibly 20k+](https://www.amnh.org/about/press-center/new-study-doubles-the-estimate-of-bird-species-in-the-world#:~:text=Birds%20are%20traditionally%20thought%20of,and%2010%2C000%20species%20of%20birds.)).  
 
**Validation**
 
The training set was composed of 63k+ recordings from the [Xeno-Canto](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwjNorSmtKzxAhVLqp4KHfNFBuMQFjAAegQICBAD&url=https%3A%2F%2Fwww.xeno-canto.org%2F&usg=AOvVaw1uRvDdPwcwVREypaRGQOPo) database of bird songs, ranging from 5-sec to minutes in duration. In contrast, the hidden test-set contained passively recorded natural soundscapes (from 4 different sites) that were approximately ten minutes long. Robust validation was difficult for a number of reasons: the public sample of test data (training soudscapes) available during the competition contained only 35% of the data, missed two of the four sites, and contained 3 full songs of entirely nocall labels. There was also significant domain shift from the training data (train_short) to the test-set, one of the fundamental challenges of using AI for bird song monitoring. 

In addition, many of the species were underrepresented in the training-set (roughly 1/3 had less than 100 instances), and many locations were lacking in data density, both for large areas (such as Africa and Polynesia) and small areas (such as several island chains). Deployment to under-represented locations would certainly not be advised, at least for models trained on this dataset. Furthermore, passively recorded natural soundscapes most likely contain species absent from the training set (calling for [self-supervised learning networks](https://www.youtube.com/watch?v=Ag1bw8MfHGQ) for more robust performance). I believe that self-supervised models capable of predicting out-of-training classes would generate more actionable biodiversity outcomes, the main goal of BirdCLEF, and I hope that the next iteration of the competition will include out-of-training species in the task.

In an attempt to account for some of the spatial correlations in the bird song records, I implemented 5-fold cross validation using a block technique. The [blockCV](https://cran.r-project.org/web/packages/blockCV/vignettes/BlockCV_for_SDM.html) strategy I employed split the data into geospatial grids for each quarter of the year. Due to the density of surveys within the training set, I considered three large areas for the gridding scheme (North America, South America, and Europe), the regions which had a high density of recordings, and otherwise randomly assigned folds for the regions with a low density of recordings. This gridding forced the models to learn how to extrapolate in space from training folds to the the validation fold. Furthermore, the temporal splitting into yearly quarters ensured the 80/20 train/test split was preserved across time periods, so that seasonal patterns in the bird calls were captured in a representative manner. 

Due to the fact that cross-validation folding is partially redundant here (relative to the train/test shift in BirdCLEF21), I selected the best performing models across different seeds and subtly changing hyper-parameters, resulting in a bagged model with each of the 5 folds represented at least once and at most twice (I should have bagged with more random seeds, tip to myself for next time). Despite the redundancies in folding the training set, my cross-validation scheme was preferred to a random splitting scheme in respect to spatial auto-correlation, biases which are common to ecological survey data.
 
<p align="center"> <img src="/posts/birdclefBlockCV.png"/ width = "550" height = "725"> </p>
 
**Code and Data Pipeline**
 
I used `Google Drive` for code storage, `Neptune.ai` for experiment tracking, and `Google Colab` for model fitting in a high-RAM & GPU enabled environment. For the CNNs I used PyTorch with Resnest and EfficientNet backbones and for the Metadata classifier I used Catboost, both trained on GPU. Since I used [pre-computed mel-spectrograms](https://www.kaggle.com/kneroma/kkiller-birdclef-2021) for the CNNs there was no need for data versioning (Github for future storage with versioning). Additionally, the spectrograms were cached to memory before training to speed up CNN fitting. I performed the CNN augmentations (mixup, striping) on the GPU per batch to reduce CPU bottlenecking. 
 
**Bird Call CNNs**
  
My models were trained on the train_short clips and evaluated with the Public LB soundscapes. They were all trained on 7-sec crops of the train_short data, with up to ten spectrograms taken at the beginning of the files (35% of the clips had the max ten 7-sec crops). Taking ~30-sec clips would have been a better strategy (used by many of the top scorers), because longer snippets are superior among the weakly labeled data (unsure where the bird is calling). To account for the 5sec snippet format of test data, I padded the 5-sec clips at model inference to 7-sec. 
 
Backbones: [resnest50](https://www.kaggle.com/ttahara/resnest50-fast-package) (striping), [efficientnet-B3](https://www.kaggle.com/tunguz/efficientnet-pytorch-071) (mixup). Transfer weights from ImageNet. 
 
Model training in Colab for the resnests was ~2.5 hours (12 epochs), while training for the effnets was ~5.5 hours (55 epochs).
  
I trained with BCE loss using Adam optimizer and cosine annealing schedule. I saw improvements using the following tricks:
 
* Augmentations. Power transformation (random int between 0.5 and 3 per batch) varies the contrast of the spectograms. Striping vertically and horizontally across the images (for a random 80% of the samples). Mixup between images (and updating the labels accordingly) using the standard FB Cifar10 params.
* Label smoothing. I used label smoothing to account for noisy annotations and absence of birds in “unlucky” 7sec crops. I used 0.0025 for zeros, 0.3 for secondary labels, and 0.995 for the primary label. 
* Next time: Quality rating as weight on loss, with rating/max(ratings).
* Next time: Add background pink noise
* Next time: Consider other normalization methods for training. 
 
**Metadata Classifier**
 
In addition to the audio based neural networks, I also trained a gradient boosting learner based only on the metadata associated with each call. I incorporated nine features to predict the primary labels in the training set, leaving out secondary ones (all data used). The features included:

* 3 BioClims pertinent for bird assemblages ([Bender et al., 2017](https://www.nature.com/articles/s41598-019-53409-6)), forest type (categorical), grass cover, datetimes (e.g., 1-365), longitude, latitude, and elevation. [[raster .tif modeling features](https://www.kaggle.com/dryanfurman/geospatialdatabirdclef)] 
 
To extract these data, I used the raster surface value at the given location (long/lat coordinates associated with each bird call instance). The BioClim rasters had a 5-arcmin resolution, while the land cover features were aggregated to match the BioClims. The numerical features were then subtracted by their mean and divided by their std so to z-score normalize the features. The Catboost model took approximately 1 hour to complete 1208 iterations on the GPU, with use-best-iteration enabled, yielding a f1 score of 0.18 on the randomly selected 20% validation set.  
 
<p align="center"> <img src="/posts/birdclef_shap.png"/ width = "650" height = "380"> </p>
 
For real-world deployment, an accurate incorporation of the ecology and biogeography would be essential for the product's stability over time (and domain shift).

**Ensembling**
 
I bagged the probabilistic inferences to blend the models into an ensemble (predict_proba). Un-weighted averaging was employed for the same type of model in the 5 folds. I then used weighted averaging upon blending multiple models (aka both the stripe and mixup augmentations, as well as the metadata classifier). I could have used hyperparam tuning with hyperopt, but instead I opted for common sense first-guess and then refined from there, based on the public LB. In the end, I blended the metadata classifier at a 0.14 weight relative to the CNNs (with weight 1). 
 
 
**Postprocessing**
 
I then used a threshold to generate the labels from the raw probabilistic inferences. If any label had a prediction above the threshold, then that species was included in the final prediction (multiple label predictions were thus possible). If no labels received a prediction greater than the threshold, it received the nocall label. I used the given training soundscapes as the toy test set for tuning the threshold against the public LB performance. I did this by calculating f1 scores for different thresholds, and plotted the results in matplotlib. I then randomly tested thresholds on either side of the maximum. 
 
* Next time: Bootstrapping of validation set for robust validation
* Next time: Geospatial limitations as a postprocessing step for each site
* Next time: Dynamic thresholding per test clip for any species at a high predicted probability

**Bibliography**

Thanks goes to LifeCLEF, Kaggle, and all the other (815) competitors. Cites: [kkiller's spectograms](https://www.kaggle.com/kneroma/kkiller-birdclef-2021), Jan’s paper, [2nd place write up](https://www.kaggle.com/c/birdclef-2021/discussion/229995), [11 place write up](https://www.kaggle.com/c/birdclef-2021/discussion/243360).

**P.S. Ecological Contexts**

After reading up on LifeCLEF's BirdCLEF competition, I quickly realized that my notes from Prof. William's Community Ecology course (taken while abroad at JCU in Queensland, Aus) were quite pertinent to both the Kaggl competition and the associated LifeCLEF conference. 

BirdCLEF cites its main goal as generating actionable biodiversity outcomes, a goal that is necessarily related to the underlying ecology. 


