
![](https://raw.githubusercontent.com/frainzy1477/_xPanel/master/xpanel.png)



安装面板 PANEL INSTALL NGINX
```
系统CentOS 7x64
安装Ngnix Server
安装PHP 7.3+
安装Ioncube Loader * [Ioncube Loader](https://www.howtoforge.com/tutorial/how-to-install-ioncube-loader/#-configure-ioncube-loader-on-centos)
安装Database(mysql or mariab)
安装Cron
	
	
下载程序代码
git clone https://github.com/frainzy1477/_xPanel.git tmp -b master && mv tmp/.git . && rm -rf tmp && git reset --hard
chmod -R 777 *

xpanel的配置上来
config/config.php

创建管理员
php cronjob createAdmin

打开nginx Config

同时，root那一行改为
root /home/xxxx/xxx/public;

然后添加下面这一段到 server
location / {
    try_files $uri $uri/ /index.php$is_args$args;
}

重启一下 nginx
service nginx restart
systemctl restart nginx 

导入 sql 目录下的 sql/xpanel.sql

crontab -e ，添加以下六段
0 */1 * * * php /home/xxxx/xxxx/cronjob backup
0 */1 * * * php /home/xxxx/xxxx/cronjob rate
*/1 * * * * php /home/xxxx/xxxx/cronjob checkjob
59 23 * * * php /home/xxxx/xxxx/cronjob dailyjob
```


安装后端 DOCKER BACKEND INSTALL

```
CENTOS 7
-------------------------------
cd /root && \
rm -rf install.sh && \
yum -y install epel-release wget bash zip unzip update && \
wget https://raw.githubusercontent.com/frainzy1477/_xPanel/master/install.sh -O /root/install.sh && \
chmod +x  install.sh && \
bash install.sh
```

```
UBUNTU 18/20
-------------------------------
cd /root && \
rm -rf install.sh && \
apt install wget bash zip unzip && \
wget https://raw.githubusercontent.com/frainzy1477/_xPanel/master/install.sh -O /root/install.sh && \
chmod +x  install.sh && \
bash install.sh
```
