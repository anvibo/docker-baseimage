FROM anvibo/baseimage:18.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -q update && apt-get -qy install --no-install-recommends dumb-init fuse \
    && apt-get -qy autoremove \
    && apt-get clean \
    && rm -r /var/lib/apt/lists/*

RUN apt-get -q update && apt-get -qy install wget \
    && wget https://github.com/GoogleCloudPlatform/gcsfuse/releases/download/v0.23.0/gcsfuse_0.23.0_amd64.deb \
    && dpkg --install gcsfuse_0.23.0_amd64.deb \
    && rm -rfv gcsfuse_0.23.0_amd64.deb \
    && apt-get purge -qy wget \
    && apt-get -qy autoremove --purge \
    && apt-get clean \
    && rm -r /var/lib/apt/lists/*

ENTRYPOINT ["/usr/bin/dumb-init", "--"]