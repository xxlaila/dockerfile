FROM jenkins/jenkins:2.150.1
MAINTAINER "Xiao Mo" <root@xiaomo.site>

# Distributed Builds plugins
RUN /usr/local/bin/install-plugins.sh ssh-slaves

# install Notifications and Publishing plugins
RUN /usr/local/bin/install-plugins.sh email-ext
RUN /usr/local/bin/install-plugins.sh mailer
RUN /usr/local/bin/install-plugins.sh slack

# Artifacts
RUN /usr/local/bin/install-plugins.sh htmlpublisher

# UI
RUN /usr/local/bin/install-plugins.sh greenballs
RUN /usr/local/bin/install-plugins.sh simple-theme-plugin

# Scaling
RUN /usr/local/bin/install-plugins.sh kubernetes


RUN /usr/local/bin/install-plugins.sh matrix-auth

RUN /usr/local/bin/install-plugins.sh antisamy-markup-formatter

USER root
# Docker
ENV DOCKER_CHANNEL stable
ENV DOCKER_VERSION 18.06.1-ce
RUN wget -O /usr/local/src/docker.tgz "https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/static/${DOCKER_CHANNEL}/x86_64/docker-${DOCKER_VERSION}.tgz" \
    && tar --strip-components=1 -xvzf /usr/local/src/docker.tgz -C /usr/local/bin \
    && rm -rf /usr/local/src/docker.tgz

# 下载Kubernetes二进制文件
ENV KUBE_VERSION=v1.13.0
RUN wget https://storage.googleapis.com/kubernetes-release/release/${KUBE_VERSION}/kubernetes-server-linux-amd64.tar.gz -O /usr/local/src/kubernetes-server-linux-amd64.tar.gz \
    && tar -zxvf /usr/local/src/kubernetes-server-linux-amd64.tar.gz  \
        --strip-components=3 -C /usr/local/bin \
        kubernetes/server/bin/kubectl \
    && rm -rf /usr/local/src/kubernetes-server-linux-amd64.tar.gz

USER jenkins