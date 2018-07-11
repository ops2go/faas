FROM ubuntu:16.04

RUN mkdir /kubespray

WORKDIR /kubespray

RUN apt update -y && \
    apt install -y \
    libssl-dev python-dev sshpass apt-transport-https \
    ca-certificates curl gnupg2 software-properties-common python-pip
    
RUN curl -sSL https://github.com/openfaas/faas/releases/download/0.8.0/fwatchdog > /usr/bin/fwatchdog && \
    chmod +x /usr/bin/fwatchdog && \
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
    add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) \
    stable" \
    && apt update -y && apt-get install docker-ce -y
    
COPY . .

RUN /usr/bin/python -m pip install pip -U && /usr/bin/python -m pip install -r tests/requirements.txt && python -m pip install -r requirements.txt

ENV fprocess="ansible-playbook"

ENV write_debug="false"

HEALTHCHECK --interval=5s CMD [ -e /tmp/.lock ] || exit 1

CMD [ "fwatchdog" ]
