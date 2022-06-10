FROM ubuntu:20.04

# Customizeable arguments.
ARG TIME_ZONE_AREA
ARG TIME_ZONE_LOCATION
ARG USER
ARG HOME=${HOME}
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
    apt-get install -y tzdata libc-bin desktop-file-utils hicolor-icon-theme shared-mime-info libpython3-dev \
                       libboost-chrono1.67.0 libboost-filesystem1.67.0 libboost-iostreams1.67.0 libboost-locale1.67.0 \
                       libboost-regex1.67.0 libboost-system1.67.0 libboost-thread1.67.0 libcfitsio8 libdbus-1-3 \
                       libde265-0 libegl1 libfontconfig1 libfreetype6 libgl1 libglx0 libgomp1 libgtk-3-0 libharfbuzz0b \
                       libice6 libjpeg8 libltdl7 libmpfr6 libnghttp2-14 libnspr4 libnss3 libodbc1 libopengl0 \
                       libpango-1.0-0 libpcre2-16-0 libpng16-16 libpq5 libsm6 libssh2-1 libtcl8.6 libtcmalloc-minimal4 \
                       libtiff5 libwebp6 libwebpdemux2 libwebpmux3 libx11-xcb1 libxcb-glx0 libxcb-icccm4 libxcb-image0 \
                       libxcb-keysyms1 libxcb-randr0 libxcb-render-util0 libxcb-render0 libxcb-shape0 libxcb-shm0 \
                       libxcb-sync1 libxcb-xfixes0 libxcb-xinput0 libxcb-xkb1 libxcomposite1 libxdamage1 libxfixes3 \
                       libxkbcommon-x11-0 libxkbcommon0 libxkbfile1 libxrandr2 libxshmfence1 libxt6 libxtst6 \
                       uuid-runtime python3-pip python3-pil python3-certifi python3-cryptography python3-lxml \
                       python3-matplotlib python3-numpy python3-bs4 gpsbabel openjdk-11-jre-headless tcllib graphviz \
                       curl
ENV DEBIAN_FRONTEND readline
ENV DEBCONF_NONINTERACTIVE_SEEN false

# Configurable environment variable values.
ENV FME_DESKTOP_DEB_FILE_NAME "fme-desktop-2022_2022.${FME_DESKTOP_BUILD_VERSION}~ubuntu.20.04_amd64.deb"

# Install FME Desktop.
WORKDIR /root
RUN curl -O https://downloads.safe.com/fme/2022/${FME_DESKTOP_DEB_FILE_NAME} && \
    dpkg -i ${FME_DESKTOP_DEB_FILE_NAME} && \
    rm -f ${FME_DESKTOP_DEB_FILE_NAME}

# Setup runtime user account.
RUN groupadd -g 1000 ${USER} && useradd -mru 1000 -g ${USER} ${USER}
USER ${USER}
WORKDIR ${HOME}

# Start FME Workbench.
CMD ["/bin/sh", "-c", "/opt/fme-desktop-2022/fmeworkbench"]