FROM ubuntu:latest

RUN apt-get -y update \
  && apt-get -y install curl supervisor

# Dockerのインストール
WORKDIR /tmp
RUN curl -fsSL https://get.docker.com -o get-docker.sh \
  && sh get-docker.sh \
  && update-alternatives --set iptables /usr/sbin/iptables-legacy \
  && update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy
COPY ./docker.conf /etc/default/docker

# Github Actionsの設定
ENV RUNNER_ALLOW_RUNASROOT 1
WORKDIR /actions-runner
RUN curl -o actions-runner-linux-x64-2.301.1.tar.gz -L https://github.com/actions/runner/releases/download/v2.301.1/actions-runner-linux-x64-2.301.1.tar.gz \
  && tar xzf ./actions-runner-linux-x64-2.301.1.tar.gz \
  && ./bin/installdependencies.sh \
  && ./config.sh --url https://github.com/yuki-noguchi/github-actions-study --token AEWYBRPPGY23MT63LFVTESTD4ZILA

# 各種プロセス起動
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

CMD ["/usr/bin/supervisord"]