#FROM registry.redhat.io/openshift3/mediawiki:latest
FROM docker-registry.default.svc.cluster.local:5000/mediawiki/mediawiki:latest
# user must be in group apache
RUN usermod -a -G apache www-data