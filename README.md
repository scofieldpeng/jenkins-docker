# jenkins-docker

docker中跑jenkins的docker-compose配置

## 启动

### step1:

将docker-compose.yml中的的16行的$(which pwd)替换为宿主机上真实的路径，例如`/usr/local/bin/docker`

### step2:

将nginx中的`conf.d/default.conf`文件中的${SERVER_NAME}替换成真实要用的域名

### step3:

nginx下新建ssl文件夹，将证书文件放进该文件夹，并替换成`server`的文件名（后缀不变），默认为key和crt后缀，如果是pem后缀，自行到更改`conf.d/default.conf`下的相关配置

### step4:

执行`docker-compose up`启动，然后输入https://server_name进行访问，初始化jenkins即可

## Tips:

### 替换jenkins镜像的源为国内源

```bash
sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
```

### 如果jenkins中的docker提示`error while loading shared libraries: libltdl.so.7: cannot open shared`

```bash
apt-get update && apt-get install -y sudo libltdl-dev
```