# FROM mediawiki:latest
FROM openshift/ose-base:rhel7
ENV BUILD_VERSION=v3.11.153 BUILD_RELEASE=2
ENV BUILD_VERSION=v3.11.152 BUILD_RELEASE=3
ENV BUILD_VERSION=v3.11.153
ENV BUILD_VERSION=v3.11.153 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.152
ENV BUILD_VERSION=v3.11.152 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.151 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.150 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.149 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.148 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.147 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.146
ENV BUILD_VERSION=v3.9.101
ENV BUILD_VERSION=v3.11.146
ENV BUILD_VERSION=v3.11.146
ENV BUILD_VERSION=v3.11.146 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.145 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.144 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.143 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.142 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.141
ENV BUILD_VERSION=v3.11.141
ENV BUILD_VERSION=v3.11.141 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.140 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.139 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.136 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.135
ENV BUILD_VERSION=v3.11.135 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.134 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.133 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.132 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.131 BUILD_RELEASE=1
ENV BUILD_VERSION=v3.11.130 BUILD_RELEASE=1
ENV USER_NAME=www-data \
    USER_UID=1001 \
    BASE_DIR=/home/www-data \
    PHP=71 \
    HOME=${BASE_DIR}
RUN yum -y install mediawiki httpd ImageMagick git rh-php${PHP}* mediawiki-container-scripts \
  && yum clean all \
  && mkdir -p ${BASE_DIR} ${BASE_DIR}/etc \
  && useradd -u ${USER_UID} -r -g 0 -M -d ${BASE_DIR} -b ${BASE_DIR} -s /sbin/nologin -c "www-data user" ${USER_NAME} \
  && mkdir -p ${BASE_DIR}/httpd/{logs,run,html,conf} \
  && cp /opt/rh/httpd24/root/etc/httpd/conf/{httpd.conf,magic} ${BASE_DIR}/httpd/conf \
  && cp -R /usr/share/mediawiki ${BASE_DIR}/httpd/mediawiki \
  && mkdir ${BASE_DIR}/tmp \
  && cp -R /opt/rh/httpd24/root/etc/httpd/conf.modules.d ${BASE_DIR}/httpd/conf.modules.d \
  && cp -R /opt/rh/httpd24/root/etc/httpd/conf.d ${BASE_DIR}/httpd/conf.d \
  && chown -R ${USER_NAME}:0 ${BASE_DIR}/httpd \
  && mkdir -p ${BASE_DIR}/httpd/mediawiki/{cache,images} \
  && chmod 777 ${BASE_DIR}/httpd/mediawiki/{cache,images} \
  && chmod 777 /var/opt/rh/rh-php${PHP}/run/php-fpm \
  && chmod 777 ${BASE_DIR}/tmp \
  && chmod -R g+rw ${BASE_DIR} /etc/passwd \
  && ln -sf /home/www-data /opt/rh/httpd24/root/home/www-data \
  && cp /usr/share/mediawiki-container-scripts/mediawiki.conf.example           ${BASE_DIR}/httpd/conf.d/mediawiki.conf \
  && sed -i -e 's/Listen 80/Listen 8080/'               -e "s@ServerRoot \"/etc/httpd\"@ServerRoot ${BASE_DIR}/httpd@"               -e 's@DocumentRoot "/var/www/.*"@DocumentRoot mediawiki/@'               -e "s@/var/www@${BASE_DIR}/httpd@"               -e "s@logs/error_log@${BASE_DIR}/httpd/logs/error_log@"               -e "s@logs/access_log@${BASE_DIR}/httpd/logs/access_log@" ${BASE_DIR}/httpd/conf/httpd.conf \
  && echo "PidFile /home/www-data/httpd/run/httpd.pid" >> ${BASE_DIR}/httpd/conf/httpd.conf \
  && echo "DefaultRuntimeDir /home/www-data/httpd/run/" >> ${BASE_DIR}/httpd/conf/httpd.conf \
  && rm -rf ${BASE_DIR}/httpd/modules \
  && ln -sf /opt/rh/httpd24/root/usr/lib64/httpd/modules/ ${BASE_DIR}/httpd/modules \
  && rm -rf /home/www-data/httpd/html \
  && ln -sf /home/www-data/httpd/mediawiki /home/www-data/httpd/html \
  && sed "s@${USER_NAME}:x:${USER_UID}:@${USER_NAME}:x:\${USER_ID}:@g" /etc/passwd > ${BASE_DIR}/etc/passwd.template
EXPOSE 8080
USER ${USER_UID}
ENTRYPOINT ["entrypoint.sh"]
LABEL \
        com.redhat.component="openshift-enterprise-mediawiki-container" \
        version="v3.11.153" \
        vendor="Red Hat" \
        name="openshift3/mediawiki" \
        License="GPLv2+" \
        release="2"
