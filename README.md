# セルフホストランナーを用いた Github Actions

## やりたきこと

- セルフホストランナーを用いて Github Actions を動かしたい
- セルフホストランナーの実行環境は Docker コンテナー上としたい
- セルフホストランナー上で Java を gradle を用いてビルドしたい
- セルフホストランナー上で Docker イメージをビルドしたい

## ファイル構成

```
├── README.md
├── .github
│   ├── self-hosted-runner
│   │   ├── Dockerfile
│   │   ├── docker.conf
│   │   └── supervisord.conf
│   └── workflows
│       └── build-java.yml
└── dummy --> Quarkusプロジェクト
    └── gradlew
    └── build/
    └── ...
```

## ビルド&起動

### ビルド

```
cd /path/to/github-actions-study/.github/self-hosted-runner

docker build -t selfhosted-runner .
```

### 起動

```
docker run --privileged=true selfhosted-runner
```

docker コンテナーの中で docker を起動する関係で、 `--privileged=true` が必要。
