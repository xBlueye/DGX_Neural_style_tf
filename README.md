# DGX_Neural_style_tf

Installing and using https://github.com/cysmith/neural-style-tf

# Step 1) Tensorflow & opencv 
pip install tensorflow-gpu (1.14 for me)

sudo apt install build-essential cmake git pkg-config libgtk-3-dev \
libavcodec-dev libavformat-dev libswscale-dev libv4l-dev \
libxvidcore-dev libx264-dev libjpeg-dev libpng-dev libtiff-dev \
gfortran openexr libatlas-base-dev python3-dev python3-numpy \
libtbb2 libtbb-dev libdc1394-22-dev libopenexr-dev \
libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev

mkdir ~/opencv_build && cd ~/opencv_build
git clone https://github.com/opencv/opencv.git

git clone https://github.com/opencv/opencv_contrib.git

cd ~/opencv_build/opencv
mkdir -p build && cd build

cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D INSTALL_C_EXAMPLES=ON \
-D INSTALL_PYTHON_EXAMPLES=ON \
-D OPENCV_GENERATE_PKGCONFIG=ON \
-D OPENCV_EXTRA_MODULES_PATH=~/opencv_build/opencv_contrib/modules \
-D BUILD_EXAMPLES=ON ..

make j8

sudo make install

# Step 2) CUDA & CuDNN

wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin
sudo mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/11.6.2/local_installers/cuda-repo-ubuntu1804-11-6-local_11.6.2-510.47.03-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1804-11-6-local_11.6.2-510.47.03-1_amd64.deb
sudo apt-key add /var/cuda-repo-ubuntu1804-11-6-local/7fa2af80.pub
sudo apt-get update
sudo apt-get -y install cuda

https://developer.nvidia.com/compute/cudnn/secure/8.4.0/local_installers/11.6/cudnn-local-repo-ubuntu1804-8.4.0.27_1.0-1_amd64.deb (You have to login on NVIDIA and sign up as a developer to download)
sudo dpkg -i cudnn-local-repo-ubuntu1804-8.4.0.27_1.0-1_amd64.deb
sudo apt-key add /var/cudnn-local-repo-*/7fa2af80.pub
sudo apt-get update
sudo apt-get install libcudnn8=8.4.0.27_1.0-1+cudaX.Y
sudo apt-get install libcudnn8-dev=8.4.0.27_1.0-1+cudaX.Y
sudo apt-get install libcudnn8-samples=8.4.0.27_1.0-1+cudaX.Y

# Step 3) weights
download VGG-19 model weights from http://www.vlfeat.org/matconvnet/pretrained/ and place the file in the project directory

# Step 4) run the project
  for images :
    basic usage
    bash stylize_image.sh <path_to_content_image> <path_to_style_image>
    advanced usage
    python neural_style.py --content_img <...> --style_imgs <...> <arguments>
  for videos :
    bash stylize_video.sh <path_to_video> <path_to_style_image>
    python neural_style.py --video --video_input_dir <...> --style_imgs <...> <arguments>
# Arguments 
  https://github.com/cysmith/neural-style-tf#arguments
# Optimization Arguments
  https://github.com/cysmith/neural-style-tf#optimization-arguments
# Video Result
https://www.youtube.com/watch?v=DbHJRLw4cOo
This file was to big for github.
