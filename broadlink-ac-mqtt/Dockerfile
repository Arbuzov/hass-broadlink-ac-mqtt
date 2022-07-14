ARG BUILD_FROM
FROM $BUILD_FROM

RUN apk add --no-cache gcc g++ make



RUN pip install --no-cache-dir -U \
    paho-mqtt \
    pyyaml \
    pycrypto \
    && cd /usr/share \
    && wget -c https://github.com/liaan/broadlink_ac_mqtt/archive/refs/tags/1.2.1b.tar.gz -O - | tar -xz
    
COPY rootfs /
