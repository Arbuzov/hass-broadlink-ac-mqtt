ARG BUILD_FROM
FROM $BUILD_FROM

RUN apt-get install -y python3 python3-pip

RUN pip install --no-cache-dir -U \
    paho-mqtt \
    pyyaml \
    pycrypto