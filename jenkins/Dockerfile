FROM jenkins/jenkins:2.150.2
MAINTAINER "Xiao Mo" <root@xiaomo.site>

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

COPY plugins.txt /tmp/
RUN /usr/local/bin/install-plugins.sh $(cat /tmp/plugins.txt | tr '\n' ' ')