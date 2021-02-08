FROM server_base


RUN apt-get -qqy update \
  && apt-get -qqy --no-install-recommends install \
    haproxy \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/*

#======================================
# Add haproxy configuration file
#======================================
COPY haproxy.cfg /etc/haproxy/


#======================================
# Add script
#======================================
COPY start_haproxy.sh /opt/bin/

#======================================
# Add Supervisor configuration file
#======================================
COPY haproxy_service.conf /etc/supervisor/conf.d/


#======================================
# Add nginx configuration
#======================================
COPY default /etc/nginx/sites-enabled

#======================================
# Add keepalived configuration
#======================================
COPY keepalived.conf /etc/keepalived/

EXPOSE 9000