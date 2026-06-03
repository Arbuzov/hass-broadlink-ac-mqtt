ARG BUILD_FROM
FROM $BUILD_FROM

COPY rootfs /

COPY patches /tmp/patches

RUN apk add --no-cache gcc g++ make libffi-dev openssl-dev patch \
    && pip3 install --no-cache-dir -U \
    paho-mqtt \
    pyyaml \
    cryptography~=42.0 \
    && cd /usr/share \
    && wget -c https://github.com/Arbuzov/broadlink_ac_mqtt/archive/refs/tags/1.2.3.tar.gz -O - | tar -xz \
    && patch -d /usr/share/broadlink_ac_mqtt-1.2.3 -p1 < /tmp/patches/skip-unreachable-devices.patch \
    && chmod a+x /etc/services.d/broadlink-ac-mqtt/*
