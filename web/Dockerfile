FROM server_base


RUN apt-get -qqy update \
  && apt-get -qqy --no-install-recommends install \
    nginx \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/*

#======================================
# Add Node web
#======================================
COPY index.nginx-debian1 index.nginx-debian2 /


#======================================
# Add script
#======================================
COPY start_nginx.sh genera_web.sh /opt/bin/
RUN chmod +x /opt/bin/genera_web.sh

#======================================
# Add Supervisor configuration file
#======================================
COPY nginx_service.conf genera_service.conf /etc/supervisor/conf.d/