windows下运行 hf


0、创建一下项目

1、docker run -it --name test-hf registry.cn-hangzhou.aliyuncs.com/jimu/php:7.4-alpine-v3.11-1.0

2、在镜像里 配置composer 加速：composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

3、切换到/home/httpd , 运行 composer create-project hyperf/hyperf-skeleton your_project_name你的项目名称

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

8、运行 docker-compose up，访问 ip + port  

#### windows docker 搭建及运行hyperf项目
    docker-composer.yml文件
    version: '3.7'
    services:
      hf:
        image: registry.cn-hangzhou.aliyuncs.com/jimu/php:7.4-alpine-v3.11-1.0-dev
        container_name: hy-study
        volumes:
          - ./:/home/httpd/hf-study
        ports:
          - 59501:9501
          - 59502:9502
        command: php bin/hyperf.php start
        working_dir: /home/httpd/hf-study

9、搭一个项目只要走一次前面8个步骤，后面可直接使用docker启动