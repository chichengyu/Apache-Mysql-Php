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

附：
PhpMyAdmin安装：
	PhpMyAdmin官网：https://www.phpmyadmin.net/
	

	下载得到phpMyAdmin-4.7.0-all-languages.zip解压重命名为PhpMyAdmin，并进入该文件夹，找到config.sample.inc.php，复制一份改名为config.inc.php，用文本编辑器打开改文件。找到下列代码：
		$cfg['blowfish_secret'] = 'xiaochi',// 随便设置,只是一个短语密码
	    并在最后追加如下：
		$cfg['Servers'][$i]['host'] = 'localhost';
		$cfg['Servers'][$i]['port'] = '3306';
		$cfg['Servers'][$i]['user'] = 'root';
		$cfg['Servers'][$i]['password'] = '';
	进入apache的conf文件夹下，新建一个phpmyadmin.conf文件，文本编辑器打开，加入下列代码，如：
		特别注意：此处的 D:/LAMP/phpMyAdmin/  路径最后的斜线 / ，一定不能少
		Alias /phpmyadmin "D:/LAMP/phpMyAdmin/"
		<Directory "D:/LAMP/phpMyAdmin/">
		    Options Indexes FollowSymLinks MultiViews
		    AllowOverride all
		    Require all granted
		    DirectoryIndex index.php index.html
		    php_admin_value upload_max_filesize 128M
		    php_admin_value post_max_size 128M
		    php_admin_value max_execution_time 360
		    php_admin_value max_input_time 360
		</Directory>
	保存退出
	最后在apache/conf文件夹内找到配置文件httpd.conf，用文本编辑器打开，在末尾增加一行
		# configure the path to phpmyadmin.conf
		Include D:/LAMP/apache/Apache24/conf/phpmyadmin.conf
	保存退出，重启apache
	在浏览器中输入 http://localhost/phpmyadmin，出现登录界面就ok了。
	
	
	注意：phpmyadmin安装完成，登录进入后，滚动条拉倒最底部，可能会看到如下信息
		phpmyadmin显示高级功能尚未完全设置部分功能未激活，请点击这李查看原因
	      这样的情况，其实解决此问题的方法已经提示了 Create a database named 'phpmyadmin' and setup the phpMyAdmin configuration storage there.
	      解决：创建一个phpmyadmin的数据库，然后在phpmyadmin的文件夹l里面找到phpmyadmin/sql/create_tables.sql，直接导入即可解决

另外说明：
	
	修改Mysql密码为空的方法
		update user set password=password(‘’) where user=’root’;
	再输入   flush privileges;
	然后 quit退出
	重启Mysql，OK
