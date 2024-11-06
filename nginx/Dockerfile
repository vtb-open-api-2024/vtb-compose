FROM debian:buster-slim

# Обновление пакетов и установка необходимых зависимостей
RUN apt-get update && \
    apt-get install -y \
    libssl-dev \
    wget build-essential libpcre3-dev zlib1g-dev

# Загрузка и распаковка исходного кода NGINX
RUN wget http://nginx.org/download/nginx-1.20.1.tar.gz && \
    tar -zxvf nginx-1.20.1.tar.gz && \
    cd nginx-1.20.1

# Конфигурация и сборка NGINX с модулем http_sub
RUN cd nginx-1.20.1 && \
    ./configure --with-http_sub_module  \
    --with-http_ssl_module && \
    make && \
    make install

# Очистка временных файлов
RUN rm -rf nginx-1.20.1.tar.gz nginx-1.20.1

# Копирование конфигурационных файлов
COPY nginx.conf       /usr/local/nginx/conf/nginx.conf
COPY common.conf      /usr/local/nginx/conf/common.conf
COPY proxy-ssl.conf   /usr/local/nginx/conf.d/proxy-ssl.conf
COPY key.pem          /usr/local/ssl/key.pem 
COPY chain.pem        /usr/local/ssl/chain.pem
 
# Открытие порта
EXPOSE 80
EXPOSE 443
# Запуск NGINX
CMD ["/usr/local/nginx/sbin/nginx", "-g", "daemon off;"]