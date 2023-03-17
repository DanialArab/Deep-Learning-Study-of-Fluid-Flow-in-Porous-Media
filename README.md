# Deep-Learning-Study-of-Fluid-Flow-in-Porous-Media

This work is a follow-up research on our previous publication, <a href="https://github.com/DanialArab/Random-Forest-Classifier-to-Characterize-Emulsions/" target="_blank" rel="noopener">link to its repo</a>. In this work, deep learning approach (modified unet) was applied to perform the semantic segmentation of microfluidic chips (please visit <a href="https://www.sciencedirect.com/science/article/abs/pii/S0920410522007045?via%3Dihub/" target="_blank" rel="noopener">here</a> for further details on the technical/non-ML parts). The model architecture is depicted in Fig. 1. The following bullet points are briefly summarized the architecture details:

* VGG16 was used as the backbone to extract the features (in the encoder part of the unet, as depicted in Fig. 1)


![](https://raw.githubusercontent.com/DanialArab/images/main/my_papers/architecture.PNG)

This approach is specifically useful when there is a high interaction between the injected chemical and the resident fluid. In these cases, there could be a high chance of complex emulsification (where there is not a sharp interface between the emulsified phase and the continuous phase, see red rectangle in figure below). In these cases, traditional ML algorithms may not be the best option for semantic segmentation: random forest is overestimated the oil saturation in the red rectangle. However, the segmentation accuracy is remarkably improved and the oil saturation in the same region (marked in the red rectangle) is precisely segmented. The intersection over union obtained for the testing datasets is averaged to ~97%. All the steps of the machine learning pipeline are detailed in the jupyter notebook attached to this repo.  


![](https://raw.githubusercontent.com/DanialArab/images/main/my_papers/deep_learning_vs_rf.PNG)

![](https://raw.githubusercontent.com/DanialArab/images/main/my_papers/prediction_unet.PNG)

![](https://raw.githubusercontent.com/DanialArab/images/main/my_papers/confusion%20table.png)
