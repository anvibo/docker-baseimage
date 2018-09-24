FROM ubuntu:14.04

ENV DEBIAN_FRONTEND noninteractive

ADD install-clean /usr/bin/install-clean
RUN chmod 0755 "/usr/bin/install-clean"

RUN install-clean wget

RUN wget --no-check-certificate -O /usr/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.2/dumb-init_1.2.2_amd64
RUN chmod +x /usr/bin/dumb-init

#RUN install-clean dumb-init

ENTRYPOINT ["/usr/bin/dumb-init", "--"]
