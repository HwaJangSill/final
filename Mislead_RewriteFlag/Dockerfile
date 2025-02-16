# 베이스 이미지로 PHP와 Apache가 포함된 이미지를 사용
FROM php:8.0-apache

WORKDIR /var/www/html/uploads

# exploit 파일 업로드
COPY uploads .

# 소유자 변경
RUN chown -R www-data:www-data /var/www/html/

# Apache 설정 파일 적용
COPY custom.conf /etc/apache2/sites-available/000-default.conf

# rewrite 모듈 활성화
RUN a2enmod rewrite

# Apache 서버가 80번 포트에서 요청을 처리하도록 설정
EXPOSE 80

# Apache 서버 실행
CMD ["apache2-foreground"]