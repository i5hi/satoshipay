FROM python:3.6-alpine3.12

RUN apk add -u \
    build-base linux-headers zlib zlib-dev \
    ca-certificates \
    curl \
    unzip \
    git \
    jq \
    openssl openssl-dev 

RUN git clone https://github.com/LunaNode/lndynamic-api.git

COPY ./deploy.py /lndynamic-api/deploy.py
COPY ./deployment.json /lndynamic-api/deployment.json

CMD [ "tail", "-f" , "/dev/null" ]
