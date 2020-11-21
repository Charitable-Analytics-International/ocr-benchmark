# CAI Meza - OCR Benchmarks

CAI Meza is a software system that receives cell phone photos of log books, digitizes their contents and inserts them into a database. Meza ‘reads’ the hand-written log-book through optical character recognition into a digitized database. Data can then be accessed by various stakeholders in the format they need for reporting and analysis. CAI Meza offers an affordable, reliable, easy and impactful solution so that remote, low-tech environments are able to get the critical data all stakeholders need at the lowest cost.

[Meza Promo Video](https://youtu.be/wlABTMQILg8) - A video explanation of the CAI Meza platform

CAI Meza currently supports Western Arabic Numerals, Eastern Arabic Numerals and Bubbles. For numerals, our neural network architectures use a CRNN-like model built in PyTorch. The models use a ResNet50 as a backbone and feature extractor, which feeds a 512-dimension latent vector to a bidirectional LSTM. For bubbles, our models splits the cell image to isolate each bubble and then uses a modified ResNet18 to detect if it's checked or not.

This repository contains the datasets we use to benchmark the accuracy of our system. It also contains scripts to benchmark the accuracy of other OCR providers such as,

- [Google Cloud Vision](https://cloud.google.com/vision/docs/ocr)
- [Amazon Textract](https://aws.amazon.com/textract/)
- [Microsoft Azure Cognitive Services](https://azure.microsoft.com/en-ca/services/cognitive-services/directory/vision/)


## Description of Charitable Analytics International

CAI helps organizations understand their data through concrete insights. We offer
unique and customized solutions to empower leaders doing social good. We focus on
tackling pressing real-world issues that have the biggest impact, with partners such as
the United Nations World Food Program and the National Democratic Institute. Our
core belief is that data technology can and should be a key tool in the mission to make
the world a better place.

![](logo.png)


## Datasets

The test data is composed of actual pictures of logbooks from our pilots in the Republic of Congo (except for estern arabic numerals, currently synthetic).

Images take two forms. In *test_data/full_images/*, the logbook images are in their raw format. In *test_data/cell_images/*, we cut the individual cells from the source images.

The *test_data/full_images/* directory also has a json file containing the shape of each potential template as Meza is configured to match incoming images with preloaded templates. As an aside, preloading templates is a feature that allows Meza to organize images and reference each extracted cell. It also allows it to automatically rotate the image if it's not upright.


### Full Images

This dataset is used to test the ability to take a raw image and cut it into its individual cells. It also comes with a *templates.json* file where the structure of the logbook is defined. The cell values can be found in the *values.json* file.

Directory = ./test_data/full_images/

Dataset Size = 6 images

Format : RGB images of varying width and height

Compression : JPEG


### Western Arabic Numerals

The images contain values expressed by this regex,

    ^[-]{0,1}[0-9]*[.,]{0,1}[0-9]*$

Dataset Size = 4451 cell images

Format : RGB images of varying width and height

Compression : JPEG


### Eastern Arabic Numerals

We have not yet collected field images containing the arabic script. Our handwritten dataset comes from [here](https://archive.ics.uci.edu/ml/datasets/PMU-UD).

The images contain values expressed by this regex,

    ^[-]{0,1}[٠-٩]*[.,]{0,1}[٠-٩]*$

Dataset Size = 1001 cell images

Format : RGB images of varying width and height

Compression : JPEG


### Bubbles

The images contain varying numbers of bubbles.

Dataset Size = 4642 cell images

Format : RGB images of varying width and height

Compression : JPEG


## Running the Benchmarks

The *run.ipynb* jupyter notebook contains the scripts to benchmark the different OCR providers on our test data. Here are the accuracy scores.


### Full Images

Here, accuracy is defined as the number of cells successfully cut out

1. CAI Meza = 100%

2. Amazon =


### Western Arabic Numerals

1. Human inter-coder agreement =

2. CAI Meza = 85%

3. Google =

4. Amazon =

5. Azure =


### Eastern Arabic Numerals

1. Human inter-coder agreement =

2. CAI Meza = 82%

3. Google =

4. Amazon =

5. Azure =


### Bubbles

1. Human inter-coder agreement =

2. CAI Meza = 96%

3. Google =

4. Amazon =

5. Azure =




## Author

* **Jean-Romain Roy** - *Primary Developer of CAI Meza* - [jeanromainroy](https://github.com/jeanromainroy)
