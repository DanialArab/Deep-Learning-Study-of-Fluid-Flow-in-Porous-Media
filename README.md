# Deep-Learning-Study-of-Fluid-Flow-in-Porous-Media

This work is a follow-up research on our previous publication, <a href="https://github.com/DanialArab/Random-Forest-Classifier-to-Characterize-Emulsions/" target="_blank" rel="noopener">link to its repo</a>. In this work, deep learning approach (modified unet) was applied to perform the semantic segmentation of microfluidic chips (please visit <a href="https://www.sciencedirect.com/science/article/abs/pii/S0920410522007045?via%3Dihub/" target="_blank" rel="noopener">here</a> for further details on the technical/non-ML parts). The model architecture is depicted in Fig. 1. The following bullet points briefly summarize the architecture details:

* VGG16 was used as the backbone to extract the features (i.e., in the encoder part of the unet, as depicted in Fig. 1)
* The transfer learning was leveraged to initialize the model with the optimized weights obtained from pre-training on ImageNET
* Backbone was frozen and fine-tuning was leveraged to continue continue training and updating the weights on the decoder path (fine-tuned on the training dataset)
* Batch normalization was applied to the output of the activation function in every layer, before passing it to the next layer, to ensure improved performance and stability of the model during training.

![](https://raw.githubusercontent.com/DanialArab/images/main/my_papers/architecture.PNG)
Fig. 1: Modified unet architecture 

The segmentation result for one of the testing images is shown in Fig. 2. As shown, the modified unet segmentation is precisely comparable with the ground truth, presented in the middle. Also, very tiny oil droplets, marked in the red circles in Fig. 2, are segmented well. 

![](https://raw.githubusercontent.com/DanialArab/images/main/my_papers/prediction_unet.PNG)

Fig. 2: Modified unet result: left) original image, middle) ground truth, and right) modified unet prediction 

This approach is specifically useful when there is a high interaction between the injected chemical and the resident fluid. In these cases, there could be a high chance of complex emulsification (where there is not a sharp interface between the emulsified phase and the continuous phase, see red rectangle in Fig. 3). In these cases, traditional ML algorithms may not be the best option for semantic segmentation: random forest is overestimated the oil saturation in the red rectangle. However, the segmentation accuracy of modified unet model is remarkably improved and the oil saturation in the same region in the same image (marked in the red rectangle) is precisely segmented out. The intersection over union obtained for the testing datasets is averaged to ~97%.

![](https://raw.githubusercontent.com/DanialArab/images/main/my_papers/deep_learning_vs_rf.PNG)
Fig. 3: Comparison of traditional ML (random forest classifier) with modified unet classifier 

The confusion table containing information for all the testing images dataset is shown in Fig. 4. As shown, true positive prediction is around 98.5%, which is remarkably accurate. Also, the average precision, recall, and f1-score are 0.978, 0.976, 0.977, respectively. All the steps of the machine learning pipeline are detailed in the jupyter notebook attached to this repo.  

![](https://raw.githubusercontent.com/DanialArab/images/main/my_papers/confusion%20table.png)

Fig. 4: Confusion table summarizing the accuracy of the modified unet model 
