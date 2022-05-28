FROM ubuntu:20.04

# Customizeable arguments.
ARG TIME_ZONE_AREA
ARG TIME_ZONE_LOCATION
ARG USER
ARG FME_DESKTOP_BUILD_VERSION

## Preseed time zone data, update package index and install required packages.
ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true
RUN truncate -s0 /tmp/preseed.cfg && \
    echo "tzdata tzdata/Areas select ${TIME_ZONE_AREA}" >> /tmp/preseed.cfg && \
    echo "tzdata tzdata/Zones/${TIME_ZONE_AREA} select ${TIME_ZONE_LOCATION}" >> /tmp/preseed.cfg && \
    debconf-set-selections /tmp/preseed.cfg && \
    rm -f /etc/timezone /etc/localtime && \
    apt-get update && \
    apt-get install -y tzdata libboost-chrono1.67.0 libboost-filesystem1.67.0 libboost-iostreams1.67.0 \
                       libboost-locale1.67.0 libboost-regex1.67.0-icu66 libboost-system1.67.0 \
                       libboost-thread1.67.0 libde265-0 libexpat1 libfreetype6 libgl1 libglib2.0-0 \
                       libgomp1 libicu66 libjpeg8 libltdl7 libmpfr6 libnghttp2-14 libodbc1 libpng16-16 \
                       libpq5 libpython3.8 libqt5concurrent5 libqt5core5a libqt5gui5 libqt5network5 \
                       libqt5opengl5 libqt5printsupport5 libqt5sql5 libqt5svg5 libqt5webenginecore5 \
                       libqt5webenginewidgets5 libqt5widgets5 libqt5xml5 libqt5xmlpatterns5 libsqlite3-0 \
                       libssh2-1 libssl1.1 libtcl8.6 libtcmalloc-minimal4 libtiff5 libx11-6 libxml2 \
                       libxt6 uuid-runtime python3-pip python3-pil python3-certifi python3-cryptography \
                       python3-lxml python3-matplotlib python3-numpy python3-bs4 gpsbabel \
                       openjdk-11-jre-headless tcllib graphviz curl
ENV DEBIAN_FRONTEND readline
ENV DEBCONF_NONINTERACTIVE_SEEN false

# Configurable environment variable values.
ENV HOME_PATH "/home/${USER}"
ENV FME_DESKTOP_DEB_FILE_NAME "fme-desktop-2021_2021.${FME_DESKTOP_BUILD_VERSION}~ubuntu.20.04_amd64.deb"

# Install FME Desktop.
WORKDIR /root
RUN curl -O https://downloads.safe.com/fme/2021/${FME_DESKTOP_DEB_FILE_NAME} && \
    dpkg -i ${FME_DESKTOP_DEB_FILE_NAME} && \
    rm -f ${FME_DESKTOP_DEB_FILE_NAME}

# Setup runtime user account.
RUN groupadd -g 1000 ${USER} && useradd -mru 1000 -g ${USER} ${USER}
USER ${USER}
WORKDIR ${HOME_PATH}

# Start FME Workbench.
CMD ["/bin/sh", "-c", "/opt/fme-desktop-2021/fmeworkbench"]