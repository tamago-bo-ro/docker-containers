FROM centos:8

ARG APP_NAME

RUN dnf -y install https://rpms.remirepo.net/enterprise/remi-release-8.rpm && \
    dnf -y install httpd && \ 
    dnf -y module install php:remi-7.4 && \
    dnf -y install php-mbstring php-intl php-xml php-json php-pdo php-mysqlnd && \
    dnf -y install git && \
    dnf -y install zip unzip && \
    dnf -y update

RUN systemctl enable httpd

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
    
RUN composer config -g repos.packagist composer https://packagist.jp && \
    composer global require hirak/prestissimo && \
    cd ~ && yes | composer create-project --prefer-dist cakephp/app:4.* $APP_NAME

CMD ["/sbin/init"]
