FROM buildpack-deps

RUN git clone https://github.com/tatsuhiro-t/nghttp2 \
    && cd nghttp2 \
    && autoreconf -i \
    && automake \
    && autoconf \
    && ./configure \
    && make

WORKDIR /nghttp2/src    
ENTRYPOINT ["./nghttpd","--no-tls"]
