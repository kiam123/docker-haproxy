FROM server_base


RUN apt-get -qqy update \
  && apt-get -qqy --no-install-recommends install \
    nginx \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/*


#======================================
# Add script
#======================================
COPY start_nginx.sh /opt/bin/

#======================================
# Add Supervisor configuration file
#======================================
COPY nginx_service.conf /etc/supervisor/conf.d/


#======================================
# Add nginx configuration
#======================================
COPY default /etc/nginx/sites-enabled