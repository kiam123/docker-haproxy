FROM server_base

ARG web_port=80
ARG stats_port=9000

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



EXPOSE ${web_port}
EXPOSE ${stats_port}
