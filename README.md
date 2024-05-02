# dev-container-python <!-- omit in toc -->

- [1. 概要](#1-概要)
- [2. 動作環境](#2-動作環境)
  - [2.1. 参考サイト](#21-参考サイト)
- [3. 起動方法](#3-起動方法)
  - [3.1. Dockerの起動](#31-dockerの起動)
    - [3.1.1. \[DockerCLI版\] Dockerの起動](#311-dockercli版-dockerの起動)
    - [3.1.2. \[DockerDesktop版\] Dockerの起動](#312-dockerdesktop版-dockerの起動)
  - [3.2. VSCodeの起動](#32-vscodeの起動)
- [4. トラブルシューティング](#4-トラブルシューティング)
  - [4.1. \[DockerDesktop版\] DevContainerの起動に失敗する](#41-dockerdesktop版-devcontainerの起動に失敗する)
    - [4.1.1. ダイアログ](#411-ダイアログ)
    - [4.1.2. エラーログ](#412-エラーログ)
    - [4.1.3. 解決方法](#413-解決方法)
    - [4.1.4. 参考サイト](#414-参考サイト)

## 1. 概要

`Docker`と`VSCode`の拡張機能である`Dev Containers`を使用することにより、ホスト環境を汚すことなくコンテナに開発環境を構築できる。

また、開発環境をコードとして管理できる。
例えば`VSCode`の設定、拡張機能のインストール、`Docker`イメージの管理、OSパッケージのインストールなどが該当する。

## 2. 動作環境

- Windows 10 Pro 22H2
- VSCode 1.82.2
- Dev Containers v0.309.0
- Docker CLI 24.0.5 / Docker Desktop 4.22.1
- WSL2
- Ubuntu 22.04
- Debian 11 (bullseye)

構築手順は下記リポジトリを参照する。

- https://github.com/silverag-corgi/dev-env-for-windows

### 2.1. 参考サイト

1. [Docker DevContainer - Google 検索](https://www.google.com/search?q=Docker+DevContainer)
    - [Developing inside a Container using Visual Studio Code Remote Development](https://code.visualstudio.com/docs/remote/containers#_system-requirements)

## 3. 起動方法

`Docker CLI`を用いた環境の場合はタイトルの先頭に`DockerCLI版`がある手順を実施する。
また、`Docker Desktop`を用いた環境の場合はタイトルの先頭に`DockerDesktop版`がある手順を実施する。

### 3.1. Dockerの起動

#### 3.1.1. [DockerCLI版] Dockerの起動

1. `Docker CLI`は`Ubuntu 22.04`が自動的に起動する

#### 3.1.2. [DockerDesktop版] Dockerの起動

1. `Windows 10`で`Docker Desktop`を起動する

### 3.2. VSCodeの起動

1. `Windows 10`で`VSCode`を起動し、画面左側のリモートエクスプローラーに表示されている`Ubuntu-22.04`に接続する
2. `Ubuntu 22.04`でワークスペースをDevContainerフォルダに切り替えるため、下記操作を実施する
    1. `ファイル＞フォルダを開く...`(`Ctrl+K Ctrl+O`)をクリックする
    2. DevContainerフォルダを指定する
      - `<Gitフォルダパス>/dev-container-python/`
3. `Ubuntu 22.04`で`DevContainer`を起動するため、下記操作を実施する
    1. コマンドパレット(`F1`)を表示する
    2. `Dev Containers: Reopen in Container`をクリックする
4. `Debian 11`でワークスペースを任意のフォルダに切り替えるため、下記操作を実施する
    1. `ファイル＞フォルダを開く...`(`Ctrl+K Ctrl+O`)をクリックする
    2. 任意のフォルダを指定する

## 4. トラブルシューティング

本環境で頻発するエラーへの解決方法をまとめる。

`Docker CLI`を用いた環境の場合はタイトルの先頭に`DockerCLI版`がある手順を実施する。
また、`Docker Desktop`を用いた環境の場合はタイトルの先頭に`DockerDesktop版`がある手順を実施する。

### 4.1. [DockerDesktop版] DevContainerの起動に失敗する

#### 4.1.1. ダイアログ

```log
コンテナの設定中にエラーが発生しました。
```

#### 4.1.2. エラーログ

```log
[2023-05-11T08:45:50.808Z] ERROR: docker endpoint for "default" not found
```

#### 4.1.3. 解決方法

1. `Windows 10`でメタ情報を削除するため、下記コマンドを`PowerShell`で実行する
    ```shell
    > rm ~/.docker/contexts/meta/<SHA256>/meta.json
    ```

#### 4.1.4. 参考サイト

1. [devcontainer ERROR: docker endpoint for "default" not found - Google 検索](https://www.google.com/search?q=devcontainer+ERROR%3A+docker+endpoint+for+%22default%22+not+found)
    1. [[BUG] docker endpoint for "default" not found - Issue #9956 - docker/compose - GitHub](https://github.com/docker/compose/issues/9956)
