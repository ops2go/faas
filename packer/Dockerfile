FROM alpine:3.7
 
RUN	apk add --no-cache \
	bash \
	ca-certificates \
	git \
	make \
    curl \
	wget \
	unzip \
	zip

RUN wget https://releases.hashicorp.com/packer/1.2.4/packer_1.2.4_linux_amd64.zip \
    && unzip packer_1.2.4_linux_amd64.zip \
    && mv packer /usr/bin/packer \
    && rm packer_1.2.4_linux_amd64.zip
    
    
RUN curl -sSL https://github.com/openfaas/faas/releases/download/0.8.0/fwatchdog > /usr/bin/fwatchdog \
    && chmod +x /usr/bin/fwatchdog 

# Populate example here - i.e. "cat", "sha512sum" or "node index.js"
ENV fprocess="xargs packer"
# Set to true to see request in function logs
ENV write_debug="false"

HEALTHCHECK --interval=5s CMD [ -e /tmp/.lock ] || exit 1
CMD [ "fwatchdog" ]
