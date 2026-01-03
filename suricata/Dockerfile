FROM ubuntu:latest As base

RUN apt update -y && apt upgrade -y
RUN apt-get -y install vim python3-pip
RUN rm /usr/lib/python3.12/EXTERNALLY-MANAGED 

# From suricata documentation
RUN apt-get install -y libcap2-bin build-essential git libjansson-dev libpcap-dev \
                libpcre2-dev libtool libyaml-dev make pkg-config zlib1g-dev 
RUN apt-get install -y autoconf automake build-essential ccache clang curl git \
                gosu jq libbpf-dev libcap-ng0 libcap-ng-dev libelf-dev \
                libevent-dev libgeoip-dev libhiredis-dev libjansson-dev \
                liblua5.1-dev libmagic-dev libnet1-dev libpcap-dev \
                libpcre2-dev libtool libyaml-0-2 libyaml-dev m4 make \
                pkg-config python3 python3-dev python3-yaml sudo zlib1g \
                zlib1g-dev libhtp2
RUN apt-get install -y libnetfilter-queue-dev libnetfilter-queue1  \
                libnetfilter-log-dev libnetfilter-log1      \
                libnfnetlink-dev libnfnetlink0 rustc

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | bash -s -- -y 
RUN /bin/bash -c "source $HOME/.cargo/env" 
RUN apt install -y cargo cbindgen

FROM base As suricata
# use build arg here instead of base (multi stage dockerfile)
ARG SURICATA_VERSION

# fetch suricata binaries
RUN curl -fL -o /tmp/suricata.tar.gz "https://github.com/OISF/suricata/archive/refs/tags/suricata-${SURICATA_VERSION}.tar.gz"
RUN mkdir /tmp/suricata && tar xzvf /tmp/suricata.tar.gz -C /tmp/suricata --strip-components 1
RUN cd /tmp/suricata && ./scripts/bundle.sh && ./autogen.sh && ./configure && make -j8 && make install-full
RUN rm -rf /tmp/suricata
# USER suricata
WORKDIR /usr/local/bin

#Test if suricata works
RUN suricata -V || (echo "Suricata was not installed successfully! Check correctness of dependencies!" && exit 1)

CMD ["tail", "-f", "/dev/null"]

