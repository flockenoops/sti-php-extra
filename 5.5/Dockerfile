FROM openshift/php-55-centos7:latest

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

RUN yum clean all -y && \
    yum install https://www.softwarecollections.org/repos/remi/php55more/epel-7-x86_64/noarch/remi-php55more-epel-7-x86_64-1-2.noarch.rpm -y && \
    yum install -y --setopt=tsflags=nodocs glibc-common php55-php-pecl-redis php55-php-mcrypt && \
    yum clean all -y

# Getup bits
RUN chmod -R a+rwx /opt/rh/httpd24/root/etc/httpd/conf.d

COPY ./s2i/bin/ $STI_SCRIPTS_PATH

USER 1001
