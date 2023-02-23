# Supervised_Learning-ANNOTATION

## _ANNOTATION for 2D IMAGE_
### 1. Annotation tools. 

**A. Object detection**

*a. One-stage (YOLO family, SSD-Net, FCOS,etc.)*

*b. Two-stage (R-CNN family.etc)*

=> Case 1: You will annotation the boxs that contain the objects we want to recognize. The [LableImg](https://github.com/heartexlabs/labelImg) tool is chosen for this task.
=> Case 2: You want to lable the oriented bounding box. The [roLabelImg](https://github.com/cgvict/roLabelImg) tool is used for this purpose.

**B. Instance segmentation**

*a. One-stage (YOLACT, SOLOv1-2, BlendMask, CenterMask, CondInst, BoxInst-Based FCOS, etc.)*

*b. Two-stage (Mask-RCNN, Rotated Mask-RCNN, MaskLab,etc.)*

=> For this task, you use this [Labelme](https://github.com/zhong110020/labelme) tool to annotate polygon of object.

**_After that:_**

**+ We should convert to standard format of the deep learning model.**

**+ Go to the _CONVERT-FORAMT_ to select one convertion method.**

### 2.Online annotation using Roboflow.

=> Following this [link](https://docs.roboflow.com/) to implement by yourself.

## _ANNOTATION for 3D POINT CLOUD_
```
1. install Mesh_Labeler-main.zip

2. 3D_segmentation_annotation.

3. You should prepare dataset that is separated and save each part into a folder.

* First, run B1.py: create new enviroment.

-To run this code, you should install librarys:
- pip install open3d-python (version --0.7.00)
- pip install plyfile
- (1) You should fix something about  input and output folder direction to match your folder
- (2) Eg: run code "python B1.py -i /home/airlab/Desktop/Annotation3D/DATACUTTING/ -o /home/airlab/Desktop/Annotation3D/DATA/"
- After you select object for train and test. And save it into two folder named: "DATATRAIN and DATATEST".

* Then run B2.py: create new enviroment.

- Intruction: create new enviroment 
- (1) Install: 
 -  pip install open3d=0.13.0.0
 -  pip install plyfile
 -  add d3 folder
- (2) you should fix something about direction
    * Eg: run code: "python B2.py -i /home/airlab/Desktop/Annotation3D/DATATRAIN" and "python B2.py -i /home/airlab/Desktop/Annotation3D/DATATEST".
* Library is to process 3D point cloud:
- open3d
- plyfile
- trimesh
- pyVista
- openGL
- PCL with C++
This project is a work in progress.
```
# Supervised_Learning-BUILD MODEL DL


