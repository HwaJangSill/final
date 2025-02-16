# Apache HTTP Server 이미지를 베이스로 사용
FROM httpd:2.4.59

# Apache에서 PHP-FPM을 사용하기 위해 필요한 모듈 설치
RUN apt-get update && \
    apt-get install -y php-fpm && \
    apt-get clean

# mod_proxy, mod_proxy_fcgi 활성화 (이미 로드되어 있으면 무시)
RUN sed -i '/LoadModule proxy_module/s/^#//g' /usr/local/apache2/conf/httpd.conf \
&& sed -i '/LoadModule proxy_fcgi_module/s/^#//g' /usr/local/apache2/conf/httpd.conf

# Apache 서버 설정
COPY ./custom.conf /etc/apache2/sites-available/000-default.conf

# admin.php 파일 (인증 필요)
COPY ./admin.php /usr/local/apache2/htdocs/admin.php

# .htpasswd 생성
RUN htpasswd -b -c /etc/apache2/.htpasswd admin admin1234! \
    && chown www-data:www-data /etc/apache2/.htpasswd \ 
    && chmod 644 /etc/apache2/.htpasswd

# PHP-FPM 소켓 경로 설정
RUN echo "listen = /run/php/php8.2-fpm.sock" >> /etc/php/8.2/fpm/pool.d/www.conf

# 서버 설정 적용
RUN echo "Include /etc/apache2/conf-available/php8.2-fpm.conf" >> /usr/local/apache2/conf/httpd.conf \
    && echo "Include /etc/apache2/sites-available/000-default.conf" >> /usr/local/apache2/conf/httpd.conf

EXPOSE 80
CMD ["sh", "-c", "service php8.2-fpm start && httpd -D FOREGROUND"]
