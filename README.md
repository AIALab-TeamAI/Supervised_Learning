# Supervised_Learning
# --------------------------------
## _ANNOTATION_##
### 1. Annotation tools for 2D image. 

**1A. Object detection**

*a. One-stage (YOLO family, SSD-Net, FCOS,etc.)*

*b. Two-stage (R-CNN family.etc)*
- Case 1: you will annotation the boxs that contain the objects we want to recognize. The [LableImg](https://github.com/heartexlabs/labelImg) tool is chosen for this task.
- Case 2: you want to lable the oriented bounding box. The [roLabelImg](https://github.com/cgvict/roLabelImg) tool is used for this purpose.

**1B. Instance segmentation**

*a. One-stage (YOLACT, SOLOv1-2, BlendMask, CenterMask, CondInst, BoxInst-Based FCOS, etc.)*

*b. Two-stage (Mask-RCNN, Rotated Mask-RCNN, MaskLab,etc.)

**_After that:_**
**+ We should convert to standard format of the deep learning model**
**+ Go to the _CONVERT-FORAMT_ to select one convertion method**


