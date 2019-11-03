#FROM registry.redhat.io/openshift3/mediawiki:latest
FROM mediawiki:latest
# user must be in group apache
USER root       
RUN usermod -a -G apache www-data 
USER www-data
