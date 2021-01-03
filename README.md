# tf-pose-realtime3D
这个项目集成了tf-pose-estimation实现了3D人体姿态实时识别功能
**注意：所有安装的模块都是在python的虚拟环境中安装
一、openpose 安装部分
创建虚拟环境：conda create -n tf1 python=3.5
激活虚拟环境：conda activate tf1
## 以下安装模块部分速度较慢情况请更改pip或conda下载源
安装tensorflow：conda install tensorflow-gpu==1.4.0
安装opencv：pip install opencv-python==3.4.2.17
安装opencv-contrib：pip install opencv-contrib-python=3.4.2.17

二、安装git 克隆github上的代码仓库

三、配置编译器swig 设置环境变量 此电脑--属性--高级系统设置--环境变量--系统变量--path（输入swig的地址）
使用cmd中输入swig --help测试是否安装成功

四、安装pycocotools 进入pycocotools文件夹 cmd进入pythonAPI文件夹中
输入以下命令 python setup.py build_ext --inplace 
python setup.py build_ext install
运行过程中fatal error C1083: Cannot open source file: 'pycocotools/_mask.c':这个问题是因为
没有安装Cython模块

五、进入tf-pose-estimation-master文件夹根目录，pip install -r requirements.txt
安装 conda install protobuf
出现的错误AttributeError: module 'google.protobuf.descriptor_pool' has no attribute 'Default'
尝试将protobuf卸载后重新安装即可

六、编译cmd进行tf-pose-estimation-master\tf_pose\pafprocess文件夹根目录
cmd输入：swig -python -c++ pafprocess.i && python setup.py build_ext --inplace
python setup.py install
已完成代码生成

七、运行代码请在项目根目录执行否则会报错误：AttributeError: 'TfPoseEstimator' object has no attribute 'persistent_sess' 
python src/run.py 
python src/run_webcam.py
添加后缀参数 --image= 或 --model=
若出现报错No module named‘tensorflow。contrib.tensorrt’将tf-pose-estimation-master\tf_pose
中estimator.py中的导入tensorrt的地方注释即可

err ==cudaSuccess|| err == cudaErrorInvalidValue Unexpected CUDA error：invalid arugemet
需要去对应报错文件加入以下一句话
import os
os.environ['CUDA_VISIBILE_DEVICES'] = '-1'

PyQt展示部分 
进入虚拟环境 conda activate tf1
进入pyqtgraph-master根目录 python setup.py install
安装pyqt5 pip install pyqt5
安装pyopengl  conda install -c anaconda pyopengl (后面运行时候出现raise source.error("unknown flag", len(char)) sre_constants.error: unknown flag)
重新卸载安装即可

之后重新运行python src/realtime.py 即可

