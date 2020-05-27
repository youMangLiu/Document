mysql 使用docker运行的情况 如何导入几个G的sql文件 所以不要傻乎乎的直接再客户端导入

首先
docker exec -it mysql_docker_name bash

mysql -uroot -p 数据库名

set names utf8 #避免导入的时候中文乱码

source file (映射到容器中的文件地址)