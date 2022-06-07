# 安装常用工具

## 编译工具
1. CMake
    ```bash
    wget https://github.com/Kitware/CMake/releases/download/v3.22.5/cmake-3.22.5-linux-x86_64.tar.gz 
    sudo tar -zxvf cmake-3.22.5-linux-x86_64.tar.gz -C /opt
    sudo mv cmake-3.22.5-linux-x86_64/ cmake/
    cd /opt/cmake/bin
    sudo ln -s /opt/cmake/bin/cmake /usr/bin/cmake
    ```
2. miniconda
    ```bash
    wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
    sudo bash Miniconda3-latest-Linux-x86_64.sh
    eval "$(/opt/miniconda3/bin/conda shell.YOUR_SHELL_NAME hook)" 
    conda init
   
   # 如果不需要在启动时自动激活 conda base 环境
   conda config --set auto_activate_base false
   
   # 升级 conda
   conda update -n base -c defaults conda
    ```
3. python
    ```bash
   # 首先先安装 miniconda 环境
   conda create --name py310 python=3.10
   conda activate py310
   
   conda info -e  # 查看当前所有的可用环境
   conda install numpy
   conda install pandas
   conda install jupyter
    ```
4. 常见开发工具
   ```bash
   yum install tcl-devel
   ```