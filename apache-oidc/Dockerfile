ARG BUILD_FROM
FROM ${BUILD_FROM}

RUN echo "https://dl-cdn.alpinelinux.org/alpine/edge/testing/" >> /etc/apk/repositories && \
    apk add --no-cache \
        apache2 apache2-proxy apache2-ssl \
        cjose curl jansson \
        autoconf automake build-base libtool wget \
        apache2-dev cjose-dev curl-dev pcre-dev && \
    curl -Ls https://api.github.com/repos/zmartzone/mod_auth_openidc/releases/latest | \
        grep -o -E "https://(.*).tar.gz" | xargs curl -L | tar xzvf - && \
    cd mod_auth_openidc-* && \
    ./configure && \
    make -j$(nproc) && \
    make install && \
    cd .. && \
    rm -rf mod_auth_openidc-* && \
    rm /etc/apache2/conf.d/info.conf /etc/apache2/conf.d/userdir.conf && \
    apk del apache2-dev cjose-dev curl-dev pcre-dev autoconf automake build-base wget libtool

COPY rootfs /
