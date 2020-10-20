# VM에 Tensorflow 설치하기

## 1. Python 개발 환경 설치

```cmd
$ python3 --version
$ pip3 --version
```

- python 환경이 이미 구성되었는지 확인
- 패키지가 설치되지 않았다면 `python`, `pip 패키지 관리자`, `venv` 설치

```linux
$sudo apt update
$sudo apt install python3-dev python3-pip python3-venv
```

> 주의  :
>
> 가상환경이 아니라면 아래 명령어에 ` python3 -m pip `사용
>
> 시스템 pip 대신 Python pip를 업그레이드 하여서 사용할 수 있다.



## 2. 가상 환경 만들기 (권장)

```cmd
$ python3 -m venv --system-site-packages ./venv/
$ cd venv 
$ source bin/activate #가상환경 활성화
```

```cmd
(venv) $ pip install --upgrade pip
(venv) $ deactivate #가상환경 종료 
```



## 3. TensorFlow pip 패키지 설치

#### 1) 가상 환경 설치

```cmd
(venv) $ pip install --upgrade tensorflow
```



#### 2) 시스템 설치

```cmd
(venv) $ pip3 install --user --upgrade tensorflow 
```



#### 3) 설치 확인

```cmd
$ python3 -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])))"

```



## 4. GPU 지원 TensorFlow 

#### 1) pip 패키지

```cmd
$ pip install tensorflow
```



> 이전 버전의 TensorFlow
>
> ```cmd
> $ pip install tensorflow==1.15 #CPU
> $ pip install tensorflow-gpu==1.15 #GPU
> ```



#### 2)  소프트웨어 요구사항

- apt 명령어를 사용해 가장 간편하게 Ubuntu에 필수 NVDIA 소프트웨어를 설치 할 수 있다.

```cmd
$ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/extras/CUPTI/lib64
```



- apt를 사용하여 CUDA 설치

> Ubuntu 18.04 

```cmd
# Add NVIDIA package repositories
$ wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-$ $ repo-ubuntu1804_10.1.243-1_amd64.deb
$ sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
$ sudo dpkg -i cuda-repo-ubuntu1804_10.1.243-1_amd64.deb
$ sudo apt-get update
$ wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb
$ sudo apt install ./nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb
$ sudo apt-get update

# Install NVIDIA driver
$ sudo apt-get install --no-install-recommends nvidia-driver-450
# Reboot. Check that GPUs are visible using the command: nvidia-smi

# Install development and runtime libraries (~4GB)
$ sudo apt-get install --no-install-recommends \
    cuda-10-1 \
    libcudnn7=7.6.5.32-1+cuda10.1  \
    libcudnn7-dev=7.6.5.32-1+cuda10.1


# Install TensorRT. Requires that libcudnn7 is installed above.
$ sudo apt-get install -y --no-install-recommends libnvinfer6=6.0.1-1+cuda10.1 \
    libnvinfer-dev=6.0.1-1+cuda10.1 \
    libnvinfer-plugin6=6.0.1-1+cuda10.1
```



#### 3) 몇 가지 설치 메커니즘을 사용하려면 TensorFlow Python 패키지의 URL이 필요

- python 3.8 GPU 지원 

```cmd
$ pip install https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-2.3.0-cp38-cp38-manylinux2010_x86_64.whl
```

- python 3.8 CPU 지원

```cmd
$ pip install https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow_cpu-2.3.0-cp38-cp38-manylinux2010_x86_64.whl
```

