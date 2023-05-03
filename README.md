# First GAN with Flowers
Just something for QTM 347 (Dr. McAlister) @ Emory that group found interesting and worthy of further exploration (very rudimentary). This project was heavily inspired by a few other ones. They will be cited in the course of this article.

# Introduction 
This project uses the TensorFlow.keras architecture and the 102 Category Flower Dataset ([link](https://www.robots.ox.ac.uk/~vgg/data/flowers/102/index.html)) that was sourced from the web. In general, this project was a soft introduction to any sort of generative adversarial network and its capabilities in image generation as well as local behavior when it came to coding. 

# Dataset 
The dataset was limited to ~1000 for try 1 of our implementation and ~3000 for try 2 of our implementation. The link to the dataset is pasted in the previous section, and a tutorial on how to utilize this dataset is given from the website. The flowers were chosen as they were nicely scaled and simple images that would be relativeley easy to work with for a beginner. An example of the images will be displayed below: 

![image_00043](https://user-images.githubusercontent.com/98007808/235814354-6adfdde6-0aef-46eb-b285-9c5f9013ddb8.jpg)

# GANs
Much of the GAN architecture was based on a GitHub repository that utilized convolutional kernels to build both the discriminator and generator. Originally, the structure was used to generate pictures of clothing. The link to that project is [link](https://github.com/nicknochnack/GANBasics/blob/main/FashionGAN-Tutorial.ipynb). Some notable features of the FashionGAN include: 

- LeakyReLU activation used for all layers of generator except for last layer (Sigmoid).
- Use of a dense layer in the final layer of the discriminator
- Use of the Adam optimizer as well as the BinaryCrossEntropy metric for both generator and discriminator evaluation

For introduction on the topic of GANs, the following articles were of great help:
- [Basic Pseudocode Example / walkthrough](https://machinelearningmastery.com/how-to-code-the-generative-adversarial-network-training-algorithm-and-loss-functions/)
- [Non-image data tutorial](https://machinelearningmastery.com/how-to-develop-a-generative-adversarial-network-for-a-1-dimensional-function-from-scratch-in-keras/)
- [Basic Knowledge blog](https://danieltakeshi.github.io/2017/03/05/understanding-generative-adversarial-networks/)

# Training and Setup
The images were originally placed inside of a Google Drive folder that is shared on the main page of this repository. This required a mounting of the drive to the Google Colab environment ([tutorial](https://www.marktechpost.com/2019/06/07/how-to-connect-google-colab-with-google-drive/)). Image sizes were put through the preprocessing step (scaling), cached/prefetch, shuffled, and then batched. These were also done to allow the model to run smoothly. The generator and discriminator were then built and the functional class was coded and compiled. These steps can all be found in the .ipynb in the repository. Finally, the callback was constructed in order to monitor the process of each subsequent epoch. Some notable elements of the callback include: 
- saving of the models / overwriting every 5 models run (should be in same folder as code file)
- printing of loss metrics as well as corresponding epoch iteration number

Another important element of this training process was the two distinct ouptut image sizes passed to the layers of the neural network. Trial 1 gave 28 x 28 images while trial 2 gave 64 x 64 images. Trial 1 was performed with ~1000 training images while trial 2 was performed with ~3000 training images.

The following is an example output of a couple of epochs while the model is running:

<img width="478" alt="process" src="https://user-images.githubusercontent.com/98007808/235817852-a5f95cef-0174-4071-a84b-74d929e72b12.png">

# Results 

## Trial 1 (after ~300 epochs)

Keep in mind that these are 28 x 28!

<img width="698" alt="3001" src="https://user-images.githubusercontent.com/98007808/235822678-fc87441b-b492-41a2-bca3-8973df8222a6.png">
<img width="706" alt="30002" src="https://user-images.githubusercontent.com/98007808/235822687-26630dbb-266f-46a3-9127-602ff153daa9.png">

## Trial 2 (after ~40 epochs)

These will be in 64 x 64.

<img width="698" alt="4001" src="https://user-images.githubusercontent.com/98007808/235822901-e7cf8a73-14a9-4e20-8408-8048b6c04538.png">
<img width="697" alt="4002" src="https://user-images.githubusercontent.com/98007808/235822911-f70bbf63-be88-4443-8cf5-116a6ad8b8ad.png">

Unfortunately, due to computing restrictions, trial 2 was stopped after epoch 49. Utilization of further cloud computing materials would require a costly solution that students are not necessarily privy to. Additionally, loss metrics were not recorded, and in hindsight, that would have been a good idea. What was observed was the vastly faster convergence of smaller loss metrics once the training data size was increased and image dimensions were blown up.

# Future Pursuits
The biggest limitation on this project was computing resources. Most importantly, extensive use of platforms such as AWS or Google Cloud would have allowed for more flexible allocation of GPU's necessary for this project. Simple laptops would run the code very slowly and, unfortunately, that is what we have. Beyond computing, more training images (though requiring longer compute time) would also be a good idea. To combat symptoms of mode collapse as well as optimizatized computations, Wasserstein loss could be a possibility for the discriminator. Finally, more knowledge and experience with differing GAN architectures would be extremely helpful in navigating additional workings.
