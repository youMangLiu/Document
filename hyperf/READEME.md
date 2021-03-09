下载镜像，宿主机与镜像里面的文件夹挂载

docker run -v /tmp/skeleton:/hyperf-skeleton -p 9501:9501 -it --entrypoint /bin/sh hyperf/hyperf:latest

# 镜像容器运行后，在容器内安装 Composer
wget https://github.com/composer/composer/releases/download/1.8.6/composer.phar
chmod u+x composer.phar
mv composer.phar /usr/local/bin/composer
# 将 Composer 镜像设置为阿里云镜像，加速国内下载速度
composer config -g repo.packagist composer https://mirrors.aliyun.com/composer

# 通过 Composer 安装 hyperf/hyperf-skeleton 项目
#### 这里可以后面跟project-dir-name 文件名称，你也可以切换到你要得目录下面去生成项目（如 /home/httpd）
composer create-project hyperf/hyperf-skeleton


####这一步是将容器里面得项目拷贝到你宿主机上
4、docker ps -a 找到你的container id, 然后 docker cp containerid:/home/httpd/your_project_name ./

5、配置 bin/hyperf.php 
在 date_default_timezone_set('Asia/Shanghai'); 后面加上以下代码
```text
if(!file_exists(BASE_PATH . '/vendor/autoload.php')){
    exec('composer install -vvv');
}
```

6、配置 .env 下 mysql,redis

7、 修改docker-compose.yml 里的 working_dir，volumes
```
version: 3.7

services:
  hf:
    image: hyperf/hyperf
    container_name: hy-ts
    volumes:
      - ./:/home/httpd/hyperf-ts
    ports:
      - 9501:9501
    command: php bin/hyperf.php start
    working_dir: /home/httpd/hyperf-ts
```

8、运行 docker-compose up，访问 ip + port  