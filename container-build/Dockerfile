# Use the httpd-parent image as base
FROM quay.io/redhattraining/httpd-parent

LABEL io.openshift.expose-services="8080:http" \
      io.k8s.description="Teste ONBUILD Apache" \
      io.k8s.display-name="Apache Server" \
      io.openshift.tags="apache,httpd"

EXPOSE 8080

ENV APP_DIRS /var/log/httpd/ /var/run/httpd/

RUN sed -i "s/Listen 80/Listen 8080/g" /etc/httpd/conf/httpd.conf \
 && chgrp -R 0 $APP_DIRS \
 && chmod -R g=u $APP_DIRS

USER 1001

