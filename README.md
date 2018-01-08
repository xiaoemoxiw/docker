### 安装docker
#### Centos 
###### yum update 
###### yum install -y docker
### nginx
###### 在nginx文件夹中执行mkdir conf.d
###### 然后执行cp nginx/demo_php_conf.d.conf nginx/conf.d，得到其中一个nginx的示例配置文件，这里可以配置无限多个站点，可以自定义nginx文件格式

### php-fpm
#### 定时任务：
###### 在定时任务放在cron文件夹中，增加新的定时任务文件，需要在supervisor中的program.conf指定读取的文件
#### 进程管理：
###### 现在进程管理配置文件中包括了队列任务，定时任务和php-fpm进程。其中[program:php-fpm]和[program:cron-restart]项不能修改
###### 增加一项进程，添加一项 
###### [program:进程名称] 下一行之后开始进程内容
###### 初始化一下，需要修改php /source/follow_cloud/artisan queue:work redis --queue=beiweiyun --sleep=3 --tries=3
###### /source/follow_cloud/artisan修改为对应项目的artisan路径
###### --queue=beiweiyun 修改为要开启队列的名称
###### 具体参考laravel手册

### docker-compose.yml
###### 执行一下命令mv docker-compose-demo.yml docker-compose.yml

### 执行docker
###### 在docker-compose.yml所在目录，也就是docker代码的根目录，执行一下命令。
###### 启动项目：docker-compose up -d
###### 关闭项目：docker-compose down

### 进入容器
###### 本项目的根目录下有一个叫exec.sh的脚本，在本目录下执行[./exec.sh 容器名称]即可进入目录。
##### 注意：
###### 在执行[./exec.sh 容器名称]之前，先执行[chmod +x ./exec.sh]命令,给脚本赋予执行权限。
##### exec.sh更方便的使用方式
###### 执行：cp ./exec.sh /usr/local/bin/exec && chmod +x /usr/local/bin/exec
###### 在任何目录下，都可以执行  [exec 容器名称] 来进入容器

###### 进入php容器：exec php
###### 进入mysql容器：exec mysql
###### 进入redis容器：exec redis
###### 进入nginx容器：exec nginx

### 执行npm或者cnpm
###### 完成进入容器这个步骤以后，通过exec php 进入php容易
###### 然后直接执行cnpm即可使用cnpm命令



