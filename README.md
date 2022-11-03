# Install Wordpress
PHP >= 7.4 
MySQL || MariaDB 
Apache || Nginx
## Todos
1. Install software
    - packet manager (apt, yum, apk, brew)
    - direct install (.exe, .dpkg, .rpm, .pkg)
    - compile from source
### Wordpress requirements
#### MySQL || MariaDB 
* mariadb -> repo (outdated)
1. Install via custom repo
add yum repo cfg ``/etc/yum.repos.d/Mariadb.repo``
```
[mariadb]
name = MariaDB
baseurl = https://ftp.bme.hu/pub/mirrors/mariadb/yum/10.8/centos7-amd64
gpgkey=https://ftp.bme.hu/pub/mirrors/mariadb/yum/RPM-GPG-KEY-MariaDB
gpgcheck=1
```
2. install mariadb packages
```bash
sudo yum install -y MariaDB-server MariaDB-client
```
3. start mariadb as a service
```bash
sudo systemctl start mariadb
```
4. execute sql
```bash
sudo mysql
```
```sql
create database blog;
create user 'blog' identified by 'blog!';
grant all privileges on blog.* to 'blog'@localhost identified by 'blog!';
FLUSH PRIVILEGES;
```
#### PHP
