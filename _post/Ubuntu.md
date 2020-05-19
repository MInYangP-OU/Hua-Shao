# Ubuntu Configure And Some Commands 

### 1. dotnet core (C#)
```python
$ mkdir -p $HOME/dotnet && tar zxf dotnet-sdk-3.1.201-linux-x64.tar.gz -C $HOME/dotnet

# ~/.bashrc
#PATH
export PATH=$PATH:$HOME/dotnet
#end line add
export DOTNET_ROOT=$HOME/dotnet

$ source ~/.bashrc
```

### 2. Nodejs
```python
# soft link
$ ln -s /home/username/node-v0.10.26-linux-x64/bin/node /usr/local/bin/node
$ ln -s /home/username/node-v0.10.26-linux-x64/bin/npm /usr/local/bin/npm
# cnpm
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
$ ln -s /home/username/node-v0.10.26-linux-x64/bin/cnpm /usr/local/bin/cnpm
#http-server
$ cnpm install -g http-server
$ ln -s /home/username/node-v0.10.26-linux-x64/bin/http-server /usr/local/bin/http-server

```

### 3. git
```
$ git config --global user.name "your_name"
$ git config --global user.email "your_email"

$ git config --list

$ ssh-keygen -t rsa -C "your_email"
$ cd ~/.ssh
$ cat id_rsa.pub

$ git clone ***
$ git add .
$ git commit -m "your_message"
$ git push -u origin

```

### 4. Matlab
```
https://www.cnblogs.com/sixuwuxian/p/12512275.html

```

### 5. MiniConda3
```python
# .sh file
$ chmod 777 Miniconda3-latest-Linux-x86_64.sh
$ sh Miniconda3-latest-Linux-x86_64.sh
# Do you wish the installer to initialize Miniconda3 by running conda init?
$ [no] >>> no

$ conda #no
$ vim ~/.bashrc
export  PATH="/home/your_home_name/miniconda3/bin:"$PATH
$ source ~/.bashrc
$ conda #yes

//conda add qinghua 
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/
conda config --set show_channel_urls yes 
conda config --get channels

$ conda env list
$ conda create -n your_env_name python=3.6.7
$ conda env list
$ source activate(deactivate) your_env_name

https://blog.csdn.net/weixin_43840215/article/details/89599559
```

### 6. VM and Foxit Reader
```
./***.bundle
./***.run
```

### 7. AppImage
```
AppImage

/home/$USERNAME/.config/  # 这个目录中是一些配置文件
/home/$USERNAME/.local/share/applications  # 这个目录中是一个桌面文件 appimagekit.desktop
```

### 8. Terminal
```

```