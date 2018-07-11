FROM google/cloud-sdk:latest
COPY ./gcloud/ /root/.config/gcloud/
ADD https://github.com/openfaas/faas/releases/download/0.7.0/fwatchdog /usr/bin
RUN chmod +x /usr/bin/fwatchdog
ENV fprocess="xargs gcloud"
HEALTHCHECK --interval=5s CMD [ -e /tmp/.lock ] || exit 1
CMD ["fwatchdog"]
