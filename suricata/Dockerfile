FROM alpine:latest

# USER suricata
# WORKDIR /tmp

RUN sudo 

RUN echo "https://github.com/OISF/suricata/archive/refs/tags/suricata-${SURICATA_VERSION}.tar.gz"

RUN curl -fL -o /tmp/suricata.tar.gz "https://github.com/OISF/suricata/archive/refs/tags/suricata-${SURICATA_VERSION}.tar.gz"
RUN mkdir /tmp/suricata && tar xzvf /tmp/suricata.tar.gz -C /tmp/suricata --strip-components 1
RUN cd /tmp/suricata && ./scripts/bundle.sh && ./autogen.sh && ./configure && make -j8 && make install
# RUN chmod -R 755 /tmp/suricata && chown -R suricata:suricata /tmp/suricata 



