* composer 使用私有库gitlab

> 发布composer 包至gitlab

```text
包的composer.json
{
    "name": "ax/apollo-symfony",
    "license": "MIT",
    "authors": [
        {
            "name": "baofan",
            "email": "baofan@aaa.com.cn"
        }
    ],
    "require": {
        "php": "^7.1.3",
        "guzzlehttp/guzzle": "^6.3",
        "ext-curl": "*",
        "ext-json": "*"
    },
    "autoload": {
        "psr-4": {
            "Apollo\\": "src/"
        }
    }
}
```

在项目中使用
```text
    "repositories": {
        "0": {  //加入
            "type": "git",
            "url": "git@gitlab.aaa.com.cn:system/apollo-symfony.git",
            "reference": "master"
        },
        "packagist": {
            "type": "composer",
            "url": "https://mirrors.aliyun.com/composer/"
        }
    }
    "require": {
        "php": "^7.2",
        "ext-ctype": "*",
        "ext-curl": "*",
        "ext-iconv": "*",
        "ext-json": "*",
        "ext-openssl": "*",
        "ext-redis": "*",
        "ax/apollo-symfony": "dev-master" //加入
    }
```

