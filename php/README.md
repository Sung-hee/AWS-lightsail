## AWS EC2에서 php 설치하기 !

### 1. PPA 사용설정

```
sudo apt-get install 소프트웨어 - 속성 - 공통점
sudo add-apt-repository ppa : ondrej / php
sudo apt-get update
```

### 2. PHP 7.1설치

```
sudo apt-get install php7.1
```

### 3. 특정 PHP 7.1 모듈 검색 및 설치

```
sudo apt-cache search php7.1
```

### 4. 모듈설치

```
sudo apt-get install php7.1 php7.1-cli php7.1- 일반 php7.1-json php7.1-opcache php7.1-mysql php7.1-mbstring php7.1-mcrypt php7.1-zip php7. 1-fpm
```

### 5. php.ini 파일 구성

```
php --ini | grep로드 됨
로드 된 구성 파일 : /etc/php/7.1/cli/php.ini
sudo nano /etc/php/7.1/cli/php.ini
```

### 5. 2) 변경

```
cgi.fix_pathinfo = 0
```

### 5. 3) 서비스 시작

```
sudo systemctl restart php7.1-fpm.service
```

### 6. Nginx 

```
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

```
sudo nginx -t
sudo service nginx start
```

