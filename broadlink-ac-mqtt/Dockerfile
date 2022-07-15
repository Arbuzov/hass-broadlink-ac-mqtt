ARG BUILD_FROM
FROM $BUILD_FROM

COPY rootfs /

RUN apk add --no-cache gcc g++ make rust cargo libffi-dev openssl-dev \
    && pip3 install --no-cache-dir -U \
    paho-mqtt \
    parser-module \
    pyyaml \
    pycrypto \
    && cd /usr/share \
    && wget -c https://github.com/liaan/broadlink_ac_mqtt/archive/refs/tags/1.2.1b.tar.gz -O - | tar -xz \
    && chmod a+x /etc/services.d/broadlink-ac-mqtt/*
    