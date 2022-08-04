# 概要

Docker Desktopのk8sの学習をLinuxコンテナから効率的(入力補完)に扱えるようにするための環境

# 手順

1. Docker Desktopのk8sの`config`(`%USERPROFILE%\.kube\config`)をkube-configにコピー<br/>
    複数のコンテキストがある場合、必要に応じて`docker-desktop`のみに編集してください
2. VSCode「Remote Container」を起動する


# metrics-server

[helm](https://artifacthub.io/packages/helm/metrics-server/metrics-server)からインストールする<br/>
[argsを修正](https://qiita.com/nakamasato/items/c49cf322cd5d7770b465)<br/>
※namespaceに要注意！<br/>

```yaml
- --kubelet-insecure-tls
- --kubelet-preferred-address-types=InternalIP
```