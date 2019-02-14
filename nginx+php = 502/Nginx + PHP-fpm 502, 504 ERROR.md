## Nginx + PHP-fpm 502, 504 ERROR 

#### Ngninx 설정하기

1. 터미널에서 sudo vi /etc/nginx/sites-enabled/default 접속

```nginx
location / {
    try_files $uri $uri.html $uri/ @extensionless-php;
    index index.php index.html index.htm;

    proxy_connect_timeout 600;
    proxy_send_timeout 600;
    proxy_read_timeout 600;
    send_timeout 600;

    # 아래부터 버그 해결을 위해 추가해 주실 옵션입니다.
    # 502 에러를 없애기 위한 proxy 버퍼 관련 설정입니다.
    proxy_buffer_size               128k;
    proxy_buffers                   4 256k;
    proxy_busy_buffers_size         256k;

    # 502 에러를 없애기 위한 fastcgi 버퍼 관련 설정입니다.
    fastcgi_buffering               on;
    fastcgi_buffer_size             16k;
    fastcgi_buffers                 16 16k;

    # 최대 timeout 설정입니다.
    fastcgi_connect_timeout         600s;
    fastcgi_send_timeout            600s;
    fastcgi_read_timeout            600s;
}
```

 위와 같이 설정해준다 !



2. PHP 설정

```ini
max_execution_time = 120
max_input_time = 60
max_input_vars = 10000
memory_limit = 128M
```



3. 혹시 이래도 해결이 안된다면 php-fpm 설정 

```ini
pm = dynamic
pm.max_children = 9
pm.start_servers = 3
pm.min_spare_servers = 2
pm.max_spare_servers = 4
pm.max_requests = 500
```

이와 같이 변경해준다 !

참고로 이 셋팅은 동시접속자 수 2000명 이상의 서버의 환경 설정을 참고하여 셋팅한거임 !

