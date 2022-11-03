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
repo's php version too old 5.4...
1. Install EPEL -> Extra Packages for Enterprise Linux
```bash
sudo yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
```
2. install php related repo
```bash
sudo yum install -y https://rpms.remirepo.net/enterprise/remi-release-7.rpm
``` 
3. install php packages
```bash
sudo yum install -y php80 php80-php php80-php-common php80-php-pecl-mysql
```
#### Apache HTTP Server
1. install apache 
```bash
sudo yum install -y httpd
```
2. start apache as a service 
```bash
sudo systemctl start httpd
```
### Instal wordpress itself
1. download wp ``https://pl.wordpress.org/latest-pl_PL.tar.gz``
```bash
wget https://pl.wordpress.org/latest-pl_PL.tar.gz -O wp.tar.gz
```
```bash
tar -xf wp.tar.gz
```
2. mv wp's files to dest: ``/var/www/html/``
    @toDo dest: ``/var/www/blog``
    ```bash
        sudo mv wordpress/* /var/www/html/
    ```
3. configure wp
    ```bash
        cp wp-config.php /var/www/html/wp-config.php
    ```
    ```php
    <?php
        define( 'DB_NAME', 'blog' );
        define( 'DB_USER', 'blog' );
        define( 'DB_PASSWORD', 'blog!' );
        define( 'DB_HOST', 'localhost' );
        define( 'DB_CHARSET', 'utf8mb4' );
        define( 'DB_COLLATE', '' );
        define( 'AUTH_KEY',         'F7seLTm#Fd#w-mIHhI{&5lWKs`krtB;0&2}^JwY*+^Y|A4/diW;M#b M4)|<i@Ht' );
        define( 'SECURE_AUTH_KEY',  's==bHxdSH>Ra6(xkC9&EB1kCx&G2Aes_u]iz zp1Yieq_E;+8BoA win7f9{]E%i' );
        define( 'LOGGED_IN_KEY',    '2ugHj]b=|Gwn]Czed5tuBCE{X+Oi83C7d=6|N,N`5l!W|Frk`^R5CNHQn~=.{U2G' );
        define( 'NONCE_KEY',        'KbQgFh>Oj]N2R0SGlWq%l,9,GW+!;UFX<?vmII?eOyfo3E,}=m^JyHvuk<|3q!w]' );
        define( 'AUTH_SALT',        'S;<+fXiag>u+I(UIj USQo{~*iA.t.[mtqJ&E%1gT/w|K20[mp~MbaXR42osAud|' );
        define( 'SECURE_AUTH_SALT', 'UIgSMmQTa*hQ(9q;NfxBuuLec+|u{6`bQgtW_X8/5055rtJi+}W@<kD!^PT};T}(' );
        define( 'LOGGED_IN_SALT',   'g!UvK* ePO3~}^S?SIIt. 6it*,R//t (r92@%H(ZQc,~QUU}uS1w9kuPHvl|wl-' );
        define( 'NONCE_SALT',       'bj[@RI@wnE2ST>cykT]>IywJ]C=~]!3`bG&tVf)_*M6`req9~zv4hCO<f2,K^s#:' );
        $table_prefix = 'wp_';
        define( 'WP_DEBUG', false );
        if ( ! defined( 'ABSPATH' ) ) {
            define( 'ABSPATH', __DIR__ . '/' );
        }
        require_once ABSPATH . 'wp-settings.php';
    ```
4. open wp -> browser http://{serverIP}
