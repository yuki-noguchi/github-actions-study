FROM ubuntu:latest

ENV RUNNER_ALLOW_RUNASROOT 1

WORKDIR /actions-runner

RUN apt-get -y update && apt-get -y install curl 

RUN curl -o actions-runner-linux-x64-2.301.1.tar.gz -L https://github.com/actions/runner/releases/download/v2.301.1/actions-runner-linux-x64-2.301.1.tar.gz \
  && tar xzf ./actions-runner-linux-x64-2.301.1.tar.gz \
  && ./bin/installdependencies.sh \
  && ./config.sh --url https://github.com/yuki-noguchi/github-actions-study --token AEWYBRMXPVU2GVLN3MAD4VDD4YH3A

ENTRYPOINT [ "./run.sh" ]