FROM httpd:2.4

ARG WEB_USER
ARG WEB_GROUP
ARG APACHE_ROOT_DIR

COPY httpd-vhosts.conf /usr/local/apache2/conf/extra/httpd-vhosts.conf
COPY httpd.conf /usr/local/apache2/conf/httpd.conf

RUN chgrp -R www-data /usr/local/apache2/conf/httpd.conf && \
    chgrp -R www-data /usr/local/apache2/conf/extra/httpd-vhosts.conf && \
    usermod -u 1000 www-data && \
    groupmod -g 1000 www-data && \
    chgrp -R www-data /usr/local/apache2

