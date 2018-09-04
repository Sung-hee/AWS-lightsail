## AWS EC2에서 php 설치하기 !

### 1. PPA 사용설정

```bash
sudo apt-get install 
sudo add-apt-repository ppa : ondrej / php
sudo apt-get update
```

### 2. PHP 7.1설치

```bash
sudo apt-get install php7.1
```

### 3. 특정 PHP 7.1 모듈 검색 및 설치

```bash
sudo apt-cache search php7.1
```

### 4. 모듈설치

```bash
sudo apt-get install php7.1 php7.1-cli php7.1- 일반 php7.1-json php7.1-opcache php7.1-mysql php7.1-mbstring php7.1-mcrypt php7.1-zip php7. 1-fpm
```

### 5. php.ini 파일 구성

```bash
php --ini | grep로드 됨
로드 된 구성 파일 : /etc/php/7.1/cli/php.ini
sudo nano /etc/php/7.1/cli/php.ini
```

### 5. 2) 변경

```bash
cgi.fix_pathinfo = 0
```

### 5. 3) 서비스 시작

```bash
sudo systemctl restart php7.1-fpm.service
```

### 6. Nginx 

```bash
sudo apt-get install nginx
sudo vi /etc/nginx/sites-enabled/default
server {
        listen 80;
        server_name example.com www.example.com;
        root /var/www/example.com;
        index index.php;

        location / {
                try_files $uri $uri/ =404;
        }

        location ~ \.php$ {
            fastcgi_pass unix:/run/php/php7.1-fpm.sock;
            include snippets/fastcgi-php.conf;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }

        location ~ /\.ht {
                deny all;
        }
}
```

```bash
sudo nginx -t
sudo service nginx start
```

---

### SQLServer Install

#### 1. ODBC 13 Drvier 설치

```bash
$ curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
$ sudo sh -c 'curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list'
$ sudo apt-get update
$ sudo apt-get install php7.1-dev php-pear
```

#### 2. PECL tools 설치

```bash
$ sudo apt-get install php7.1-dev php-pear
```

#### 3. sqlsrv, pdo_sqlsrv 설치

```bash
$ sudo pecl install sqlsrv
$ sudo pecl install pdo_sqlsrv
```

#### 4. ini 파일 만들기

```bash
$ sudo sh -c 'echo "extension=sqlsrv.so" > /etc/php/7.1/mods-available/sqlsrv.ini'
$ sudo sh -c 'echo "extension=pdo_sqlsrv.so" > /etc/php/7.1/mods-available/pdo_sqlsrv.ini'
```

#### 5. php 확장기능 사용

```bash
$ sudo phpenmod sqlsrv pdo_sqlsrv
```

#### 6. nginx 및 php-FPM 재시작 (아파치는 아파치 재시작)

```bash
$ sudo service php7.1-fpm restart
$ sudo service nginx restart
```

