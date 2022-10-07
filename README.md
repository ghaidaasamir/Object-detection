# Complex YOLOv4 3d Object detection


The PyTorch Implementation based on YOLOv4 of the paper: [Complex-YOLO: Real-time 3D Object Detection on Point Clouds](https://arxiv.org/pdf/1803.06199.pdf)

---

## Installation

**Clone the project and install requirements**

```shell script
pip install -U -r requirements.txt
```

## Data Preparation
3D KITTI detection dataset  [here](http://www.cvlibs.net/datasets/kitti/eval_object.php?obj_benchmark=3d).

- Velodyne point clouds _**(29 GB)**_: input data to the Complex-YOLO model
- Training labels of object data set _**(5 MB)**_: input label to the Complex-YOLO model
- Camera calibration matrices of object data set _**(16 MB)**_: for visualization of predictions
- Left color images of object data set _**(12 GB)**_: for visualization of predictions

## How to run

```shell script
cd src/data_process
```


## Folder structure

```
${ROOT}
└── checkpoints/    
    ├── complex_yolov3/
    └── complex_yolov4/
└── src/
    ├── config/
    ├── cfg/
        │   ├── complex_yolov3.cfg
        │   ├── complex_yolov3_tiny.cfg
        │   ├── complex_yolov4.cfg
        │   ├── complex_yolov4_tiny.cfg
    │   ├── train_config.py
    │   └── kitti_config.py
    ├── data_process/
    │   ├── complex_yolov4_mse_loss.pth
    │   ├── kitti_bev_utils.py
    │   ├── kitti_dataloader.py
    │   ├── kitti_dataset.py
    │   ├── kitti_data_utils.py
    │   ├── train_val_split.py
    │   └── transformation.py
    ├── models/
    │   ├── darknet2pytorch.py
    │   ├── darknet_utils.py
    │   ├── model_utils.py
    │   ├── yolo_layer.py
    └── utils/
    │   ├── evaluation_utils.py
    │   ├── iou_utils.py
    │   ├── logger.py
    │   ├── misc.py
    │   ├── torch_utils.py
    │   ├── train_utils.py
    │   └── visualization_utils.py
    └── dataset/kitti/
        ├──ImageSets/
        │   ├── train.txt
        │   └── val.txt
        │   └── test.txt <-- list of names of test data
        ├── training/
        │   ├── image_2/ <-- for visualization
        │   ├── calib/
        │   ├── label_2/
        │   └── velodyne/
        └── testing/  
        │   ├── image_2/ <-- for visualization
        │   ├── calib/
        │   └── velodyne/ 
        └── classes_names.txt
    ├── test.py
    ├── test.sh
    ├── train.py
    └── train.sh
├── README.md 
└── requirements.txt
```

## Results

Data Format Description
=======================
The data for training can be found in the corresponding folders.
The sub-folders are structured as follows:

  - image_02/ contains the left color camera images (png)
  - label_02/ contains the left color camera label files (plain text files)
  - calib/ contains the calibration for all five cameras (plain text file)
  - velodyne/ contains the velodyne point cloud (bin)

The label files contain the following information, which can be read and
written using the matlab tools (readLabels.m, writeLabels.m) provided within
this devkit. All values (numerical or strings) are separated via spaces,
each row corresponds to one object. The 15 columns represent:

#Values    Name      Description
----------------------------------------------------------------------------
   1    type         Describes the type of object: 'Car', 'Van', 'Truck',
                     'Pedestrian', 'Person_sitting', 'Cyclist', 'Tram',
                     'Misc' or 'DontCare'
   1    truncated    Float from 0 (non-truncated) to 1 (truncated), where
                     truncated refers to the object leaving image boundaries
   1    occluded     Integer (0,1,2,3) indicating occlusion state:
                     0 = fully visible, 1 = partly occluded
                     2 = largely occluded, 3 = unknown
   1    alpha        Observation angle of object, ranging [-pi..pi]
   4    bbox         2D bounding box of object in the image (0-based index):
                     contains left, top, right, bottom pixel coordinates
   3    dimensions   3D object dimensions: height, width, length (in meters)
   3    location     3D object location x,y,z in camera coordinates (in meters)
   1    rotation_y   Rotation ry around Y-axis in camera coordinates [-pi..pi]





## Credit

- Complex-YOLO: https://arxiv.org/pdf/1803.06199.pdf
YoloV3 Implementation is borrowed from:
- https://github.com/eriklindernoren/PyTorch-YOLOv3
Point Cloud Preprocessing is based on:
- https://github.com/skyhehe123/VoxelNet-pytorch
- https://github.com/dongwoohhh/MV3D-Pytorch

