FROM alpine:edge

RUN apk --no-cache add tini git \
    && apk --no-cache add --virtual devs tar curl && rm -rf /var/cache/apk/*

#Install Caddy Server, and All Middleware
RUN curl "https://caddyserver.com/download/linux/amd64?plugins=http.cors,http.git,http.hugo,http.ipfilter,http.jwt,http.mailout,http.prometheus,http.realip,http.upload&license=personal" \
    | tar --no-same-owner -C /usr/bin/ -xz caddy

#Remove build devs
RUN apk del devs

#Copy over a default Caddyfile
COPY ./Caddyfile /etc/Caddyfile
#Copy over tls files
COPY ./cert.pem /root/cert.pem
COPY ./key.pem /root/key.pem

ENTRYPOINT ["/sbin/tini"]

CMD ["caddy", "--conf", "/etc/Caddyfile"]
