FROM golang:alpine as builder
MAINTAINER Jessica Frazelle <jess@linux.com>

ENV PATH /go/bin:/usr/local/go/bin:$PATH
ENV GOPATH /go

RUN	apk add --no-cache \
	bash \
	ca-certificates \
	git \
	make \
    curl \
	zip

ENV TERRAFORM_VERSION v0.11.7

RUN go get github.com/hashicorp/terraform

WORKDIR /go/src/github.com/hashicorp/terraform

RUN git checkout "${TERRAFORM_VERSION}"

# Install the vendor packages so stringer works.
# See: https://github.com/golang/go/issues/10249
RUN go install ./vendor/...

RUN XC_ARCH="amd64" XC_OS="linux" LD_FLAGS=" -extldflags -static" make bin \
	&& mv bin/terraform /usr/bin/terraform

FROM alpine:latest

COPY --from=builder /usr/bin/terraform /usr/bin/terraform
COPY --from=builder /etc/ssl/certs/ /etc/ssl/certs

RUN curl -sSL https://github.com/openfaas/faas/releases/download/0.8.0/fwatchdog > /usr/bin/fwatchdog \
    && chmod +x /usr/bin/fwatchdog 

# Populate example here - i.e. "cat", "sha512sum" or "node index.js"
ENV fprocess="xargs terraform"
# Set to true to see request in function logs
ENV write_debug="false"

HEALTHCHECK --interval=5s CMD [ -e /tmp/.lock ] || exit 1
CMD [ "fwatchdog" ]
