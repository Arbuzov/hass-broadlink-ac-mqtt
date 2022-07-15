ARG BUILD_FROM
FROM $BUILD_FROM

COPY rootfs /

RUN apk add --no-cache python3-pycryptodome python3-yaml python3-paho-mqtt \
    && pip3 install --no-cache-dir -U \
    parser-module \
    && cd /usr/share \
    && wget -c https://github.com/liaan/broadlink_ac_mqtt/archive/refs/tags/1.2.1b.tar.gz -O - | tar -xz \
    && chmod a+x /etc/services.d/broadlink-ac-mqtt/*
    