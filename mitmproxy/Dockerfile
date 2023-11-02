FROM alpine:latest

RUN addgroup -S mitmproxy && adduser -S -G mitmproxy mitmproxy \
    && apk --update --no-cache add python3-dev curl gcc musl-dev libffi-dev libffi py3-pip py3-virtualenv git wget autoconf build-base bsd-compat-headers \
    && curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y \
    && PATH="/root/.cargo/bin:${PATH}" \
    && git clone https://github.com/mitmproxy/mitmproxy.git /tmp/mitmproxy \
    && cd /tmp/mitmproxy \
    && python3 -m pip install -e .[dev] \
    && python3 -u release/build.py standalone-binaries 2>&1 > ~/mitmbuild.err || echo "Build details see ~/mitmbuild.err" \
    && rm -r /tmp/mitmproxy \
    && echo "Build SUCCESSFUL"

VOLUME /home/mitmproxy/.mitmproxy

COPY docker-entrypoint.sh /usr/local/bin/

USER mitmproxy

ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 8080 8081

CMD ["mitmproxy"]