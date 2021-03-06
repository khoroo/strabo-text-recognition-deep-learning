# strabo-text-recognition-deep-learning Version 0.67

The goal of this project is to detect and recognize the text in the maps. Input
to the system is an image (jpeg or png). The output is a geo json image which
contains the coordinates of the text in the map along with the recognized text
in that area.

This document contains the installation and testing guide for Strabo.

### Library Requirement
The libraries you will need are shown below. They will be installed in the Section 1 `Installation`.
```
opencv-python==4.0.0.21
tensorflow==1.4
Shapely==1.5.17
Flask==1.0.2
matplotlib==3.0.3
scipy==0.19.0
plumbum==1.6.7
numpy==1.14.3
ipython==6.3.0
Pillow==5.2.0

tesseract-ocr==4.0.* 
libtesseract-dev==4.0.* 
libleptonica-dev==1.76.*  
```

###  Prerequisite
* Ubuntu OS

* pip for python3

## I. Installation

Here is the instruction for installing Strabo. The following commands
have been tested on Linux system with **Ubuntu 16.04.2 LTS distribution**. 

You should first download the `install.sh` from [here](https://drive.google.com/open?id=17Tat38W_M_4yaHS_dHTf2TakNaT-jQel)  and `StraboDependency.zip` from [here](https://drive.google.com/open?id=1MjBMO_Ql7kth7VPPX6XkDXW4sr1qtjDV) (Google Drive).

You do **NOT** need to clone this repo mannually to use Strabo. This operation is included in the installation steps. 

There are two methods to install Strabo (1.1 and 1.2), you can choose the one you prefer. 1.1 provides a user-friendly version of one-line-installation. 1.2 gives the step-to-step instructions. These two methods are essentially the same, you only need **one** of them (no need for running both).

### 1.1 Simple Installation
**We provide a install.sh file for your convinience if you want one-line-installation instead of following the commands below. You can simply type** `sh install.sh` **and it will install Strabo automatically.** (PS: virtual environment installation is not included in the install.sh file). When you use this install.sh file, please make sure it is in the same folder as StraboDependency.zip. Strabo will be installed in the **same** folder that your `install.sh` and `StraboDependency.zip` reside in. 

### 1.2 Customized installation
If you want to run Strabo inside virtual environment, and you do not have
the virtualenv installed, step 1 will help you with that. If you do not want
to use virtual environment or have it already installed, you can go to step 2
directly.

#### Step1 - Set up virtual environment (optional)

Download and install virtualenv

```
sudo apt-get install virtualenv
```

Create the directory to store all the environments
```
mkdir ~/Environments
cd ~/Environments
```
Create a new virtual environment and name it strabo_env.
```
virtualenv -p python3 strabo_env
```
Bring up the virtual environment
```
source strabo_env/bin/activate
```
Then you’ll see "(strabo_env)" ahead of the prompt, which indicates that the
strabo_env is up.
```
(strabo_env) zekun@zekun-ThinkPad-P50:~/Environments$
```

#### Step2 - Copy files

We have provided a zip file that contains necessary dependency files. We need
to extract the zip file in this step.

First go to the directory where the zip file resides in with the cd command.
We will refer to this directory as `<Strabo_Dep_DIR>`.

```
cd <Strabo_Dep_DIR>
```
If you don't have `unzip` installed, then install `unzip` via

```
sudo apt-get install unzip
```

Then extract the files by
```
unzip StraboDependency.zip
```
You should see the following output in the command line
```
Archive: StraboDependency.zip
creating: east_icdar2015_resnet_v1_50_rbox/
inflating: east_icdar2015_resnet_v1_50_rbox/checkpoint
inflating: east_icdar2015_resnet_v1_50_rbox/model.ckpt-49491.data-00000-of-00001
inflating: east_icdar2015_resnet_v1_50_rbox/model.ckpt-49491.index
inflating: east_icdar2015_resnet_v1_50_rbox/model.ckpt-49491.meta
inflating: text-detection-requirements.txt
```

#### Step3 - Install libraries
Install python3-dev and other softwares
```
sudo apt-get install python3-dev
sudo apt-get install software-properties-common
```

Install library for Shapely

```
sudo apt-get install libgeos-dev
```

Install other required libraries. This step will take some time.

```
sudo pip3 install -r ${Strabo_Dep_DIR}/text-detection-requirements.txt
```

#### Step4 - Download and install

Then download and install the core code for text detection and recognition.

```
sudo add-apt-repository -y ppa:alex-p/tesseract-ocr
sudo apt-get update
sudo apt-get install -y tesseract-ocr=4.0.* libtesseract-dev=4.0.* libleptonica-dev=1.76.*  
sudo pip3 install git+https://github.com/spatial-computing/tesserocr
git clone https://github.com/spatial-computing/strabo-text-recognition-deep-learning.git
export LC_ALL=C
```
#### Step5 - Save virtual env configuration (optional)

If you want to save the configurations and use it on other machines later, you
can run the following commandline and save the configurations into the require-
ments.txt file.

```
pip3 freeze --local > ~/Environments/requirements.txt
```

## II. Test with demo images

We already prepared 2 demo images in the strabo-text-recognition-deep-learning
folder: 1920-3.png and 1920-5.png.

The command to run strabo on testing image is:

```
cd strabo-text-recognition-deep-learning
python3 run_command_line.py --checkpoint-path <Strabo_Dep_DIR>/east_icdar2015_resnet_v1_50_rbox --image 1920-5.png --config configuration.ini
```
The output is stored in static/results/test2/. Each input image has an
output folder that starts with the image name. Each folder contains the input
and output image in detection phase, the output json files and final.txt.

Output in the terminal should look similar to this:

```
defaultdict(<class 'int'>, {'result_path': 'static/results/test2'})
image name is 1920-5.png
make: Entering directory '/opt/strabo-text-recognition-deep-learning/lanms'
make: 'adaptor.so' is up to date.
make: Leaving directory '/opt/strabo-text-recognition-deep-learning/lanms'
resnet_v1_50/block1 (?, ?, ?, 256)
resnet_v1_50/block2 (?, ?, ?, 512)
resnet_v1_50/block3 (?, ?, ?, 1024)
resnet_v1_50/block4 (?, ?, ?, 2048)
Shape of f_0 (?, ?, ?, 2048)

Shape of f_1 (?, ?, ?, 512)
Shape of f_2 (?, ?, ?, 256)
Shape of f_3 (?, ?, ?, 64)
Shape of h_0 (?, ?, ?, 2048), g_0 (?, ?, ?, 2048)
Shape of h_1 (?, ?, ?, 128), g_1 (?, ?, ?, 128)
Shape of h_2 (?, ?, ?, 64), g_2 (?, ?, ?, 64)
Shape of h_3 (?, ?, ?, 32), g_3 (?, ?, ?, 32)
2019-03-04 13:14:07.151536: I tensorflow/core/platform/cpu_feature_guard.cc:137] Your CPU su
here
3537 text boxes before nms
1913 text boxes before nms
1730 text boxes before nms
static/results/test2/1920-5.png_69f4e89c-3e7f-11e9-92bb-0242ac110004/result.json
40
static/results/test2/1920-5.png_69f4e89c-3e7f-11e9-92bb-0242ac110004/input.png
static/results/test2/1920-5.png_69f4e89c-3e7f-11e9-92bb-0242ac110004/output.png
static/results/test2/1920-5.png_69f4e89c-3e7f-11e9-92bb-0242ac110004/result.png
static/results/test2/1920-5.png_69f4e89c-3e7f-11e9-92bb-0242ac110004/geoJson1.json
python3 text_recognition.py -i static/results/test2/1920-5.png_69f4e89c-3e7f-11e9-92bb-0242a
4

```
The output is stored instatic/results/test2/. Each input image has an output folder that starts with the image name. Each folder contains the input and output image in detection phase, the output json files and final.txt. A sample pair of input and output images are shown in figure below.

![image_1](Playground/input.png)
![image_2](Playground/output.png)

You can also visualize the output using *QGIS* tool by loading the json file. The json file contains all the predicted bounding boxes.
![image_2](Playground/strabo.png)


## III. FAQ
1. RuntimeError: Failed to init API, possibly an invalid tessdata path: /usr/share/tesseract-ocr/tessdata/
```
git clone https://github.com/tesseract-ocr/tessdata.git
sudo mv tessdata /usr/share/tesseract-ocr/
```

2. Error Message: !strcmp(locale, "C") || !strcmp(locale, "C.UTF-8"):Error:Assert failed:in file baseapi.cpp, line 211
Illegal instruction (core dumped)

Type `export LC_ALL=C` in the command line

3.  Error Message: OSError: Could not find or load any library geos_c icts of variants ['libgeos_c.so.1', 'libgeos_c.so']

Install libgeos via  `sudo apt-get install libgeos-dev`


## Acknowledgments

* Special thanks to EAST [paper](https://arxiv.org/abs/1704.03155v2) and [code](https://github.com/argman/EAST)
* Special thanks to Tesseract https://github.com/tesseract-ocr/
