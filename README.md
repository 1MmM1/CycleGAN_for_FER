# CycleGAN_for_FER
Check out our [website](https://sites.google.com/cs.washington.edu/cyclegan-for-fer/home) for more information on our project!

## Usage
Below we explain how to set up our Python notebooks to train our CycleGANs to generate images and use the generated images to augment the FER2013 dataset during CNN training. Note that the instructions and code provided are intended to be run on [Google Colab](www.colab.research.google.com/).

### PyTorch CycleGAN
Please make sure to first download the [FER2013 Kaggle dataset](https://www.kaggle.com/c/challenges-in-representation-learning-facial-expression-recognition-challenge). It would be easiest to put the `fer2013.csv` file into your Google Drive in the same location as where you want to save your model checkpoints and images. For reference, the folder structure we used was the following:

```
MyDrive/
└── colab_files/
|   └── final_project/
|   |   ├── fer2013.csv                       # FER2013 dataset
|   |   └── logs/
|   |   |   ├── 0.1/
|   |   |   ├── 0.2/
|   |   |   └── 0.3/                          # files for experiment 0.3
|   |   |   |   ├── <E>_generated.npy         # generated images from emotion <E> to add to CNN
|   |   |   |   ├── log.pkl                   # log file
|   |   |   |   ├── test_images_<N>/          # test images from epoch <N>
|   |   |   |   ├── images/                   # images generated during training
|   |   |   |   ├── D_A/                      # reference discriminator checkpoints
|   |   |   |   ├── D_B/                      # target discriminator checkpoints
|   |   |   |   ├── G_A2B/                    # reference -> target generator checkpoints
|   |   |   |   └── G_B2A/                    # target -> reference  generator checkpoints
```

This colab file should work regardless of folder structure, as long as you make sure the following file path variables point to the correct place:

* `BASE_PATH`: the base folder for your files in your Google Drive
* `LOG_PATH`: folder to save all training logs and images
* `TEST_PATH`: folder to save your test images from a specific epoch
* `OUTPUT_PATH`: folder to save your generated images for the CNN
* `GEN_A2B_PATH`: folder to save reference -> target model checkpoints
* `GEN_B2A_PATH`: folder to save target -> reference model checkpoints
* `DISC_A_PATH`: folder to save reference discriminator model checkpoints
* `DISC_B_PATH`: folder to save reference target model checkpoints

### Keras CycleGAN
To run this notebook, please make sure to first download the [FER2013 Kaggle dataset](https://www.kaggle.com/c/challenges-in-representation-learning-facial-expression-recognition-challenge). It would be easiest to put the `fer2013.csv` file into your Google Drive in the same location as where you want to save your model checkpoints and images. For reference, the folder structure we used was the following:

```
MyDrive/
└── colab_files/
|   └── final_project/
|   |   ├── fer2013.csv                       # FER2013 dataset
|   |   └── logs/
|   |   |   ├── epoch_0/
|   |   |   ├── epoch_10/
|   |   |   └── epoch_20/                     # files for epoch 20
|   |   |   |   ├── <E>_new.npy               # generated images from emotion <E> to add to CNN
|   |   |   |   ├── <N>_Original_A            # test image <N> class A
|   |   |   |   ├── <N>_Reconstructed_A       # reconstructed image <N> from class B
|   |   |   |   ├── <N>_Translated_A          # image generated during training
|   |   |   |   ├── d_loss_<N>.h5             # discriminator loss
|   |   |   |   ├── g_loss_<N>.h5             # generator loss
```
This colab file should work regardless of folder structure, as long as you make sure the following file path variables point to the correct place:

* `BASE_PATH`: the base folder for your files in your Google Drive
* `LOGS_PATH`: folder to save your test images, losses and model weights from a specific epoch

Follow the instructions in the colab notebook to run and train the CycleGAN model.

### CNN
To run this notebook, please make sure to first download the [FER2013 Kaggle dataset](https://www.kaggle.com/c/challenges-in-representation-learning-facial-expression-recognition-challenge). It would be easiest to put the `fer2013.csv` file into your Google Drive in the same location as where you want to save your model checkpoints and images. For reference, the folder structure we used was the following:

```
MyDrive/
└── colab_files/
|   └── final_project/
|   |   ├── fer2013.csv                       # FER2013 dataset
|   |   └── data/
|   |   |   ├── logs/
|   |   |   |   ├── 0.1/
|   |   |   |   ├── 0.2/
|   |   |   |   └── 0.3/                      # files for experiment 0.3
|   |   |   |   |   ├── log.pkl               # log file

```

This colab file should work regardless of folder structure, as long as you make sure the following file path variables point to the correct place:

* `BASE_PATH`: the base folder for your files in your Google Drive
* `LOG_PATH`: folder to save all training logs
* `augmented_data_path`: folder to load synthesized data for data augmentation

Follow the instructions in the colab notebook to run and train the CNN model.


## How to run the notebooks
Now that everything has been set up, follow the instructions below to train, test, and generate images using our models.

### PyTorch CycleGAN
First, make sure everything is set up correctly by selecting the "Training the model" header and running all cells above it (you can use Runtime > Run before). This will make sure all packages/libraries are imported, the GPU and your Google Drive have been connected, and the functions are loaded. Then, follow the instructions in the "Training the model" section of the notebook to set your training parameters/constants and then you can train the CycleGAN.

Since loss is a usually a poor indicator of model correctness, we can only test the model by simply displaying generated images from the test set ("PublicTest"). The test set can be quite large, so we have also added saving functionality to our test function so that you can view the generated images along with the input in your Drive. Follow the instructions under the  "Testing the model" section in the notebook to generate and display test images.

If you would like to use your model to generate images for our CNN model, follow the instructions under the "Generating images" section in the notebook.

### Keras CycleGAN
To train the model, follow the instructions in the colab notebook.

### CNN
To train CNN before data augmentation, select "Preprocess Input And Data Augmentation" header and set "augment" to False. Run all the cells up to Evaluation. In the Evaluation section you can train the model for as many epochs as you prefer. Currently, it's set to be trained for 500 epochs. Also, you can choose which of the three implemented models you want to train by uncommenting the appropriate line.

After this step, set "augment" to True to load data generated by CycleGAN to be added to the dataset. Then follow the above instructions to run the CNN after data augmentation.

## References
The majority of our code was implemented by us, but we referenced several Github repositories in the process:
* https://github.com/aitorzip/PyTorch-CycleGAN/
* https://github.com/junyanz/CycleGAN/
* https://github.com/FrancescoSaverioZuppichini/ResNet
* https://github.com/ivadym/FER/
* https://github.com/yunjey/mnist-svhn-transfer/
* https://github.com/ivadym/FER
