FROM node:20

WORKDIR /work

ARG USERNAME

RUN apt-get update && apt install -y \
        iputils-ping \
        iproute2 \
        jq \
        dnsutils \
        sysstat \
        lsof \
        nkf \
        socat \
    # clear apt cache
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    # change node user image added beforehand UID:GID to another
    && groupmod -g 2000 node \
    && usermod -u 2000 node \
    && chown -R 2000:2000 /home/node \
    && chown 2000:2000 /opt/yarn-*/* \
    # add host user
    && groupadd ${USERNAME} \
    && useradd -d /home/${USERNAME} -s /bin/bash -g ${USERNAME} -m ${USERNAME} \
    && mkdir -m 777 /workspaces \
    # install npm packages
    && npm install -g git-cz typescript aws-cdk
