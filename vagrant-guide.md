# Vagrant初级指南

## 介绍
工欲善其事必先利其器，Vagrant就是一个提升你开发效率，免去因配置环境而浪费的时间的瑞士军刀。

简单的说，Vagrant是一个虚拟机(简称VM)管理工具，能帮助开发人员更有效的使用VM来进行开发，并减少因为环境不一致等因素造成的BUG。

## 安装
本文档介绍了Windows下安装的方法，Linux或者Mac系统请自行参考官方文档。

### 安装Vagrant
版本是1.6.5。

访问`\\192.168.225.43\Share\Software\Vagrant`，拷贝到本地再安装`vagrant_1.6.5.msi`。

### 安装VirtualBox
版本是4.3.18。

访问`\\192.168.225.43\Share\Software\Vagrant`，拷贝到本地安装`VirtualBox-4.3.18-96516-Win.exe`。

## 初始化标准的Ubuntu 12.04 64位VM
Vagrant和VirtualBox都安装好以后，现在开始教你怎么使用Vagrant来创建虚拟机。

### 新建并启动VM
访问`\\192.168.225.43\Share\Software\Vagrant\boxes\ubuntu-1204-64`，拷贝整个目录到
`C:\Users\<你的用户名>\vagrant\`下。

再启动CMD(命令行工具)，并CD到ubuntu-1204-64目录。

最后在命令行里执行`vagrant up`，你会看到如下输出：
```
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box 'ubuntu-1204-64'...
==> default: Matching MAC address for NAT networking...
==> default: Setting the name of the VM: ubuntu-1204-64_default_1413510419186_44629
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
    default: Adapter 2: hostonly
==> default: Forwarding ports...
    default: 22 => 2222 (adapter 1)
==> default: Running 'pre-boot' VM customizations...
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default: Warning: Connection timeout. Retrying...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
==> default: Configuring and enabling network interfaces...
==> default: Mounting shared folders...
    default: /vagrant => C:/Users/foobar/vagrant/ubuntu-1204-64
```

### SSH登录VM
用putty或者其他SSH客户端登录VM。
```
host: 127.0.0.1
port: 2222
username: vagrant
password: vagrant
```
### 关闭VM
使用`vagrant halt`命令可以正常关闭VM

使用`vagrant suspend`命令可以先保存当前状态再关闭VM

### 重启VM
当配置文件`Vagrantfile`发现变化后需要执行`vagrant reload`命令加载配置。

该命令也可以用于重启VM。

### 更改VM IP
编辑`Vagrantfile`, 修改`config.vm.network "private_network", ip: "192.168.33.10"`
可以指定VM IP。

使用`ifconfig`命令可以察看当前VM的IP。

#### 私有网络
默认是Private Network，只有Host机器可以访问。

#### 共有网络
在`Vagrantfile`里启用`config.vm.network "public_network"`，并注释掉`config.vm.network "private_network"`可以使用共有网络。
让其他机器可以访问你的VM。

### 再新建一个VM
新建一个目录，拷贝Vagrantfile到新目录。

运行命令行，CD到该目录再运行`vagrant up`

### 删除VM
在Vagrantfile所在目录运行`vagrant destroy`就可以删除该目录所绑定的VM。

## 使用VM

### 共享目录
Vagrantfile文件所在目录是默认的共享目录，该目录下所有文件能在VM里的`/vagrant`目录下找到。

### 已安装组件
1. htop
1. NodeJS v0.11.14, NPM v2.0.0
1. Yeoman v1.3.2
1. Grunt CLI v0.1.13
1. Bower v1.3.12
1. Oracle JDK 7 1.7.0_72
1. Tomcat v7.0.26
1. Nginx v.1.1.19
1. php5-fpm v5.3.10
1. PHP Extension
    1. PEAR
    1. APC
    1. GD
    1. mcrypt
    1. xmlrpc
    1. memcache
    1. redis
    1. mongo
    1. imagick
1. Mysql v5.5.40
1. Redis v2.2.12
1. Memcached v1.4.13
1. MongoDB v2.0.4
1. ImageMagic  v6.6.9-7
1. Composer 1.0-dev

### 安装新组件
`sudo apt-get install <package-name>`

### 安装NodeJS的包
`cnpm install <package>` or `cnpm install -g <package>`

项目中有使用package.json的话，通过`cnpm install`来安装依赖包。

PS:

1. NodeJS是通过NVM安装的，所有安装包时不需要加sudo
2. CNPM是NPM的替代，从taobao的npm镜像下载包。

### 察看系统资源和进程
使用htop工具可以查看top命令的信息

### 启动和停止服务
`sudo service nginx {start|stop|restart|reload|force-reload|status|configtest}`

`sudo service tomcat7 {start|stop|restart|try-restart|force-reload|status}`

`sudo service php5-fpm {start|stop|status|restart|reload|force-reload}`

`sudo service mysql {start|stop|restart}`

`sudo service redis-server {start|stop|restart|force-reload}`

`sudo service memcached {start|stop|restart|force-reload|status}`

`sudo service mongodo {start|stop|restart|force-reload|status}`

### 组件配置

#### Nginx
配置文件目录：`/etc/nginx/`

Document Root： `/usr/share/nginx/www`

#### PHP
php.ini位置：`/etc/php5/fpm/php.ini`

#### MySQL
root用户密码：password

root用户可以远程登录

配置文件目录：`/etc/mysql`

#### Tomcat
配置文件目录：`/etc/tomcat7`

Document Root: `/var/lib/tomcat7/webapps/`

Tomcat Manager Web App: http://192.168.33.10:8080/manager
Username: tomcat, Password: tomcat

#### Redis
配置文件`/etc/redis/redis.conf`

#### Memcached
配置文件`/etc/memcached.conf`

#### MongoDB
配置文件`/etc/mongodb.conf`

### 常见问题
#### 怎样建立symbol link
在Nginx的www目录下建立一个symbol link指向共享目录下的wordpress目录：

假设当前目录是`/usr/share/nginx/www`，wordpress安装目录是`/vagrant/wordpress`

`sudo ln -s /vagrant/wordpress wordpress`

#### 共享目录中执行`(c)npm install`报错
如果你在共享目录/vagrant下运行`cnpm install`遇到错误类似：

`npm ERR! EPROTO, symlink '../express/bin/express'`

说明npm在创建symbol link的时候失败了。
因为共享目录本质是一个windows目录，而windows因为安全原因，默认是不允许非管理员用户创建symbol link的。

所有一个workaround就是在打开命令行CMD时候，选择以管理员身份运行。
再执行`vargrant up`启动虚拟机，这样在VM的共享目录里就可以创建symbol link了。

但是还没完，接下来你会遇到另一个问题：windows目录或者文件路径最大只支持260个字符，如果node_modules安装时嵌套比较深的话，
安装还是会失败。

所以建议把node_modules安装到linux的目录下，然后在共享目录symbol到该node_mudules目录。
具体步骤如下：
```
$ mkdir ~/node_modules
$ cd /vagrant/angular-express-blog
$ ln -s ~/node_modules node_modules
$ cnpm install
$ ll
...
lrwxrwxrwx 1 vagrant vagrant    0 Oct 17 07:07 node_modules -> /home/vagrant/node_modules//
...
```

这样操作的话安装应该可以成功，而且在Windows的Host机器上，可以直接编辑/vargrant目录下的其他文件。

更多信息可以参考[这篇文章](http://kmile.nl/post/73956428426/npm-vagrant-and-symlinks-on-windows)。

### Ubuntu Box完整的安装脚本
VM创建完整的脚本请看[这篇文章](ubuntu-box-initialization.md)