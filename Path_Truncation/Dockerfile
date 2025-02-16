FROM httpd:2.4.59

# Apache 설정 파일 추가 (기존 httpd.conf를 덮어쓰지 않음)
COPY custom.conf /usr/local/apache2/conf/extra/custom.conf

# 이미지 업로드하기
COPY ./fruits/apple.png /usr/local/apache2/htdocs/fruits/apple/1.png
COPY ./fruits/pear.png /usr/local/apache2/htdocs/fruits/pear/1.png
COPY ./fruits/banana.png /usr/local/apache2/htdocs/fruits/banana/1.png
COPY ./fruits/reality.jpg /usr/local/apache2/htdocs/fruits/reality/apple.jpg

# httpd.conf에 Include 추가
RUN echo "Include conf/extra/custom.conf" >> /usr/local/apache2/conf/httpd.conf

# mod_rewrite 활성화 (이미 로드되어 있으면 무시)
RUN sed -i '/LoadModule rewrite_module/s/^#//g' /usr/local/apache2/conf/httpd.conf

EXPOSE 80
CMD ["httpd", "-D", "FOREGROUND"]