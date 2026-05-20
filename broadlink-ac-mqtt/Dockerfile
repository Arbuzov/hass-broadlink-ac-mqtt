ARG BUILD_FROM
FROM $BUILD_FROM

COPY rootfs /

RUN apk add --no-cache gcc g++ make \
    && pip3 install --no-cache-dir -U \
    paho-mqtt \
    pyyaml \
    pycrypto \
    && cd /usr/share \
    && wget -c https://github.com/liaan/broadlink_ac_mqtt/archive/refs/tags/1.2.1b.tar.gz -O - | tar -xz \
    && sed -i 's/console\.setLevel(logging\.INFO)/console.setLevel(logging.DEBUG if os.environ.get("BROADLINK_DEBUG") else logging.INFO)/' /usr/share/broadlink_ac_mqtt-1.2.1b/monitor.py \
    && chmod a+x /etc/services.d/broadlink-ac-mqtt/*
    