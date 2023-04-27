FROM nginx:1.19-alpine

RUN set -x \
&&  apk add --no-cache \
      apache2-utils \
      curl \
      bash \
      netcat-openbsd \
      openssl \
&&  mkdir -p /etc/nginx/letsencrypt \
&&  curl -s https://raw.githubusercontent.com/certbot/certbot/master/certbot-nginx/certbot_nginx/_internal/tls_configs/options-ssl-nginx.conf > "/etc/nginx/letsencrypt/options-ssl-nginx.conf" \
&&  curl -s https://raw.githubusercontent.com/certbot/certbot/master/certbot/certbot/ssl-dhparams.pem > "/etc/nginx/letsencrypt/ssl-dhparams.pem" \
&&  chown -R nginx /etc/nginx/letsencrypt \
&&  rm -rf /var/cache/apk/* \
           /tmp/* \
           /var/tmp/*


RUN mv /docker-entrypoint.sh /old-entrypoint.sh
COPY docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["nginx", "-g", "daemon off;"]