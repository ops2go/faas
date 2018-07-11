FROM alpine:3.7

RUN apk --no-cache add \
    curl \
    python \
    py-crcmod \
    bash \
    libc6-compat \
    openssh-client \
    git \
    && curl -sSL https://github.com/openfaas/faas/releases/download/0.8.0/fwatchdog > /usr/bin/fwatchdog \
    && chmod +x /usr/bin/fwatchdog \
    && curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz && \
    tar xzf google-cloud-sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz && \
    rm google-cloud-sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz && \
    ln -s /lib /lib64 && \
    gcloud config set core/disable_usage_reporting true && \
    gcloud config set component_manager/disable_update_check true && \
    gcloud config set metrics/environment github_docker_image && \
    gcloud --version
    
ENV CLOUD_SDK_VERSION 206.0.0

ENV PATH /google-cloud-sdk/bin:$PATH
    
VOLUME ["/root/.config"]

# Populate example here - i.e. "cat", "sha512sum" or "node index.js"
ENV fprocess="gcloud"
# Set to true to see request in function logs
ENV write_debug="false"

HEALTHCHECK --interval=5s CMD [ -e /tmp/.lock ] || exit 1
CMD [ "fwatchdog" ]
