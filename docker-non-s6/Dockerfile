FROM alpine:latest

RUN apk add --no-cache ca-certificates

COPY bin/hbbs /usr/bin/hbbs
COPY bin/hbbr /usr/bin/hbbr
COPY entrypoint.sh /usr/bin/entrypoint.sh

RUN chmod a+x /usr/bin/hbbs /usr/bin/hbbr /usr/bin/entrypoint.sh

EXPOSE 31114 31115 31116 31116/udp 31117 31118 31119

WORKDIR /data
VOLUME /data

HEALTHCHECK --interval=10s --timeout=5s \
  CMD test "$(cat /proc/1/comm)" = hbbs || test "$(cat /proc/1/comm)" = hbbr || exit 1

ENTRYPOINT ["/usr/bin/entrypoint.sh"]
CMD ["hbbs"]
