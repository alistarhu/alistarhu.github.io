# 训练机使用说明

## 用户名与密码

用户名：姓名首字母缩写，如：hl

初始密码：123456

**密码修改方法：**
```Shell
$ sudo su
$ sudo passwd XXX   （XXX为当前用户名）
$ 输入新密码，确认密码。
```

## 目录介绍
- `/home/XXX` 是每个人各自的目录

- `/media/data1/` 和 `/media/data2/`两块硬盘（每块3T）可供存放大型的训练数据
   - `/media/data1/XXX` 用于存放私人文件数据的目录

   - `/media/data2/` 用于存放公共文件数据的目录

- `/software/`是预装的一些软件

## 预装软件
- CUDA9.0 + cudnn7.0.5
- tensorflow-gpu 1.9.0
- caffe
- cmake
- vim
- python2:numpy scipy matplotlib pandas sklearn等

## 远程访问服务器
- 连接服务器
   - linux环境下
   ```Shell
   $ ssh XXX@172.17.122.203
   ```
   - Windows环境下：可以安装Xshell等软件进行访问

- 数据传输
   - linux环境下
    ```Shell
    $ scp source_file XXX@172.17.122.203:dest_path  (单个文件)
    ```
    ```Shell
    $ scp -r source_folder XXX@172.17.122.203:dest_path  (文件夹)
    ```
   - Windows环境下
   可以使用Xftp进行界面化文件传输操作

## 安装python包
```Shell
$ pip install XXX --user
```


>使用过程中遇到任何问题都可以联系我：
>
>**胡磊**
>
>**座位号：21B45**
>
>**email:hl7356@arcsoft.com.cn**
>
>**skype:hl7356**
