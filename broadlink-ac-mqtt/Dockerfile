ARG BUILD_FROM
FROM $BUILD_FROM

## Upstream 1.2.4 plus the unmapped-fan-speed fix, pinned by commit rather than
## by tag: a tag can be moved, and then the same add-on version would build
## different code with nothing in this repository to show for it. Applying the
## patches used to catch that by accident, because their context stopped
## matching. Bump together with config.yaml's version.
ARG UPSTREAM_COMMIT=b86c16b5c17b5a8a3350684e9f1efeec892ef3f8

COPY rootfs /

## No build toolchain: every requirement resolves to a musllinux wheel on both
## architectures, from the Home Assistant wheel index the base image points pip
## at. Should a future release stop shipping one, pip fails loudly here and the
## toolchain comes back.
##
## The cryptography bound is ours, not upstream's, which floats it unbounded.
## ac_db.py still passes the backend= argument to Cipher() and imports
## default_backend, deprecated since cryptography 3.1 -- so an unbounded major
## can break this image on a rebuild with no change to any pinned source. Drop
## the bound once upstream stops naming a backend; the argument is optional.
RUN mkdir -p /usr/share/broadlink_ac_mqtt \
    && wget -qO- "https://github.com/Arbuzov/broadlink_ac_mqtt/archive/${UPSTREAM_COMMIT}.tar.gz" \
       | tar -xz -C /usr/share/broadlink_ac_mqtt --strip-components=1 \
    && pip3 install --no-cache-dir -r /usr/share/broadlink_ac_mqtt/requirements.txt "cryptography<50" \
    && chmod a+x /etc/services.d/broadlink-ac-mqtt/*
