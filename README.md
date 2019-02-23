#### A psuedo-random set of notes that might help

##### Useful references

https://github.com/opencv/opencv/wiki/TensorFlow-Object-Detection-API
https://github.com/opencv/opencv_extra/tree/master/testdata/dnn

##### Installation on Linux: (Mask RCNN example) 

```sh
$ wget http://download.tensorflow.org/models/object_detection/mask_rcnn_inception_v2_coco_2018_01_28.tar.gz
$ tar zxvf mask_rcnn_inception_v2_coco_2018_01_28.tar.gz
```

##### Install on MacOS: (Mask RCNN example)

```sh
$ curl -O http://download.tensorflow.org/models/object_detection/mask_rcnn_inception_v2_coco_2018_01_28.tar.gz
$ tar zxvf mask_rcnn_inception_v2_coco_2018_01_28.tar.gz
```

##### OpenCV installation:

Install 4.0.0 - versions before 3.4.3 will throw CNN model exceptions given there was no cv.dnn functionality

```sh
$ pip install opencv-python
```

If you are running without the need or access to an X server, there is the (lighter-weight) headless python package which can be installed:

```sh
$ pip install opencv-python-headless
```

##### Model weights and graphs:

I have omitted the model weight files given they are huge and invariably exceed the GitHub repo limit.

Please take a look at the top of recog_argparse.py for the names of the relevant files to search for - some should be obtainable from the OpenCV DNN 'model zoo' page on GitHub.

TODO : add links here to the necessary files for SSD Mobilenet v1 & v2, YOLO v3 and Faster-RCNN models


##### TF graph creation:

The pbtxt file for the associated CNN model architecture should be on the tf or opencv GitHub - see Useful References above - but, if not, can be generated thus:

```sh
$ python tf_text_graph_faster_rcnn.py --input /path/to/model.pb --config /path/to/example.config --output /path/to/graph.pbtxt
```

Example:

```sh
$ python tf_text_graph_ssd.py --input ./ssd_mobilenet_v2_coco_2018_03_29/frozen_inference_graph.pb --config ./ssd_mobilenet_v2_coco.config --output ./ssd_mobilenet_v2_coco_2019_01_28.pbtxt
```

##### Usage examples:

```sh
$ python3 recog.py --stream='http://192.168.0.1/video.cgi' --classes='./models/yolo3/yolo3.classes' --weights='./models/yolo3/yolo3.weights' --model='./models/yolo3/yolo3.cfg' 
$ python3 recog.py --video=people.mpg  --classes='<path>'  --weights='<path>'  --model='<path>'
$ python3 recog.py                     --classes='<path>'  --weights='<path>'  --model='<path>'
(uses your local webcam as video source)
```

##### Licence-free video clips for testing and paramter-tuning:

https://videos.pexels.com/videos/time-lapse-video-of-runners-855789


##### Headless OpenCV install on AWS Linux:

```sh
$ sudo yum update
$ sudo yum install git cmake gcc-c++ cmake3
$ git clone https://github.com/Itseez/opencv.git
$ cd opencv
$ mkdir ./build
$ git checkout
$ cd ./build
$ cmake3 ../
$ sudo yum install numpy python-devel pip
$ sudo pip install opencv-python
$ pip install opencv-python-headless --user
$ pip install supervisor
```

(see http://supervisord.org/introduction.html)


##### MPEG4 motion vector rendering:

```sh
$ ffplay -flags2 +export_mvs runners.mp4 -vf codecview=mv=pf+bf+bb
$ ffmpeg -flags2 +export_mvs -i input.mp4 -vf codecview=mv=pf+bf+bb output.mp4
```