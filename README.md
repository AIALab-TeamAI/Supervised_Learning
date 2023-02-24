# Supervised_Learning-[LECTURE](https://cs.nyu.edu/~yann/talks/lecun-ranzato-icml2013.pdf)

# Supervised_Learning-ANNOTATION

## _ANNOTATION for 2D IMAGE_
### 1. Annotation tools. 

**A. Object detection**

*a. One-stage (YOLO family, SSD-Net, FCOS,etc.)*

This is the common structure.
![pic1](https://github.com/AIALab-TeamAI/Supervised_Learning/blob/main/src_img/single_stage_object_detection.png)

*b. Two-stage (R-CNN family.etc)*

This is the common structure
![pic2](https://github.com/AIALab-TeamAI/Supervised_Learning/blob/main/src_img/two_stage_object_detection.png)) 

=> Case 1: You will annotation the boxs that contain the objects we want to recognize. The [LableImg](https://github.com/heartexlabs/labelImg) tool is chosen for this task.

=> Case 2: You want to lable the oriented bounding box. The [roLabelImg](https://github.com/cgvict/roLabelImg) tool is used for this purpose.

**B. Instance segmentation**

*a. One-stage (YOLACT, SOLOv1-2, BlendMask, CenterMask, CondInst, BoxInst-Based FCOS, etc.)*

This is the SOLOv2 structure.
![pic3](https://github.com/AIALab-TeamAI/Supervised_Learning/blob/main/src_img/single_stage_instance_segmentation.png)

*b. Two-stage (Mask-RCNN, Rotated Mask-RCNN, MaskLab,etc.)*

This is the MASK-RCNN structure.
![pic4](https://github.com/AIALab-TeamAI/Supervised_Learning/blob/main/src_img/two_stage_instance_segmentation.PNG)

=> For this task, you use this [Labelme](https://github.com/zhong110020/labelme) tool to annotate polygon of object.

**_After that:_**

**+ We should convert to standard format of the deep learning model.**

**+ Go to the _CONVERT-FORAMT_ to select one convertion method.**

### 2. Online annotation using Roboflow.

=> Following the [Roboflow](https://docs.roboflow.com/) for implementation.


## _ANNOTATION for 3D POINT CLOUD_

### 1. Install Mesh_Labeler-main.zip

### 2. 3D_segmentation_annotation.

### 3. You should prepare dataset that is separated and save each part into a folder.

** _First, run B1.py: create new enviroment._

***_To run this code, you should install librarys:_

- pip install open3d-python (version --0.7.00)
- pip install plyfile
- (1) You should fix something about  input and output folder direction to match your folder
- (2) Eg: run code "python B1.py -i /home/airlab/Desktop/Annotation3D/DATACUTTING/ -o /home/airlab/Desktop/Annotation3D/DATA/"
- After you select object for train and test. And save it into two folder named: "DATATRAIN and DATATEST".

** _Then run B2.py: create new enviroment._

***_Intruction: create new enviroment_ 

- (1) Install: 
 -  pip install open3d=0.13.0.0
 -  pip install plyfile
 -  add d3 folder
- (2) you should fix something about direction
    * Eg: run code: "python B2.py -i /home/airlab/Desktop/Annotation3D/DATATRAIN" and "python B2.py -i /home/airlab/Desktop/Annotation3D/DATATEST".
    
** _Library is to process 3D point cloud:_

- open3d
- plyfile
- trimesh
- pyVista
- openGL
- PCL with C++
This project is a work in progress.

# Supervised_Learning-BUILD MODEL DL

## _FRAMEWORK for DEEP LEARNING_

- There are many framework used for developming DL such as [Tensorflow](https://www.tensorflow.org/tutorials/quickstart/beginner), [Pytorch](https://pytorch.org/tutorials/beginner/pytorch_with_examples.html), [Caffe](https://recodeminds.com/blog/a-beginners-guide-to-caffe-for-deep-learning/), [ONNX](https://onnx.ai/),Keras, etc.
- TensorFlow and Pytorch are well-know in Deep Leaning model.
- TensorFlow for academia.
- Pytorch for developming applicatioon.
- ONNX for real-time model.   

## _PLATFORM for DEEP LEARNING_

- [Detectron2](https://detectron2.readthedocs.io/en/latest/tutorials/index.html) is generated by FACEBOOK AI Researchers.
- [mmcv](https://github.com/open-mmlab/mmcv) is built by OpenMMLab team.  

## _BACKBONE_EXTRACT_FEATURE_

### _AlexNET_

### _VGG_

### _RESNET*_

### _RESNEXT_

### _DENSNET_

### _GOOOGLENET_

### _

## _NECKBONE_


## _HEADDEAD_PREDICTION_ 
