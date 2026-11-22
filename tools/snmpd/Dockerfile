# net-snmp's snmpd as the reference agent for integration tests and
# benchmarks. Usage:
#   docker build -t snmpify-snmpd tools/snmpd
#   docker run -d --rm --name snmpify-snmpd -p 127.0.0.1:1161:161/udp snmpify-snmpd
#   SNMPIFY_AGENT=127.0.0.1:1161 cargo test --test netsnmp
FROM ubuntu:26.04@sha256:d66b366dac61b575bee2aef07e9c26e8070096fbe84a3d4d3eb0da069b5d76db
RUN apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends snmpd snmp \
 && rm -rf /var/lib/apt/lists/*
COPY snmpd.conf /etc/snmp/snmpd.conf
EXPOSE 161/udp
# -f: foreground, -Lo: log to stdout, -C: only our config file
# No MIB files are installed (Debian ships them separately); everything is numeric.
ENV MIBS=""
ENTRYPOINT ["/usr/sbin/snmpd", "-f", "-Lo", "-C", "-c", "/etc/snmp/snmpd.conf"]
