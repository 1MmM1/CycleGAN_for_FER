# CycleGAN_for_FER
Check out our website for more information on our project!

## Google Drive setup

## Usage
Below we explain how to set up our Python notebooks to train our CycleGANs to generate images and use the generated images to augment the FER2013 dataset during CNN training. Note that the instructions and code provided are intended to be run on [Google Colab](colab.research.google.com/).

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

## How to run the notebooks
Now that everything has been set up, follow the instructions below to train, test, and generate images using our models.

### PyTorch CycleGAN
To train the model, you can simply select the "Training the model" header and run all cells above it (you can use Runtime > Run before). This will set up everything for training. Then, follow the instructions in the "Training the model" section of the notebook to set your training parameters/constants and then you can train the CycleGAN.

Since loss is a usually a poor indicator of model correctness, the we can only test the model by simply displaying generated images from the test set ("PublicTest"). Since the test set can be quite large, we have also added saving functionality to our test function so that you can view the generated images along with the input in your Drive. Follow the instructions under the  "Testing the model" section in the notebook to generate and display test images.

If you would like to use your model to generate images for our CNN model, follow the instructions under the "Generating images" section in the notebook.

## References
The majority of our code was implemented by us, but we referenced several Github repositories in the process:
* https://github.com/aitorzip/PyTorch-CycleGAN/
* https://github.com/junyanz/CycleGAN/
* https://github.com/FrancescoSaverioZuppichini/ResNet
* https://github.com/ivadym/FER/
* https://github.com/yunjey/mnist-svhn-transfer/
