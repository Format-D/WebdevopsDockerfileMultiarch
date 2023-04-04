#+++++++++++++++++++++++++++++++++++++++
# Dockerfile for webdevops/toolbox:latest
#    -- automatically generated  --
#+++++++++++++++++++++++++++++++++++++++

FROM alpine:latest
ARG TARGETPLATFORM
RUN apk add --no-cache \
        ca-certificates \
        openssl \
        curl \
        bash \
        sed \
        wget \
        zip \
        unzip \
        bzip2 \
        p7zip \
        drill \
        ldns \
        openssh-client \
        rsync \
        git \
        gnupg \
    && mkdir -p \
            /baselayout/sbin \
            /baselayout/usr/local/bin \
        # Baselayout scripts
        && wget -O /tmp/baselayout-install.sh https://raw.githubusercontent.com/webdevops/Docker-Image-Baselayout/master/install.sh \
        && sh /tmp/baselayout-install.sh /baselayout \
        ## Install go-replace \
    && if [ "$TARGETPLATFORM" = "linux/arm64" ]; then GO_REPLACE="go-replace.linux.arm64"; else GO_REPLACE="go-replace.linux.amd64"; fi \
    && wget -O "/baselayout/usr/local/bin/go-replace" "https://github.com/webdevops/go-replace/releases/download/22.10.0/${GO_REPLACE}" \
    && chmod +x "/baselayout/usr/local/bin/go-replace" \
    && "/baselayout/usr/local/bin/go-replace" --version \
        && ln -s /baselayout/usr/local/bin/go-replace /usr/local/bin/ \
        # Install gosu \
    && if [ "$TARGETPLATFORM" = "linux/arm64" ]; then ARCH="arm64"; else ARCH="amd64"; fi \
    && wget -O "/baselayout/sbin/gosu" "https://github.com/tianon/gosu/releases/download/1.16/gosu-${ARCH}" \
    && wget -O "/tmp/gosu.asc" "https://github.com/tianon/gosu/releases/download/1.16/gosu-${ARCH}.asc" \
    && export GNUPGHOME="$(mktemp -d)" \
    && gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
    && gpg --batch --verify /tmp/gosu.asc "/baselayout/sbin/gosu" \
    && rm -rf "$GNUPGHOME" /tmp/gosu.asc \
    && chmod +x "/baselayout/sbin/gosu" \
    && "/baselayout/sbin/gosu" nobody true
