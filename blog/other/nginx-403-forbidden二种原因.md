# nginx 403 forbidden 二种原因

引起Nginx 403 forbidden有二种原因，一是缺少索引文件，二权限问题。今天又遇到 了，顺便总结一下。

###1，缺少index.html或者index.PHP文件
```
server {  
 listen       80;  
 server_name  localhost;  
 index  index.php index.html;  
 root  /home/zhangy/www; 
```
如果在/home/zhang/www下面没有index.php,index.html的时候，直接访问域名，找不到文件，会报403 forbidden。例如：你访问www.test.com而这个域名，对应的root指定的索引文件不存在。

###2，权限问题
```
server {  
 listen       80;  
 server_name  localhost;  
 index  index.php index.html;  
 root  /home/zhangy/www;  
```
我把web目录放在用户的所属目录下面，nginx的启动用户默认是nginx的，所以对目录根本没有读的权限，这样就会报403错误了。这个时候，把web目录的权限改大，或者是把nginx的启动用户改成目录的所属用户，重起一下就能解决。