FROM node:6.8

RUN apt-get update \
    && rm -rf /var/lib/apt/lists/*

#RUN npm install -g slack-cli
RUN npm install -g slack-webhook-cli

RUN apt-get install -y curl

RUN curl -sSL https://github.com/openfaas/faas/releases/download/0.8.0/fwatchdog > /usr/bin/fwatchdog \
    && chmod +x /usr/bin/fwatchdog \
    
ENV fprocess="xargs slack-hook"
# Set to true to see request in function logs
ENV write_debug="false"

HEALTHCHECK --interval=5s CMD [ -e /tmp/.lock ] || exit 1
CMD [ "fwatchdog" ]
