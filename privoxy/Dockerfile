FROM alpine:latest

RUN apk update \
    && apk --no-cache add privoxy

#RUN addgroup -S privoxy && adduser -S privoxy -G privoxy

COPY config /etc/privoxy/
COPY user.filter /etc/privoxy/ 
COPY default.filter /etc/privoxy/ 
COPY match-all.action /etc/privoxy/ 
COPY default.action /etc/privoxy/ 
COPY user.action /etc/privoxy/ 

EXPOSE 8118/tcp 

HEALTHCHECK --interval=120s --timeout=15s --start-period=120s --retries=2 CMD curl --fail -x http://127.0.0.1:8118 -s 'http://httpbin.org/ip' -k > /dev/null && echo "HealthCheck succeeded..." || exit 1

USER privoxy

CMD ["privoxy", "--no-daemon", "/etc/privoxy/config"]