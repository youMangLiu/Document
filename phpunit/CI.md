cp phpunit.xml.dist phpunit.xml
//指定环境
export APP_ENV=dev(或者其他环境)
//复制配置文件
cp .env.dist .env
//更换镜像
composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
//安装组件 （不执行脚本）
composer install --no-scripts
//创建数据库
php bin/console doctrine:database:create
//导入数据表
php bin/console doctrine:migrations:execute  --up 20200512075917 --no-interaction
//清除缓存
php bin/console cache:clear
//执行单元测试，-vvv展示执行过程
php bin/phpunit -vvv
//删除数据库
php bin/console doctrine:database:drop --force