## 华为Atlas200开发踩过的坑
### 1.Face-Detection
  #### 1.1 主要参考[华为的教程](https://github.com/Ascend/sample-facedetection)
  Deployment 选择ip的时候，需要选择和atlas200 同一网段打ip，如果是工作站，ip会自动显示出来（我们使用的是192.168.70.22），可以自己输入。
  如果使用的是虚拟机，共享打主机打ip，就选择默认的[http://127.0.0.1:7007/](http://127.0.0.1:7007/)
  #### 1.2 接下来启动服务
  ```shell
  python3 presenterserver/presenter_server.py --app face_detection &
  ```
  如果启动正常，会出现
  ```shell
  Presenter socket server listen on 192.168.37.134:7006
  Please visit http://127.0.0.1:7007 for face detection
  ```
  一般不会这么顺利。。。。。
  这就是第一个坑，主要是权限不够， permission denied，需要修改python3.5下面安装打各种wheel的权限，执行
  ```shell
  sudo chmod 775 /usr/local/lib/python3.5/dist-packages/ -R
  ```
  修改所有文件夹下面的权限，就可以了～   （另外，监控摄像头打channel和MindStudio的网址虽然重复，但是端口号不同，不会冲突）
  
### 2.安装MindStudio
  ### 2.1 执行sh ./install.sh 之后报错
  ```shell
  sudo update-alternatives --remove python /usr/bin/python3
  ```
  删除python3 的候选项即可
