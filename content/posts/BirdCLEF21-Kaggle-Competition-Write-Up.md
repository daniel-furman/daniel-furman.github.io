---
title: "BirdCLEF21 Kaggle Competition Write Up."
date: 2021-06-19
katex: true
markup: "mmark"
---

## BirdCLEF21 Kaggle Competition Write Up. 
### [[Code](https://nbviewer.jupyter.org/github/daniel-furman/RandomDS/blob/main/BirdCLEF21_Training.ipynb)]
---

Bird song recognition with AI has the potential to streamline (by semi-automating) scientific monitoring of bird assemblages. Faster identification of bird species in natural settings, as a result, equips land managers and policy-makers with a stronger understanding of environmental risks in ecological systems. The BirdCLEF21 Kaggle challenge brought state of the art in computer vision to bird song recognition, tasking competitors to classify species from bird calls into 397 target classes. The competition's focus on actionable biodiversity outcomes was particularly exciting (given my interest in the environment and [drive-train deployment](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwi0jMKQqKzxAhUDuZ4KHVvtDWQQFjAAegQIBRAD&url=https%3A%2F%2Fwww.oreilly.com%2Fradar%2Fdrivetrain-approach-data-products%2F&usg=AOvVaw2sfgvY74DrpoZ0EhghEGH4)). 
 
**Solution TLDR**

I blended several audio-based Convolutional Neural Networks (CNNs) taking up to 10 spectrogram representations of 7-sec segments per bird call file (raw .ogg's). I employed striping and mixup to improve the CNNs’ generalization to out-of-training domains. I then used the network for inference on the test-set (5-sec snippets padded to 7-sec), refining the predictions by blending a metadata gradient boosting classifier with weighted averaging. My solution achieved a top 9% result (solo bronze), improving 8 spots relative to the competition between the public (f1 = 0.68) and private (f1 = 0.61) leaderboards. Not bad for my first go at a feature competition! 

The shift from the training set (short bird call recordings, train_short) to the test-set (passively recorded natural soundscapes) resulted in significant performance drop off: 1st place's f1 score decreased by ~10%, 2nd place decreased by ~14%, while my solution decreased by ~10% (from the public to private leaderboards). I am led to believe that model deployment to real-world settings (beyond Kaggle) may result in even larger f1 performance drop offs, a reality which is partially related to the sheer number of bird species worldwide ([possibly 20k+](https://www.amnh.org/about/press-center/new-study-doubles-the-estimate-of-bird-species-in-the-world#:~:text=Birds%20are%20traditionally%20thought%20of,and%2010%2C000%20species%20of%20birds.)).  
 
**Validation**
 
The training set was composed of 63k+ recordings from the [Xeno-Canto](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwjNorSmtKzxAhVLqp4KHfNFBuMQFjAAegQICBAD&url=https%3A%2F%2Fwww.xeno-canto.org%2F&usg=AOvVaw1uRvDdPwcwVREypaRGQOPo) bird song database, ranging from 5-sec to minutes in duration. The hidden test-set, in contrast, contained passively recorded natural soundscapes (from 4 different sites) that were approximately ten minutes in duration. 

Robust validation here was difficult for a number of reasons: the public sample of test data (training soundscapes) available during the competition contained only 35% of the total data, missed two of the four sites, and contained 3 full songs of entirely nocall labels. There was also a significant domain shift from the training data (train_short) to the test-set, one of the fundamental challenges of using AI for bird song monitoring. In addition, many of the species were underrepresented in the training-set (roughly 1/3 had less than 100 instances), and many locations were lacking in data density, both for large areas (such as Africa and Polynesia) and small areas (such as several island chains). Furthermore, passively recorded natural soundscapes most likely contain species absent from the training set (calling for [self-supervised learning networks](https://www.youtube.com/watch?v=Ag1bw8MfHGQ) for more robust performance). I hope that the next iteration of the competition incorporates out-of-training species classes in some way.

I used [blockCV](https://cran.r-project.org/web/packages/blockCV/vignettes/BlockCV_for_SDM.html) to account for some of the spatial autocorrelation in the bird song records, a common bias in ecological data. I implemented 5-fold cross validation using this geospatial block technique, which split the data into grids.  Due to the density of surveys within the training set, I considered three large areas for the gridding scheme (North America, South America, and Europe), the regions which had a high density of recordings, and otherwise randomly assigned folds for the regions with a low density of recordings. To account for the seasonal trends in bird calls, I performed the blockCV splitting for samples constrained to a single quarter of the year (3 regions x 4 quarters = 12 samples). Finally, I concatenated the fold arrays and merged them with the metadata dataframe for use during model training.

<p align="center"> <img src="/posts/birdclefBlockCV.png"/ width = "550" height = "700"> </p>

The gridding forced the models to extrapolate in space between the training and validation folds, hopefully yielding a more generalizable classifier. Furthermore, the temporal splitting into yearly quarters ensured that the 80% to 20% train to test split was preserved across each quarter of the year, so that seasonal bird song patterns were captured in a more representative manner. Because cross-validation folding is partially redundant in relation to the true train/test shift in BirdCLEF21, I selected the best models from different seeds and (subtly altered) hyper-parameters, resulting in a bagged model with each of the 5 folds represented at least once (I should have bagged with more random seeds, tip to myself for next time). Despite these issues with folding, blockCV was preferable to a random splitting scheme in respect to correcting spatial autocorrelation, a set of biases which would further inflate validation metrics relative to the true modeling performance.
  
**Code and Data Pipeline**
 
I used `Google Drive` for code storage, `Neptune.ai` for experiment tracking, and `Google Colab` for model fitting in a high-RAM & GPU enabled environment. For the CNNs I used PyTorch with Resnest and EfficientNet backbones, and I used Catboost for the metadata classifier, both trained on GPU. Since I used [pre-computed mel-spectrograms](https://www.kaggle.com/kneroma/kkiller-birdclef-2021) for the CNNs there was no need for data versioning (Github for future storage with versioning). Additionally, the spectrograms were cached to memory before training to speed up CNN fitting. I performed the CNN augmentations (mixup, striping) on the GPU per batch to reduce CPU bottlenecking. 
 
**Bird Call CNNs**
  
My models were trained on the train_short clips and evaluated with the Public LB soundscapes. They were all trained on 7-sec crops of the train_short data, with up to ten spectrograms taken at the beginning of the files (35% of the clips had the max ten 7-sec crops). Taking ~30-sec clips would have been a better strategy (used by many of the top scorers), because longer snippets are superior among the weakly labeled data (unsure where the bird is calling). To account for the 5sec snippet format of test data, I padded the 5-sec clips at model inference to 7-sec. 
 
Backbones: [resnest50](https://www.kaggle.com/ttahara/resnest50-fast-package) (striping), [efficientnet-B3](https://www.kaggle.com/tunguz/efficientnet-pytorch-071) (mixup), both with transfer learning weights set from ImageNet.  
 
Model training in Colab for the resnests was ~2.5 hours (12 epochs), while training for the effnets was ~5.5 hours (55 epochs).
  
I trained with BCE loss using Adam optimizer and cosine annealing schedule. I saw improvements using the following tricks:
 
 * Augmentations. Power transformation (random int between 0.5 and 3 per batch) varies the contrast of the spectrograms. Striping vertically and horizontally across the images (for a random 80% of the samples). Mixup between images (and updating the labels accordingly) using the standard FB Cifar10 params.
 * Label smoothing. I used label smoothing to account for noisy annotations and absence of birds in “unlucky” 7sec crops. I used 0.0025 for zeros, 0.3 for secondary labels, and 0.995 for the primary label. 
 * Next time: Quality rating as weight on loss, with rating/max(ratings).
 * Next time: Add background pink noise
 * Next time: Consider other normalization methods for training. 
 
**Metadata Classifier**
 
In addition to the audio based neural networks, I also trained a gradient boosting learner based only on the metadata associated with each call. I incorporated nine features to predict the primary labels in the training set, leaving out secondary ones (all data used). The features included:

 * 3 BioClims pertinent for bird assemblages ([Bender et al., 2017](https://www.nature.com/articles/s41598-019-53409-6)), forest type (categorical), grass cover, datetimes (e.g., 1-365), longitude, latitude, and elevation. [[raster .tif modeling features](https://www.kaggle.com/dryanfurman/geospatialdatabirdclef)] 
 
To extract these data, I used the raster surface value at the given location (long/lat coordinates associated with each bird call instance). The BioClim rasters had a 5-arcmin resolution, while the land cover features were aggregated to match the BioClims. The numerical features were then subtracted by their mean and divided by their std so to z-score normalize the features. The Catboost model took approximately 1 hour to complete 1208 iterations on the GPU, with use-best-iteration enabled, yielding a f1 score of 0.18 on the randomly selected 20% validation set.  
 
<p align="center"> <img src="/posts/birdclef_shap.png"/ width = "625" height = "362"> </p>
 
For real-world deployment, an accurate incorporation of the ecology and biogeography would be essential for the product's stability over time (and domain shift).

**Ensembling**
 
I bagged the probabilistic inferences to blend the models into an ensemble (predict_proba). Un-weighted averaging was employed for the same type of model in the 5 folds. I then used weighted averaging upon blending multiple models (aka both the stripe and mixup augmentations, as well as the metadata classifier). I could have used hyperparam tuning with hyperopt, but instead I opted for common sense first-guess and then refined from there, based on the public LB. In the end, I blended the metadata classifier at a 0.14 weight relative to the CNNs (with weight 1). 
 
 
**Postprocessing**
 
I used a postprocessing threshold to generate the species labels from the tensors of probabilistic inferences. If a class had a probability above this threshold, then the species was included in the prediction (multi-labeling enabled). If none of the labels received a probability greater than the threshold, the instance received the nocall label. More postprocessing to come in BirdCLEF22 (which has already been confirmed)!
 
 * Next time: Bootstrapping of validation set for robust validation
 * Next time: Geospatial limitations as a postprocessing step for each site
 * Next time: Dynamic thresholding per test clip for any species at a high predicted probability

**Bibliography**

Thanks goes to LifeCLEF, Kaggle, and all the other (815) competitors. Cites: [kkiller's spectrograms](https://www.kaggle.com/kneroma/kkiller-birdclef-2021), [Paper 181 BirdCLEF2018](http://ceur-ws.org/Vol-2125/paper_181.pdf), [2nd place write up](https://www.kaggle.com/c/birdclef-2021/discussion/229995), [11 place write up](https://www.kaggle.com/c/birdclef-2021/discussion/243360).

**P.S. Ecological Contexts**

BirdCLEF cites its main goal as generating actionable biodiversity outcomes, a goal that is necessarily related to the underlying ecology and biogeography at play. 

 * The goal of ecology is to describe species communities in natural settings, at various temporal and geospatial scales, ultimately across the entire biosphere.
 * Biogeographic barriers constrain species distributions and abundance in ecological systems. 
 * Describing community structures is difficult due to the complexity of multispecies assemblages. 
 * The retrieval of ecological survey data includes many biases: observer, species detectability, technique, habitat, weather, and sampling representation. For BirdCLEF21's Xeno-Canto bird song data, species detectability biases (certain birds have softer calls, not as recorded), habitat & weather biases (can't retrieve data from certain areas), and sampling representation biases (1/3 of the classes had less than 100 instances) played a role. 
 
Overall, ecological models critical trade-off between specificity and generality, either capable of predicting species distributions/abundance at current conditions (specific model) or under changing conditions (generalizable model). For bird call recognition real-world deployment, the specificity/generality of the model would probably vary by site and vary by objective. The repeated nature of the (annual) BirdCLEF competition is a huge plus in terms of updating the models to generalize under domain shifts due to changing environmental conditions. 


