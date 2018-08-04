# Apache-Mysql-Php
	记录一下windows下安装apache+2.4+mysql5.6.38+php5.6的安装过程与一些坑

	这是整理好的环境包,下载地址：https://share.weiyun.com/5n3ESRJ


Apache版本   	===>  Apache-2.4.33-win64-VC11


Mysql版本	 	===>  mysql-5.6.38-winx64

phpMyAdmin版本	===>  phpMyAdmin-4.8.0-all-languages


Php版本	 	 	===>  php-5.6.35-Win32-VC11-x64

Php-Redis扩展  	===>  php_redis-2.2.7-5.6-ts-vc11-x64

Redis版本		===>  Redis-win-x64-3.0.504

	注意：安装php_redis扩展与redis时,必须先phpinfo查看相对应的支持与版本

附：PhpMyAdmin安装：PhpMyAdmin官网：https://www.phpmyadmin.net/	

附：修改Mysql密码为空的方法\n
		update user set password=password(‘’) where user=’root’;
	再输入   \n
		flush privileges;
	然后 \n
		quit
	退出\n
	重启Mysql，OK
