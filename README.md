# ReMOT

> **Rethinking Two-Stage Data Association for Multiple Object Tracking in Crowd Scenes**
> 
> Ruonan Wei, Yuehuan Wang, and Jinpu Zhang

## Visualization on MOT challenge test set
https://github.com/HUST-IAL/ReMOT/blob/main/visualization/MOT17-03-DPM_batch.mp4

https://github.com/HUST-IAL/ReMOT/blob/main/visualization/MOT17-14-DPM_batch.mp4

https://github.com/HUST-IAL/ReMOT/blob/main/visualization/MOT20-04_batch.mp4

https://github.com/HUST-IAL/ReMOT/blob/main/visualization/MOT20-06_batch.mp4

https://github.com/HUST-IAL/ReMOT/blob/main/visualization/MOT20-08_batch.mp4

## Installation
 
### Setup with Anaconda

**Step 1.** Install torch and matched torchvision from [pytorch.org](https://pytorch.org/get-started/locally/).<br>
The code was tested using torch 1.11.0+cu113 and torchvision==0.12.0 

**Step 2.** Install ReMOT.
```shell
cd ReMOT
pip3 install -r requirements.txt
python3 setup.py develop
```
**Step 3.** Install [pycocotools](https://github.com/cocodataset/cocoapi).
```shell
pip3 install cython; pip3 install 'git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI'
```

Step 4. Others
```shell
# Cython-bbox
pip3 install cython_bbox

# faiss cpu / gpu
pip3 install faiss-cpu
pip3 install faiss-gpu
```

## Data Preparation

Download [MOT17](https://motchallenge.net/data/MOT17/) and [MOT20](https://motchallenge.net/data/MOT20/) from the [official website](https://motchallenge.net/). And put them in the following structure:

```
<dataets_dir>
      │
      ├── MOT17
      │      ├── train
      │      └── test    
      │
      └── MOT20
             ├── train
             └── test
```

## Tracking

Tuning the tracking parameters carefully could lead to higher performance.

* **Test on MOT17**

```shell
cd <ReMOT_dir>
python3 tools/track.py <dataets_dir/MOT17> --default-parameters --with-reid --benchmark "MOT17" --eval "test" --fp16 --fuse
python3 tools/interpolation.py --txt_path <path_to_track_result>
```

* **Test on MOT20**

```shell
cd <ReMOT_dir>
python3 tools/track.py <dataets_dir/MOT20> --default-parameters --with-reid --benchmark "MOT20" --eval "test" --fp16 --fuse
python3 tools/interpolation.py --txt_path <path_to_track_result>
```

* **Evaluation on MOT17 validation set (the second half of the train set)**

```shell
cd <ReMOT_dir>
python3 tools/track.py <dataets_dir/MOT17> --default-parameters --benchmark "MOT17" --eval "val" --fp16 --fuse
# or
python3 tools/track.py <dataets_dir/MOT17> --default-parameters --with-reid --benchmark "MOT17" --eval "val" --fp16 --fuse
```

## Acknowledgement
This code is based on the implementation of [ByteTrack](https://github.com/ifzhang/ByteTrack), [BoT-SORT](https://github.com/NirAharon/BoT-SORT).
A lot of ideas and results are borrowed from 
[ByteTrack](https://github.com/ifzhang/ByteTrack), 
[BoT-SORT](https://github.com/NirAharon/BoT-SORT),
[StrongSORT](https://github.com/dyhBUPT/StrongSORT),
[FastReID](https://github.com/JDAI-CV/fast-reid),
[YOLOX](https://github.com/Megvii-BaseDetection/YOLOX) and
[YOLOv7](https://github.com/wongkinyiu/yolov7). 
Thanks for their excellent work!
## Contact
If you have any questions, please contact ruonan2765@gmail.com
