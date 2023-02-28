# SUPERVISED LEARNING-[LECTURE](https://cs.nyu.edu/~yann/talks/lecun-ranzato-icml2013.pdf)

# SUPERVISED LEARNING-ANNOTATION

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

**+ Go to the _CONVERT-FORMAT_ to select one convertion method.**

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

# SUPERVISED LEARNING-BUILD MODEL DL

## _FRAMEWORK for DEEP LEARNING_

- There are many framework used for developming DL such as [Tensorflow](https://www.tensorflow.org/tutorials/quickstart/beginner), [Pytorch](https://pytorch.org/tutorials/beginner/pytorch_with_examples.html), [Caffe](https://recodeminds.com/blog/a-beginners-guide-to-caffe-for-deep-learning/), [ONNX](https://onnx.ai/),Keras, etc.
- TensorFlow and Pytorch are well-know in Deep Leaning model.
- TensorFlow for academia.
- Pytorch for developming applicatioon.
- ONNX for real-time model.   

## _PLATFORM for DEEP LEARNING_

- [Detectron2](https://detectron2.readthedocs.io/en/latest/tutorials/index.html) is generated by FACEBOOK AI Researchers.
- [mmcv](https://github.com/open-mmlab/mmcv) is built by OpenMMLab team (specificial computer vision).  
- [mmDet](https://github.com/open-mmlab/mmdetection) is an open source object detection toolbox based on PyTorch and is built by OpenMMlab team.
- etc.

## _[FEATURE_EXTRACTION_BACKBONE-MODEL](https://github.com/AIALab-TeamAI/Supervised_Learning/blob/main/PAPER/backbone.pdf)_

### _AlexNET MODEL_

![pic5](https://github.com/AIALab-TeamAI/Supervised_Learning/blob/main/src_img/AlexNet.png)

#### Example:

```
import torch.nn as nn

class AlexNet(nn.Module):

    def __init__(self, num_classes=1000):
        super(AlexNet, self).__init__()
        
        self.features = nn.Sequential(
            nn.Conv2d(3, 64, kernel_size=11, stride=4, padding=2),
            nn.ReLU(inplace=True),
            nn.MaxPool2d(kernel_size=3, stride=2),
            nn.Conv2d(64, 192, kernel_size=5, padding=2),
            nn.ReLU(inplace=True),
            nn.MaxPool2d(kernel_size=3, stride=2),
            nn.Conv2d(192, 384, kernel_size=3, padding=1),
            nn.ReLU(inplace=True),
            nn.Conv2d(384, 256, kernel_size=3, padding=1),
            nn.ReLU(inplace=True),
            nn.Conv2d(256, 256, kernel_size=3, padding=1),
            nn.ReLU(inplace=True),
            nn.MaxPool2d(kernel_size=3, stride=2),
        )
        
        self.avgpool = nn.AdaptiveAvgPool2d((6, 6))
        
        self.classifier = nn.Sequential(
            nn.Dropout(),
            nn.Linear(256 * 6 * 6, 4096),
            nn.ReLU(inplace=True),
            nn.Dropout(),
            nn.Linear(4096, 4096),
            nn.ReLU(inplace=True),
            nn.Linear(4096, num_classes),
        )

    def forward(self, x):
        x = self.features(x)
        x = self.avgpool(x)
        x = torch.flatten(x, 1)
        x = self.classifier(x)
        return x
```
### _VGGs_

![pic6](https://github.com/AIALab-TeamAI/Supervised_Learning/blob/main/src_img/VGGs.png)

#### Example:

```
import torch.nn as nn

cfg = {
    'VGG11': [64, 'M', 128, 'M', 256, 256, 'M', 512, 512, 'M', 512, 512, 'M'],
    'VGG13': [64, 64, 'M', 128, 128, 'M', 256, 256, 'M', 512, 512, 'M', 512, 512, 'M'],
    'VGG16': [64, 64, 'M', 128, 128, 'M', 256, 256, 256, 'M', 512, 512, 512, 'M', 512, 512, 512, 'M'],
    'VGG19': [64, 64, 'M', 128, 128, 'M', 256, 256, 256, 256, 'M', 512, 512, 512, 512, 'M', 512, 512, 512, 512, 'M']
}

class VGG(nn.Module):
    
    def __init__(self, vgg_name):
        super(VGG, self).__init__()
        self.features = self._make_layers(cfg[vgg_name])
        self.avgpool = nn.AdaptiveAvgPool2d((7, 7))
        self.classifier = nn.Sequential(
            nn.Linear(512 * 7 * 7, 4096),
            nn.ReLU(True),
            nn.Dropout(),
            nn.Linear(4096, 4096),
            nn.ReLU(True),
            nn.Dropout(),
            nn.Linear(4096, 1000),
        )

    def forward(self, x):
        x = self.features(x)
        x = self.avgpool(x)
        x = x.view(x.size(0), -1)
        x = self.classifier(x)
        return x
    
    def _make_layers(self, cfg):
        layers = []
        in_channels = 3
        for x in cfg:
            if x == 'M':
                layers += [nn.MaxPool2d(kernel_size=2, stride=2)]
            else:
                layers += [nn.Conv2d(in_channels, x, kernel_size=3, padding=1),
                           nn.BatchNorm2d(x),
                           nn.ReLU(inplace=True)]
                in_channels = x
        layers += [nn.AvgPool2d(kernel_size=1, stride=1)]
        return nn.Sequential(*layers)
 ```

### _RESNETs_

![pic7](https://github.com/AIALab-TeamAI/Supervised_Learning/blob/main/src_img/ResNet_VGGs.png)

#### Exmaple:

```
'''
ResNet in PyTorch.
For Pre-activation ResNet, see 'preact_resnet.py'.
Reference:
[1] Kaiming He, Xiangyu Zhang, Shaoqing Ren, Jian Sun
    Deep Residual Learning for Image Recognition. arXiv:1512.03385
'''
import torch
import torch.nn as nn
import torch.nn.functional as F

class BasicBlock(nn.Module):
    expansion = 1

    def __init__(self, in_planes, planes, stride=1):
        super(BasicBlock, self).__init__()
        self.conv1 = nn.Conv2d(
            in_planes, planes, kernel_size=3, stride=stride, padding=1, bias=False)
        self.bn1 = nn.BatchNorm2d(planes)
        self.conv2 = nn.Conv2d(planes, planes, kernel_size=3,
                               stride=1, padding=1, bias=False)
        self.bn2 = nn.BatchNorm2d(planes)

        self.shortcut = nn.Sequential()
        if stride != 1 or in_planes != self.expansion*planes:
            self.shortcut = nn.Sequential(
                nn.Conv2d(in_planes, self.expansion*planes,
                          kernel_size=1, stride=stride, bias=False),
                nn.BatchNorm2d(self.expansion*planes)
            )

    def forward(self, x):
        out = F.relu(self.bn1(self.conv1(x)))
        out = self.bn2(self.conv2(out))
        out += self.shortcut(x)
        out = F.relu(out)
        return out
class Bottleneck(nn.Module):
    expansion = 4

    def __init__(self, in_planes, planes, stride=1):
        super(Bottleneck, self).__init__()
        self.conv1 = nn.Conv2d(in_planes, planes, kernel_size=1, bias=False)
        self.bn1 = nn.BatchNorm2d(planes)
        self.conv2 = nn.Conv2d(planes, planes, kernel_size=3,
                               stride=stride, padding=1, bias=False)
        self.bn2 = nn.BatchNorm2d(planes)
        self.conv3 = nn.Conv2d(planes, self.expansion *
                               planes, kernel_size=1, bias=False)
        self.bn3 = nn.BatchNorm2d(self.expansion*planes)

        self.shortcut = nn.Sequential()
        if stride != 1 or in_planes != self.expansion*planes:
            self.shortcut = nn.Sequential(
                nn.Conv2d(in_planes, self.expansion*planes,
                          kernel_size=1, stride=stride, bias=False),
                nn.BatchNorm2d(self.expansion*planes)
            )

    def forward(self, x):
        out = F.relu(self.bn1(self.conv1(x)))
        out = F.relu(self.bn2(self.conv2(out)))
        out = self.bn3(self.conv3(out))
        out += self.shortcut(x)
        out = F.relu(out)
        return out


class ResNet(nn.Module):
    def __init__(self, block, num_blocks, num_classes=10):
        super(ResNet, self).__init__()
        self.in_planes = 64

        self.conv1 = nn.Conv2d(3, 64, kernel_size=3,
                               stride=1, padding=1, bias=False)
        self.bn1 = nn.BatchNorm2d(64)
        self.layer1 = self._make_layer(block, 64, num_blocks[0], stride=1)
        self.layer2 = self._make_layer(block, 128, num_blocks[1], stride=2)
        self.layer3 = self._make_layer(block, 256, num_blocks[2], stride=2)
        self.layer4 = self._make_layer(block, 512, num_blocks[3], stride=2)
        self.linear = nn.Linear(512*block.expansion, num_classes)

    def _make_layer(self, block, planes, num_blocks, stride):
        strides = [stride] + [1]*(num_blocks-1)
        layers = []
        for stride in strides:
            layers.append(block(self.in_planes, planes, stride))
            self.in_planes = planes * block.expansion
        return nn.Sequential(*layers)

    def forward(self, x):
        out = F.relu(self.bn1(self.conv1(x)))
        out = self.layer1(out)
        out = self.layer2(out)
        out = self.layer3(out)
        out = self.layer4(out)
        out = F.avg_pool2d(out, 4)
        out = out.view(out.size(0), -1)
        out = self.linear(out)
        return out

def ResNet18():
    return ResNet(BasicBlock, [2, 2, 2, 2])


def ResNet34():
    return ResNet(BasicBlock, [3, 4, 6, 3])


def ResNet50():
    return ResNet(Bottleneck, [3, 4, 6, 3])


def ResNet101():
    return ResNet(Bottleneck, [3, 4, 23, 3])


def ResNet152():
    return ResNet(Bottleneck, [3, 8, 36, 3])


def test():
    net = ResNet18()
    y = net(torch.randn(1, 3, 32, 32))
    print(y.size())
```

## [_NECKBONE MODEL_]()

### _[BOTOOM-UP](https://github.com/airsplay/py-bottom-up-attention)_

### _[TOP-DOWN](https://github.com/mks0601/3DMPPE_ROOTNET_RELEASE)_

## _HEADEAD PREDICTION_ 
