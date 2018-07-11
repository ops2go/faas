FROM ubuntu:16.04

RUN apt-get update && apt-get install -y \
	software-properties-common \
	--no-install-recommends && \
	add-apt-repository ppa:wireshark-dev/stable && \
	apt-get update && \
	apt-get install -y \
    curl \
	wireshark \
	&& rm -rf /var/lib/apt/lists/
    
RUN curl -sSL https://github.com/openfaas/faas/releases/download/0.8.0/fwatchdog > /usr/bin/fwatchdog \
    && chmod +x /usr/bin/fwatchdog 

RUN setcap 'CAP_NET_RAW+eip CAP_NET_ADMIN+eip' /usr/bin/dumpcap

ENV fprocess="xargs wireshark"
# Set to true to see request in function logs
ENV write_debug="false"

HEALTHCHECK --interval=5s CMD [ -e /tmp/.lock ] || exit 1
CMD [ "fwatchdog" ]
