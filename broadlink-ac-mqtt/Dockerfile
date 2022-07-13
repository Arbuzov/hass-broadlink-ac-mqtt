ARG BUILD_FROM
FROM $BUILD_FROM

RUN apk add --no-cache gcc python-dev



RUN pip install --no-cache-dir -U \
    paho-mqtt \
    pyyaml \
    pycrypto