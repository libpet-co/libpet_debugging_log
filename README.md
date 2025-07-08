# autoware 调试日志，从零开始
硬件 S210H 19-10980HK 
## step1: 准备工作
在新的 ubuntu 22.04 更新、升级、安装必要软件

1）系统软件更新的升级
```
sudo apt update
sudo apt upgrade
```
上述指令没有VPN的或者其它原因可能会失败，可以安装VPN后再尝试运行

2）安装vpn 

3）换源
```
wget http://fishros.com/install -O fishros && . fishros
```
4） 安装中文输入法，取决于自己喜好，这里安装google pinyin
https://cloud.tencent.com/developer/article/2417968

5）安装vscode, ros2 humble
```
wget http://fishros.com/install -O fishros && . fishros
```
## step2: 安装autoware v1.0 环境，

一定要注意版本选择 release-v1.0_beta ，按照下面的步骤进行操作
```
https://autowarefoundation.github.io/autoware-documentation/release-v1.0_beta/installation/autoware/source-installation/
```

注意事项1：不安装nvidia 库

![alt text](<docs/Screenshot from 2025-07-08 10-56-01.png>)

注意事项2：下载artifacts 选择yes
![alt text](<docs/Screenshot from 2025-07-08 10-56-09.png>)

注意事项3：遇到onnx下载相关错误 解决方法：注释掉下面文件28行以后的代码，这些是感知模块用的，暂时不调试感知，所以可以注释
![alt text](<docs/Screenshot from 2025-07-08 11-04-43.png>)
![alt text](<docs/Screenshot from 2025-07-08 11-06-06.png>)

注意事项34：rosdep init 和 rosdep update 有时会遇到问，我这里没有问题，直接过，可能和网络有关，如果遇到问题，请自行查找解决方案。
![alt text](<docs/Screenshot from 2025-07-08 11-22-20.png>)