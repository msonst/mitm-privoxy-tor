FROM alpine:latest

RUN apk update \
    && apk --no-cache add mitmproxy

EXPOSE 8080/tcp 

HEALTHCHECK --interval=120s --timeout=15s --start-period=120s --retries=2 CMD curl --fail -x http://127.0.0.1:8080 -s 'http://httpbin.org/ip' -k > /dev/null && echo "HealthCheck succeeded..." || exit 1

#USER privoxy

#CMD ["privoxy", "--no-daemon", "/etc/privoxy/config"]