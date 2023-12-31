# Geo-Localization

Ground-to-Aerial Image Geo-Localization with A Hard Exemplar Reweighting Triplet Loss

Abstract:

Geo-localisation refers to the process of precisely locating the geographical location or position of an object. Identifying an object's position on Earth using its longitude and latitude helps us to pinpoint its exact location with respect to any other location which is used in various applications such as GPS, mapping, etc. Drones, also known as unmanned aerial vehicles (UAVs), have risen in popularity in recent years due to their capacity to collect high-quality multimedia data from the sky. Applications including aerial photography, videography, mapping, agriculture, geo-localization, drone delivery, event detection and distribution have all become much more feasible as a result.
The first task is Drone-view target localization which involves locating the target building by finding the most similar satellite-view image for a given drone-view image. The second task is Drone navigation which involves the drone finding the most relevant place in its flight history to navigate back to the target place in a given satellite-view image.


![image](https://github.com/abineha/Geo-Localization/assets/101180980/1cec58c9-88d0-4270-95fe-fa70633cc51b)


 
 Figure 1: A cross-view matching example between three platforms, i.e., satellite, drone and ground. 


The motivation is to simulate the real- world geo-localization scenario by utilizing an extremely large satellite-view pool. We have used the current University-1652 dataset with extra 167,486 satellite- view gallery distractors. These distractor satellite- view images have a size of 1024 × 1024 and are obtained by cutting orthophoto images of real urban and surrounding areas.

We have imported the pretrained networks, such as AlexNet, VGG16, ResNet and DenseNet in pytorch. The pretrained networks help in achieving a better performance as it preserves some good visual patterns from ImageNet.

ResNet (Residual Network) is a specific type of convolutional neural network (CNN). It is commonly used in computer vision applications. Since we are using data from three different platforms, they may not share the same low-level patterns and thus the model is modified to use the backbone without sharing weights. After preparing the data folder and training models, we completed the training phase. The testing phase involves loading the network weight, from the trained data model, to extract the visual feature of every image. Thus, we imported the model structure and then loaded the weight to the model. For every query and gallery image, we extracted the feature by simply forwarding the data. Then, to evaluate the precision we sorted the predicted similarity score after matching the images by features. There are two kinds of images to be considered as not right-matching images. Those include mis-detected images and images of same identity in same cameras. 

To enhance the network training with instance-wise exemplars, we used the Hard Exemplar Reweighting Triplet Loss strategy which is based on triplet reweighting. Given a triplet of anchor Ai, its associated positive exemplar Pi, and negative exemplar Ni,k in an mini-batch, the original triplet loss is defined as: 
 
 Ltri(Ai , Pi , Ni,k) = max(0, m + dp(i) − dn(i, k))
 
 where m is the max-margin, dp(i) represents the squared Euclidean distance between Ai and Pi , dn(i, k) represents the squared Euclidean distance between Ai and Ni,k. 

The triplet loss strategy ensures that two examples with the same label have their embeddings close together in the embedding space and two examples with different labels have their embeddings far away.

Thus, we have designed a cross-view geo-localization method by matching ground-view images to aerial images and utilized the Hard Exemplar Reweighting Triplet Loss to improve the precision of the model.

