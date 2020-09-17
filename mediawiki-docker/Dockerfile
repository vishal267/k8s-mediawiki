FROM centos:7
MAINTAINER  vishal
WORKDIR /var/www/html/
#RUN yum install -y epel-release yum-utils; yum install -y http://rpms.remirepo.net/enterprise/ remi-release-7.rpm ; yum-config-manager --enable remi-php74 ; yum install -y php php-gd php-mysql php-intl wget -y
RUN yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm; yum -y install https://rpms.remirepo.net/enterprise/remi-release-7.rpm; yum -y install yum-utils;yum-config-manager --enable remi-php74 ;  yum update -y ;  yum install -y mysql  php php-gd php-mysql php-intl php-mbstring php-xml wget -y
RUN set -x; \
    cd /var/www/html \
    && curl -fSL "https://releases.wikimedia.org/mediawiki/1.34/mediawiki-1.34.2.tar.gz" -o mediawiki.tar.gz \
    && tar -xz --strip-components=1 -f mediawiki.tar.gz \
    && rm -f mediawiki.tar.gz 
RUN chown -R apache:apache /var/www/html/

EXPOSE 80

ADD run-httpd.sh /run-httpd.sh
ADD docker-entrypoint.sh /entrypoint.sh
RUN chmod -v +x /run-httpd.sh
RUN chmod -v +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
CMD ["/run-httpd.sh"]
