ARG BUILD_FROM
FROM $BUILD_FROM

RUN apk add --no-cache gcc build-essential



RUN pip install --no-cache-dir -U \
    paho-mqtt \
    pyyaml \
    pycrypto