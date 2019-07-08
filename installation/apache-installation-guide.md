# On Linux

Compiling and installing Apache Httpd Server

pre-installation
	解压缩httpd
	解压缩apr-<version>和apr-util-<version>源代码包到httpd目录下的srclib目录下,
	并重名为不带版本号的名称：apr和apr-util

1 ./configure --prefix=/usr/local/apache2 \
   --enable-so
   --with-included-apr
   --with-pcre=/usr/local/pcre 

2 make

3 checkinstall

*****************************
Compiling and installing PHP7

./configure --prefix=/usr/local/php7 \
--with-apxs2=/usr/local/apache2/bin/apxs \
--with-mysqli \
--with-pdo-mysql \
--enable-mbstring \
--enable-zip \
--enable-ftp \
--with-curl


# On Windows
















*************************************
Apache-$APACHE_PREFIX/conf/httpd.conf

Edit the Apache httpd.conf file in the $APACHE_PREFIX/conf directory.
(a) Uncomment the line with the ServerName directive and specify the host name and port number for your web server.
    For example: ServerName myhostname.ibm.com:8080
(b) Locate the Listen directive and ensure that it is set to the same port number you specified in the ServerName directive.
(c) Change the DirectoryIndex directive to DirectoryIndex index.html index.php
(d) Change all instances of AllowOverride none to AllowOverride All


*******************************
PHP-$PHP_PREFIX/lib/php.ini

(a) Copy the php.ini configuration file and the libphp5 module to your PHP installation directory.
	cp php.ini-production $PHP_PREFIX/lib/php.ini
	cp libs/libphp5.so <<$PHP_PREFIX>>/libphp5.so
(b) Edit the php.ini configuration file.
	Set <<doc_root>> to the htdocs directory of your Apache installation ($APACHE_PREFIX/htdocs).
	Set extension_dir to the lib/php/exensions directory of your PHP installation ($PHP_PREFIX/lib/php/extensions)
	Add the line "extension=pdo_informix.so" to load the PDO_INFORMIX driver
	Set max_execution_time to the number of seconds you want the web server to wait before timing out and set memory_limit to at least 256 M
(c) Edit the Apache httpd.conf file ($APACHE_PREFIX/conf/httpd.conf)
	Comment the existing LoadModule php5_module modules/libphp5.so directive.
	Add the following lines, where everything in angle brackets (<< >>) is replaced by the actual path:
	LoadModule php5_module <<$PHP_PREFIX>>/libphp5.so
	AddType application/x-httpd-php .php
	PhpIniDir <<$PHP_PREFIX>>/lib

***********************
