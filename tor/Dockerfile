FROM alpine:latest

RUN apk update \
    && apk --no-cache add tor

COPY torrc /etc/tor/

EXPOSE 9050/tcp 9051/tcp

HEALTHCHECK --interval=120s --timeout=15s --start-period=120s --retries=2 CMD curl --fail -x socks5://127.0.0.1:9050 -s 'http://httpbin.org/ip' -k > /dev/null && echo "HealthCheck succeeded..." || exit 1

USER tor

CMD ["tor"]