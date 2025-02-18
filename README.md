
# VAID_dataset

## Introduction

VAID(Vehicle Aerial Imaging from Drone) dataset contains 6000 aerial images under different illumination conditions, viewing angles from different places in Taiwan.The images are taken with the resolution of 1137 * 640 pixels in JPG format. Our VAID fataset contains seven classes of Vehicles, namely 'sedan' , 'minibus' , 'truck' , 'pickup truck' , 'bus' , 'cement truck' , ' trailer'.  
From left to right in the figure below are labels 'sedan' , 'minibus' , 'truck' , 'pickup truck' , 'bus' , 'cement truck' , ' trailer'
![image](https://github.com/KaiChun-RVL/VAID_dataset/blob/master/images/class.PNG)
You can download VAID dataset in this website.https://vision.ee.ccu.edu.tw/aerialimage/




## Test model

We test VAID dataset on 5 common model including Faster R-CNN, Yolov4, MobileNetv3 , RefineDet and U-Net.


### How to use 
 
#### Faster R-CNN
environment : tensorflow1.4 cuda9.2
1. Download the file https://drive.google.com/drive/folders/1S35gyY4c2B6HGzgB8WRl_scDYWdukhTb?usp=sharing
2. Put for_download/faster rcnn/data and for_download/faster rcnn/output into VAID_dataset/tf-faster-rcnn
3. Download dataset and put the fold Annotations amd JPEGImages into VAID_dataset/tf-faster-rcnn/data/VOCdevkit2007/VOC2007
4. make at VAID_dataset/tf-faster-rcnn/lib and VAID_dataset/tf-faster-rcnn/data/coco/PythonAPI

command :<br>
demo<br>
GPU_ID=0<br>
CUDA_VISIBLE_DEVICES=${GPU_ID} ./tools/demo.py --net res101 --dataset pascal_voc<br>

train<br>
./experiments/scripts/train_faster_rcnn.sh 0 pascal_voc res101

test<br>
./experiments/scripts/test_faster_rcnn.sh 0 pascal_voc res101

#### Yolov4
environment : cuda10.0 , cudnn>7.0 , opencv>2.4
1. Download the file https://drive.google.com/drive/folders/1S35gyY4c2B6HGzgB8WRl_scDYWdukhTb?usp=sharing
2. Put the folders for_download/yolov4/3rdparty , for_download/yolov4/backup , for_download/yolov4/cfd , for_download/yolov4/data , for_download/yolov4/include and for_download/yolov4/src into VAID_dataset/Yolov4/darknet
3. make in VAID_dataset/Yolov4/darknet
4. ./darknet if you succeed to make ,you will see usage: ./darknet <function>
5. put for_download/yolov4/yolov4.conv.137 into VAID_dataset/Yolov4/darknet
6.Download dataset and put the fold Annotations amd JPEGImages into VAID_dataset-master/Yolov4/darknet/VOCdevkit VOC2007 and VAID_dataset-master/Yolov4/darknet/VOCdevkit VOC2007_test

command:<br>
train <br>
./darknet detector train cfg/voc.data cfg/yolo-obj.cfg yolov4.conv.137
calculate<br> map <br>
./darknet detector map cfg/voc.data cfg/yolo-obj.cfg backup/yolo-obj_best.weights <br>
test <br>
./darknet detector test cfg/voc.data cfg/yolo-obj.cfg backup/yolo-obj_best.weights<br>
If you want to know more command , you can see the official yolo github.
#### Mobilenetv3
environment : pytorch 1.4.0 cuda9.2
Download dataset and put the fold Annotations amd JPEGImages into VAID_dataset-master/MobileNetV3-SSD-Compact-Version/VAID
run create_data_lists.py

command <br>
python train.py<br>
python eval.py
#### RefineDet
environment : cuda9.2 , pytorch 1.4.0
1. modify home path in VAID_dataset-master/RefineDet.PyTorch-master/data/config.py
2. modify VOC_ROOT path in VAID_dataset-master/RefineDet.PyTorch-master/data/voc0712.py
3. Download dataset and put the fold Annotations amd JPEGImages into VAID_dataset-master/RefineDet.PyTorch-master/data/VAID
4. Download the file https://drive.google.com/drive/folders/1S35gyY4c2B6HGzgB8WRl_scDYWdukhTb?usp=sharing
5. put for_download/Refinedet/weights into VAID_dataset-master/RefineDet.PyTorch-master

command:<br>
train <br>
./train_refinedet320.sh <br>
calculate map <br>
./eval_refinedet.sh 
#### U-Net
environment : cuda 10.0 , Keras 2.2.4

1.Download the file https://drive.google.com/drive/folders/1S35gyY4c2B6HGzgB8WRl_scDYWdukhTb?usp=sharing
2.Put for_download/U-Net/data and for_download/U-Net/model into VAID_dataset/U-Net/ ; put for_download/U-Net/results into VAID_dataset/U-Net/MAP/ ; put for_download/U-Net/detection-results into VAID_dataset/U-Net/MAP/car/ 

3.Train(unet+_residual_vgg16.py)
(1)modify 'path' to VAID_dataset/U-Net/data/train_val(seperate)/
(2)modify the model name you want to save in 'model_checkpoint'

4.Test(test.py)
(1)modify 'test_path' to VAID_dataset/U-Net/data/test/test_jpg/
(2)modify 'label_save_dir' to VAID_dataset/U-Net/data/predict/predict_label/
(3)modify 'visualize_save_dir' to VAID_dataset/U-Net/data/predict/predict_visualize/
(4)modify 'modelFile' to model file(model_name.hdf5) in 'model' folder

5.IOU(evaluate_iou.py)
(1)modify 'test_label_path' to VAID_dataset/U-Net/data/test/test_label/
(2)modify 'predict_path' to VAID_dataset/U-Net/data/predict/predict_label/

6.mAP(main_map.py)
### Source
The code are from the following website. <br>
Faster R-CNN : https://github.com/endernewton/tf-faster-rcnn <br>
Yolov4 : https://github.com/AlexeyAB/darknet<br>
Mobilenet : https://github.com/shaoshengsong/MobileNetV3-SSD-Compact-Version <br>
RefineDet : https://github.com/luuuyi/RefineDet.PyTorch <br>
