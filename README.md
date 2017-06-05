## Docker solution for face detection using Faster R-CNN

**dockerface** is a docker image solution for face detection in videos and images. It deploys a trained Faster R-CNN network on Caffe through an easy to use docker image. Bring your videos and images, run dockerface and obtain videos and images with bounding boxes of face detections and an easy to use face detection annotation text file.

The docker image is large for now because OpenCV has to be compiled and stored in the image to be able to use video and it takes up 7+ GB of space.

### Instructions

Install NVIDIA Cuda 8 and cudnn v5
```
https://developer.nvidia.com/cuda-downloads
https://developer.nvidia.com/cudnn
```

Install docker
```
https://docs.docker.com/engine/installation/
```

Install nvidia-docker
```
wget -P /tmp https://github.com/NVIDIA/nvidia-docker/releases/download/v1.0.1/nvidia-docker_1.0.1-1_amd64.deb
sudo dpkg -i /tmp/nvidia-docker*.deb && rm /tmp/nvidia-docker*.deb
```

Go to your working folder and create a directory called data, your videos and images should go here. Also create a folder called output.

```
cd $WORKING_DIR
mkdir data
mkdir output
```

Run the docker container
```
sudo nvidia-docker run -it -v $PWD/data:/opt/py-faster-rcnn/edata -v $PWD/output/video:/opt/py-faster-rcnn/output/video natanielruiz/dockerface:tag
```

Once inside the container use this command to process videos
```
python tools/run_face_detection_on_video.py --gpu 0 --video edata/YOUR_VIDEO_FILENAME --output_string STRING_TO_BE_APPENDED_TO_OUTPUTFILE_NAME
```

Voila, that easy!

*Nataniel Ruiz<br>
Georgia Institute of Technology*
