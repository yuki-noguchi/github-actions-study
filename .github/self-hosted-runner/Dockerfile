FROM ubuntu:latest

RUN apt-get -y update \
  && apt-get -y install curl supervisor

# Dockerのインストール
# ref: https://docs.docker.com/engine/install/ubuntu/#install-using-the-convenience-script
WORKDIR /tmp
RUN curl -fsSL https://get.docker.com -o get-docker.sh \
  && sh get-docker.sh
COPY ./docker.conf /etc/default/docker

# kubectlのインストール
# ref: https://kubernetes.io/ja/docs/tasks/tools/install-kubectl/
RUN curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl" \
  && chmod +x ./kubectl \
  && mv ./kubectl /usr/local/bin/kubectl

# Github Actionsの設定
# ref: https://github.com/yuki-noguchi/github-actions-study/settings/actions/runners/new?arch=x64&os=linux
ENV RUNNER_ALLOW_RUNASROOT 1
WORKDIR /actions-runner
RUN curl -o actions-runner-linux-x64-2.301.1.tar.gz -L https://github.com/actions/runner/releases/download/v2.301.1/actions-runner-linux-x64-2.301.1.tar.gz \
  && tar xzf ./actions-runner-linux-x64-2.301.1.tar.gz \
  && ./bin/installdependencies.sh \
  # 実際に使用する際にはトークンを正しいものに書き換える
  && ./config.sh --url https://github.com/yuki-noguchi/github-actions-study --token dummy

# 各種プロセス起動
# Github ActionsとDockerの2プロセスを起動するために、supervisorを使用する
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
CMD ["/usr/bin/supervisord"]