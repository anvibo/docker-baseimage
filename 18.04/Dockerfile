FROM ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive

ADD install-clean /usr/bin/install-clean

RUN chmod 0755 "/usr/bin/install-clean"

RUN install-clean dumb-init

ENTRYPOINT ["/usr/bin/dumb-init", "--"]
