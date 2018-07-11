FROM golang:alpine as builder
 
RUN	apk add --no-cache \
	bash \
	ca-certificates \
	git \
	make \
        curl \
	wget \
	unzip \
	zip

RUN wget https://releases.hashicorp.com/vault/0.10.3/vault_0.10.3_linux_amd64.zip \
    && unzip vault_0.10.3_linux_amd64.zi \
    && mv vault /usr/bin \
    && rm vault_0.10.3_linux_amd64.zi
    
    
RUN curl -sSL https://github.com/openfaas/faas/releases/download/0.8.0/fwatchdog > /usr/bin/fwatchdog \
    && chmod +x /usr/bin/fwatchdog 

# Populate example here - i.e. "cat", "sha512sum" or "node index.js"
ENV fprocess="xargs terraform"
# Set to true to see request in function logs
ENV write_debug="false"

HEALTHCHECK --interval=5s CMD [ -e /tmp/.lock ] || exit 1
CMD [ "fwatchdog" ]
