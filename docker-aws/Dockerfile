FROM docker:latest

ARG awscli_version
ARG terraform_version
ARG kubectl_version
ARG helm_version
ARG istio_version
ENV AWSCLI_VERSION=${awscli_version:-1.16.304}
ENV TERRAFORM_VERSION=${terraform_version:-0.12.18}
# ENV TERRAFORM_SHA256SUM=b786c0cf936e24145fad632efd0fe48c831558cc9e43c071fffd93f35e3150db
ENV TOOLSET_NAME="kops-tools"
ENV CWD="/${TOOLSET_NAME}"
ENV UNPRIVILEDGED_USER="kops"
ENV KUBECTL_VERSION=${kubectl_version:-v1.17.0}
ENV HELM_VERSION=${helm_version:-v2.14.0}
ENV YAML_SHASUM=28308a7231905030a62f20c92d41513e570d24f1984c1864198cbc4e039d3bec
ARG ISTIOCTL_VERSION=${istio_version:-1.4.2}
# ENV KOPS_RELEASE_ID=8410205

RUN apk add --update --no-cache bash ca-certificates coreutils jq git make py2-pip util-linux openssh openssl tree gettext curl

# ADD commands are not cached by docker, using wget
RUN wget https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip -O terraform_${TERRAFORM_VERSION}_linux_amd64.zip
RUN unzip -o terraform_${TERRAFORM_VERSION}_linux_amd64.zip -d /bin
RUN rm -f terraform_${TERRAFORM_VERSION}_linux_amd64.zip
RUN rm -f terraform_${TERRAFORM_VERSION}_SHA256SUMS

# install awscli
RUN pip --disable-pip-version-check install awscli==$AWSCLI_VERSION

# kops
RUN wget -O kops https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64 \
&& chmod +x ./kops \
&& mv ./kops /usr/local/bin/

RUN wget https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl -O /usr/local/bin/kubectl \
    && chmod +x /usr/local/bin/kubectl
RUN wget http://storage.googleapis.com/kubernetes-helm/helm-${HELM_VERSION}-linux-amd64.tar.gz \
    && tar -xvf helm-${HELM_VERSION}-linux-amd64.tar.gz \
    && mv linux-amd64/helm /usr/local/bin \
    && rm -f /helm-${HELM_VERSION}-linux-amd64.tar.gz

RUN wget -O istio.tar.gz https://github.com/istio/istio/releases/download/$ISTIOCTL_VERSION/istio-$ISTIOCTL_VERSION-linux.tar.gz \
  && tar -xzf istio.tar.gz \
  && mv istio-$ISTIOCTL_VERSION /istio \
  && rm istio.tar.gz && chmod +x /istio/bin/istioctl && ln -s /istio/bin/istioctl /usr/local/bin/

RUN wget https://github.com/mikefarah/yq/releases/download/2.1.2/yq_linux_amd64 -O /usr/local/bin/yq && chmod +x /usr/local/bin/yq

ENTRYPOINT ["/bin/sh"]


