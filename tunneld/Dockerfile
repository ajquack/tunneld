FROM alpine

LABEL org.opencontainers.image.source=https://github.com/ajquack/tunneld
LABEL org.opencontainers.image.title=tunneld
LABEL org.opencontainers.image.url=https://github.com/ajquack/tunneld
LABEL org.opencontainers.image.version=latest

COPY . /usr/bin/

RUN apk add --no-cache iptables iproute2 py3-kubernetes

RUN echo "net.ipv4.ip_forward=1" > /etc/sysctl.conf \ 
    && touch /tmp/cron.log \
    && chmod +x /usr/bin/add-masquerade-to-services.py \
    && chmod +x /usr/bin/startup.sh \
    && echo '* * * * * python3 /usr/bin/add-masquerade-to-services.py >> /tmp/cron.log 2>&1' > /etc/crontabs/root 
    
ENTRYPOINT ["/usr/bin/startup.sh"]
