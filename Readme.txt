---------------------------------------------------------------------


docker文件夹下是wotrus_nginx镜像所需的打包文件

打包方法：
docker build -t wotrus_nginx:latest .
保存镜像文件到本地：
docker save -o wotrus_nginx.tar wotrus_nginx:latest
将镜像文件复制到服务器之后加载镜像：
docker load<wotrus_nginx.tar


---------------------------------------------------------------------


wotrus_nginx文件夹下是启动wotrus_nginx容器相关的文件

启动命令：
docker-compose up -d


---------------------------------------------------------------------