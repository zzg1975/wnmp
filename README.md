
# WNMP

## 软件简介

***本软件包专门为ThinkPHP 3.2.3和Moodle而写的WNMP运行架构***

**作者：曾棕根 老师**

- 2021-06-08  于宁波市北仑区
- 邮箱：461932968@qq.com
- 手机：18757462581
- Moodle亚洲开发群：QQ群号263569269

## 技术公开

- 本闪电Moodle包中的WNMP/LNMP架构技术改进已经写成论文发表在全国中文核心期刊《计算机应用与软件》杂志，分别是：
- （1）2018年4月15发表，论文名称《便携式高性能WNMP架构的研制》，论文查询网址www.cnki.net。

- （2）2021年6月15发表，论文名称《LNMP生产服务器技术改进》，论文查询网址www.cnki.net。

## 适用环境

- Windows 7或Windows 10 64位操作系统，同一年代的Windows服务器版本操作系统也能正常运行。

## 组件版本

- 【Nginx版本】1.20.0 stable
- 【PHP版本】php-7.3.28-nts-Win32-VC15-x64
- 【MariaDB版本】10.4.19 stable【注意：10.5.10版本不能在Windows 7上运行，在 Windows 10上能运行，故没有使用这个版本】
- 【ThinkPHP版本】3.2.3

## 集成的Moodle开发工具

免责声明：下面几个工具是从官网上下载的，集成在这里，方便用户使用，如果有异议，请官方邮件联系我删除！

- 1、C:\wnmp\navicat150_mysql_en_x64.exe   :  Mysql数据库可视化Client端

## 本WNMP运行包具体使用步骤    

**********************************************************************

- 1、本包的运行环境是Windows 7或Windows 10 64位操作系统，或同一年代的Windows服务器版本的操作系统。
- 2、Windows操作系统中内存至少为2GB，否则本闪电包WNMP架构无法启动。若要作为生产环境使用，内存至少要4GB，32GB内存就更好了。
- 3、本闪电包中的Nginx运行在80端口，所以要先检查80端口是否已被占用，如果被占用，那必须先停用80号端口。以管理员的身份进入命令行窗口，运行命令【netstat -ano】，查看80号端口是否处于LISTENING监听状态。如果没有找到80端口，恭喜你，本步操作到此为止。如果发现80号端口处于LISTENING监听状态，则记下它对应的PID即进程ID号，再打开任务管理器，在详细信息页中通过该PID列找到对应的映像名称。如果映像名称是XAMPP、Tomcat之类的Web运行框架，请先卸载它或禁用它；如果是IIS微软Web服务器，也请停用它。如果映像名称是System即被系统进程占用，那么应该不会是真正的系统，而是微软的其余系列产品的进程在运行，那么请按这两种方法之一解除占用，推荐使用第（1）种方法：
  （1）Win10中，控制面板-程序-启用或关闭Windows功能-Internet Information Services-万维网服务：关闭；.NET Framework 4.8 Advanced Services-WCF服务-HTTP激活：关闭；.NET Framework 4.8 Advanced Services-ASP.NET 4.8：关闭。这种方法关闭，不会影响打印机服务。
  （2）以管理员身份运行cmd，再在命令行窗口中输入【net stop http】，如果提示是否真的需要停止这些服务，则选择”Y“，完成后输入【sc config http start=disabled】，再重启win10操作系统，再在命令行中运行【netstat -ano】，发现80号端口已经没有被占用了。但是，一旦使用了【sc config http start=disabled】这个命令，Print Spooler服务无法启动，先前安装好的打印机找不到了，无法进行打印。若要恢复设置，则需要以管理员身份运行cmd,输入【sc config http start= demand & net start http】，这时候发现Print Spooler服务可以启动了，之前安装好的打印机能正常打印了。

- 4、从github上下载wnmp-main.zip到C盘根目录下，解压缩后目录名称是【C:\wnmp-main】,请一定要把所在目录名称修改为【C:\wnmp】,否则无法运行本架构。本架构默认在【C:\wnmp】这个固定目录中运行。
    从gitee上下载zzg1975-wnmp-main.zip到C盘根目录下，解压缩后目录名称是【C:\wnmp】，无需修改。
- 5、安装Visual C++ Redistributable for Visual Studio 2015、2017 和 2019， 
  运行压缩包根目录下software文件夹内的VC_redist.x64-2015-2019.exe进行安装。因为php 7.3是用VC15 或者 VS16编译的。
  如果不安装它，启动PHP时，出现“由于找不到 VCRUNTIME140.dll，无法继续执行代码。”的错误信息，且PHP的php_intl.dll模块无法加载！ 
  该程序是从这里下载的 
  https://aka.ms/vs/16/release/VC_redist.x64.exe

​       可能无法升级，主要是操作系统有些补丁没打上，安装时确保windows更新被打开了
​       如果提示安装失败，请先把之前已安装的全部的Visual C++ Redistributable for Visual Studio 2015卸载！

- 6、 先关闭正在运行的安全软件，如360安全卫士、360杀毒等安全软件，它们会阻止创建zzg_mysql服务；再用鼠标直接双击startwnmp.bat和stopwnmp.bat来运行和停止启动nginx、PHP和MariaDB服务或进程。如果当前用户不是Administrator账号登录，这两个命令会先叫你输入Administrator账号的密码，否则WNMP架构不能运行！
  这时，在任务管理器中，就能看到zzg_mysql服务的ID号了，说明mysql数据库服务安装成功，且在运行状态中。
  startwnmp.bat的功能是创建zzg_mysql开机自动启动的服务，并立即启动这项服务，这项服务有对应的MySQL进程。
  可以从Windows的【控制面板-管理工具-服务】中看到zzg_mysql服务及其进行ID号。

  如果大家使用阿里云，请一定记住，内存2GB太小了，无法使闪电包运行顺畅。至少要4GB的内存资源，这样mysql的innodb缓存开到2GB数据库才能展开，性能才会好。内存增大后的配置，请看本文件后面的Q4。

- 7、再在浏览器（Firefox浏览器、Chrome浏览器为最佳）中输入【http://127.0.0.1/】或【这台服务器的内网IP】或【这台服务器的外网IP】或【这台服务器的域名】即开始运行WNMP。
  其中MySQL数据库账号为root，密码为空，端口为3366
  
- 8、若要停止并删除zzg_mysql服务，则需运行stopwnmp.bat。 
  需要注意的是，运行stopwnmp.bat后，会从Windows的【控制面板-管理工具-服务】中
  直接停止并删除zzg_mysql服务，因此，重新启动Windows后，mysql就不会自动启动了，还需要运行一次startwnmp.bat。 

- 9、若要关闭或重启Windows操作系统，请务必先运行C:\wnmp\stopwnmp.bat；开机后，请务运行一次C:\wnmp\startwnmp.bat。


*******************************************************************************

## FAQ

### Q1：本安装包会生成哪几个服务和哪几个进程？

支持startwnmp.bat后，会注册并生成 zzg_mysql服务，在管理工具-服务窗口中可以管理它们；
并生成对应的进程：nginx.exe（3个进程，1个父进程，2个子进程）、mysqld.exe、php-cgi.exe（8个PHP FastCGI进程）、xxfpm.exe（8个PHP FastCGI进程的管理进程）。
运行stopwnmp.bat后，会停止并注销上述服务，同时杀死nginx.exe、xxfpm.exe、php-cgi.exe、mysqld.exe进程。

### Q2：您在哪里修改了端口？

nginx端口为80，修改文件：\nginx\conf\nginx.conf
MySQL端口为3366，修改文件：\mariadb\bin\my.ini 和 \php\php.ini
MySQL账号为root，密码为空。

### Q3：您现在的配置是2GB内存的最佳配置，如果我内存增大了，应当修改哪里？

请将\mariadb\bin\my.ini：innodb_buffer_pool_size = 64M  的64MB内存设置为你电脑内存的50%~80%大小。
例如，你内存为32GB，则可以设置为：\mariadb\bin\my.ini：innodb_buffer_pool_size = 16G，如果内存再大，注意不要超过16GB。

用记事本打开\nginx\conf\nginx.conf，将最顶上的【worker_processes  2;】修改为你CPU的核数。
用记事本打开\startwnmp.bat，将 【-n 8】修改为16、32、64、128等值，最大不要超过128。

上述配置完成后，需要重新启动nginx和MySQL，即先运行stopwnmp.bat，再运行startwnmp.bat，配置生效。

### Q4：如何管理MariaDB数据库？

请运行C:\wnmp\software\navicat150_mysql_en_x64.exe程序来管理数据库，MariaDB数据库服务地址为localhost，用户名为root，密码为空，端口为3366。


### Q5：如何将WNMP网址中的80端口修改为8081？

先运行stopwnmp.bat停止WNMP架构，再将 nginx/conf/nginx.conf中的这句修改掉即可：
  将【listen 80;】中的【80】修改为【8081】；
再将nginx/html/config.php中的IP地址中的8081去掉：
  将【$CFG->wwwroot='http://127.0.0.1';】修改为【$CFG->wwwroot='http://127.0.0.1:8081';】；
最后再运行startwnmp.bat启动wnmp架构，这样，直接通过【http://127.0.0.1:8081】来访问你的moodle网站了。

### Q6：生产环境里，至少需要有8GB内存，请问如何配置WNMP各部件？

  假如8GB内存，mysql的innodb分配5GB（具体操作看Q4）。其余3GB空着，留给php-cgi 1.5GB(php-cgi开64个，具体操作是，用记事本打开startwnmp.bat,找到“-n 8”，修改为“-n 64”)，留给windows操作系统1.5GB.    你的moodle肯定不卡了。

### Q7：Nginx配置ThinkPHP 3.2 PATHINFO模式(已经配置好了，这里只是作个记录)

```bash
server {
    listen       80;
    server_name  localhost ;
    root   "C:/wnmp/nginx/html";
    location / {
        index  index.html index.htm index.php;
        if (!-e $request_filename) {
            rewrite  ^(.*)$  /index.php?s=$1  last;
            break;
          }
        #autoindex  on;
      }
      location ~ \.php(.*)$ {
        fastcgi_pass   127.0.0.1:9000;
        fastcgi_index  index.php;
        fastcgi_split_path_info  ^((?U).+\.php)(/?.+)$;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        fastcgi_param  PATH_INFO  $fastcgi_path_info;
        fastcgi_param  PATH_TRANSLATED  $document_root$fastcgi_path_info;
        include        fastcgi_params;
    }
}
```

### Q8：如何开启PHP的Opcache模块？

C:\wnmp\php\php.ini的第1884行中，【opcache.enable = 0】默认将Opcache模块关闭了，主要为了修改了php语句后，可以立即看到运行效果，便于学生调试。在生产环境中，应该开户Opcache模块，以提高PHP网页的运行速度，设置【opcache.enable = 1】后，运行一次C:\wnmp\stopwnmp.bat后，再运行C:\wnmp\startwnmp.bat立即生效。

