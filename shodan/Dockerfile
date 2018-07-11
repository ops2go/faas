FROM ubuntu:14.04

RUN apt-get update ; apt-get -y install python-pip \    
        python  -dev

RUN pip install shodan      

RUN curl -sSL https://github.com/openfaas/faas/releases/download/0.8.0/fwatchdog > /usr/bin/fwatchdog && \
    chmod +x /usr/bin/fwatchdog

ENV APIKEY=""
ENV fprocess="xargs shodan"
ENV write_debug="false"

CMD shodan init $APIKEY
HEALTHCHECK --interval=5s CMD [ -e /tmp/.lock ] || exit 1
CMD [ "fwatchdog" ]
