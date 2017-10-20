FROM nextcloud:12.0.3-fpm
ARG BUILD_ARCH

COPY qemu-arm-static /usr/bin/qemu-arm-static
COPY qemu-aarch64-static /usr/bin/qemu-aarch64-static

RUN if [ "$BUILD_ARCH" = "armhf" ]; then rm /usr/bin/qemu-aarch64-static;\
    elif [ "$BUILD_ARCH" = "aarch64" ]; then rm /usr/bin/qemu-arm-static;\
    else\
    rm /usr/bin/qemu-aarch64-static;\
    rm /usr/bin/qemu-arm-static;\
    fi

RUN apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    		jq \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* ~/.cache


COPY run_addon.sh /
RUN chmod a+x /run_addon.sh

ENTRYPOINT [ "/run_addon.sh" ]