FROM buildpack-deps:stretch-scm

ARG awscli_version
ENV AWSCLI_VERSION=${awscli_version:-1.15.7}

RUN wget https://download.docker.com/linux/static/stable/x86_64/docker-18.09.0.tgz -O docker.tgz && tar --extract --file docker.tgz --strip-components 1 --directory /usr/local/bin/ \
    && rm docker.tgz

RUN wget https://github.com/nuclio/nuclio/releases/download/0.7.2/nuctl-0.7.2-linux-amd64 -O /usr/local/bin/nuctl \
    && chmod +x /usr/local/bin/nuctl

RUN wget -O kops https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64 \
&& chmod +x ./kops \
&& mv ./kops /usr/local/bin/

RUN wget https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl -O /usr/local/bin/kubectl \
     && chmod +x /usr/local/bin/kubectl

RUN wget https://bootstrap.pypa.io/get-pip.py -O get-pip.py && python get-pip.py

RUN  pip install awscli --upgrade

COPY modprobe.sh /usr/local/bin/modprobe
COPY docker-entrypoint.sh /usr/local/bin/

RUN chmod +x /usr/local/bin/docker-entrypoint.sh
ENTRYPOINT ["docker-entrypoint.sh"]
# CMD ["sh"]