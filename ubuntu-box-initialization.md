# 更改APT的源地址到CN镜像
```
$ sudo nano /etc/apt/sources.list
$ sudo apt-get update
```
# 安装htop
$ sudo apt-get install htop

# 安装NodeJS
## 通过APT安装（慢）
```
$ curl -sL https://deb.nodesource.com/setup | sudo bash -
$ sudo apt-get install nodejs
```

## 通过NVM安装（较快）
```
$ sudo apt-get install build-essential libssl-dev
$ curl https://raw.githubusercontent.com/creationix/nvm/v0.17.2/install.sh | bash
$ source ~/.profile
$ nvm ls-remote
$ nvm install 0.11.14
$ nvm alias default 0.11.14
```

## 安装NPM镜像
`$ npm install -g cnpm`

## 安装NodeJS工具包
```
$ cnpm install -g yo
$ cnpm install -g generator-webapp
$ cnpm install -g generator-angular
$ cnpm install -g bower
$ cnpm install -g grunt-cli
```

# 安装Tomcat
`$ sudo apt-get install tomcat7 tomcat7-admin tomcat7-docs tomcat7-examples`

## 修改配置
$ sudo nano /etc/tomcat7/tomcat-users.xml
```
  <role rolename="manager"/>
  <role rolename="manager-gui"/>
  <role rolename="admin"/>
  <role rolename="admin-gui"/>
  <user username="tomcat" password="tomcat" roles="manager-gui,admin-gui"/>
```

$ sudo nano /etc/default/tomcat7

Enable remote debugging: uncomment JAVA_OPTS="${JAVA_OPTS} -Xdebug -Xrunjdwp:transport=dt_socket,address=8000,server=y,suspend=n" 

# 安装Nginx
$ sudo apt-get install nginx-extras

# 安装PHP5-fpm
$ sudo apt-get install php5-fpm

$ sudo nano /etc/php5/fpm/php.ini

Find the line, cgi.fix_pathinfo=1, and change the 1 to 0.
cgi.fix_pathinfo=0

$ sudo nano /etc/php5/fpm/pool.d/www.conf

Find the line, listen = 127.0.0.1:9000, and change the 127.0.0.1:9000 to /var/run/php5-fpm.sock.

listen = /var/run/php5-fpm.sock
Uncomment all permission lines, like:
```
listen.owner = www-data
listen.group = www-data
listen.mode = 0660
```
```
$ sudo service php5-fpm restart
$ sudo nano /etc/nginx/sites-available/default
```
```
# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
#
location ~ \.php$ {
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
#       # NOTE: You should have "cgi.fix_pathinfo = 0;" in php.ini
#
#       # With php5-cgi alone:
#       fastcgi_pass 127.0.0.1:9000;
#       # With php5-fpm:
        fastcgi_pass unix:/var/run/php5-fpm.sock;
        fastcgi_index index.php;
        include fastcgi_params;
}
```

## 安装PHP扩展
$ sudo apt-get install php-apc	php5-curl php5-gd php5-imagick php5- mcrypt php5-memcache php-pear php5-xmlrpc

-- update make
$ sudo apt-get install make
$ sudo pecl install mongo

-- use nano instead, otherwise report permission denied
echo 'extension=mongo.so' > /etc/php5/conf.d/mongo.ini
sudo pecl install redis

-- use nano instead, otherwise report permission denied
echo 'extension=redis.so' > /etc/php5/conf.d/redis.ini

Update for cli by modifying file "/etc/php5/cli/php.ini"
```
max_execution_time = 300
memory_limit = 512M
error_reporting = E_ALL | E_STRICT
```

# 安装Mysql
```
sudo apt-get install mysql-server php5-mysql
sudo /usr/bin/mysql_secure_installation
```

From /etc/mysql/my.cnf
```
# Instead of skip-networking the default is now to listen only on
# localhost which is more compatible and is not less secure.
#bind-address           = 127.0.0.1
```

(comment this line: bind-address = 127.0.0.1)


Then run service mysql restart.

then $ mysql -u root -ppassword
```
mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'password';
mysql> FLUSH PRIVILEGES;
```

# 安装Redis
$ sudo apt-get install redis-server

# 安装Memcached
$ sudo apt-get install memcached

# 安装Git
$ sudo apt-get install git

# 安装MongoDB
$ sudo apt-get install mongodb

# 安装Oracle JDK 7
```
$ sudo apt-get install python-software-properties
$ sudo add-apt-repository ppa:webupd8team/java
$ sudo apt-get update

$ sudo apt-get install oracle-java7-installer

$ sudo update-alternatives --config java

$ sudo nano /etc/environment

Add JAVA_HOME= /usr/lib/jvm/java-7-oracle

$ source /etc/environment
$ echo $JAVA_HOME
```

# 安装ImageMagic
`$ sudo apt-get install imagemagick`

# 安装Composer
```
$ curl -sS https://getcomposer.org/installer | php
$ sudo mv composer.phar /usr/local/bin/composer
```