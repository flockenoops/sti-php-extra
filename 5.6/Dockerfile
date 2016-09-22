FROM centos/php-56-centos7:latest

USER root

#Upload AIM files
ADD aim/* /tmp/aim/

#Run AIM tasks
RUN unalias cp \
    mkdir /tmp/aim \
    mkdir /JavaBB \
    cp /tmp/aim/aimparms.sample /var/tmp/aimparms \
    rpm -i /tmp/aim/CARKaim-9.70.0.3.x86_64.rpm \
    cp /tmp/aim/JavaBB/* /JavaBB/ \
    yum install -y python-setuptools \
    easy_install supervisor

RUN yum install https://www.softwarecollections.org/en/scls/remi/php56more/epel-7-x86_64/download/remi-php56more-epel-7-x86_64.noarch.rpm -y && \
    yum install -y --setopt=tsflags=nodocs reinstall glibc-common \
    more-php56-php-pecl-redis more-php56-php-mcrypt && \
    yum clean all -y

# Getup bits
RUN chmod -R a+rwx /opt/rh/httpd24/root/etc/httpd/conf.d

COPY ./s2i/bin/ $STI_SCRIPTS_PATH

USER 1001
