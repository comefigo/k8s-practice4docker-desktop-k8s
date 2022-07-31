# 概要

Docker Desktopのk8sの学習をLinuxコンテナから効率的(入力補完)に扱えるようにするための環境

# 手順

1. Docker Desktopのk8sの`config`(`%USERPROFILE%\.kube\config`)をkube-configにコピー<br/>
    複数のコンテキストがある場合、必要に応じて`docker-desktop`のみに編集してください
2. VSCode「Remote Container」を起動する