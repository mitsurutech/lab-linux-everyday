# 毎日使うLinuxコマンドのラボ：ls、grep、tail -f、ssh、scp、kill を1台のUbuntu VMで

[English](README.md) | [Français](README.fr.md) | [日本語](README.ja.md) | [Español](README.es.md)

[![check](https://github.com/mitsurutech/lab-linux-everyday/actions/workflows/check.yml/badge.svg)](https://github.com/mitsurutech/lab-linux-everyday/actions/workflows/check.yml)

授業ですぐ使える**Linuxコマンドのラボ**です。学校がそれぞれの生徒に専用のUbuntuマシンとブラウザ上のターミナルを渡せる、[MitsuruTech Learning Platform](https://mitsurutech.co.uk/ja/learning)のものです。ソフトウェアエンジニアが調べずに打つコマンドのひとつひとつに、実際に動かせる相手を用意しています。**ファイルをたどって探す**（`ls`、`cd`、`find`、`grep`）、**書き込み中のログを読む**（`tail -f`）、**プロセスを見つけて止める**（`ps | grep`、`kill`、`kill -9`）、**ファイルを取得して展開する**（`curl`、`wget`、`zip`、`gzip`）、**別のアカウントに入ってファイルを送る**（`ssh`、`scp`）。生徒のパソコンには何もインストールしません。

## マシンの中身

| 何 | どこ | 使うコマンド |
| --- | --- | --- |
| 1時間分の行があり、2秒ごとに増えるログ | `/var/log/test.log` | `tail`、`grep`、エラーの数え方 |
| アーカイブと、圧縮するファイル | `~/test.zip`、`~/test` | `unzip`、`gzip` |
| たどるための小さなフォルダ木と、安心して消せるフォルダ | `~/projects`、`~/scratch` | `ls`、`cd`、`find`、`cp`、`mv`、`rm -rf` |
| 小さなファイルを2つ置いた、ポート8000のWebサーバー | `localhost:8000` | `curl`、`wget` |
| 2つのプロセス（1つは通常の `kill` を無視する） | `lab-worker`、`lab-stubborn` | `ps`、`kill`、`kill -9` |
| 鍵で入れる2つ目のアカウント `dev`（名前は `devbox`） | `ssh devbox` | `ssh`、`scp` |

2つ目のアカウントは**同じマシン**にあり、別のマシンではありません。コマンドは同じで、2台目のVMは待ち時間が増えるだけだからです。このラボには自動採点も課題もありません。プラットフォームの5つのレッスンが活動で、点数をつけたい先生は自分で提出物を設定します。

## ファイルの中身

`linux-everyday.lab.yaml` は、プラットフォームがそのまま実行する**VMラボの定義**です。

| キー | 内容 |
| --- | --- |
| `cpus`、`memory`、`disk` | 生徒ごとのVMの大きさ：CPU 1つ、1024 MB、10 GB |
| `open` | ブラウザで開くポート：なし。ラボはターミナルです |
| `setup` | 各生徒のVMが初めて起動するときに、rootで1回だけ実行されるスクリプト。Ubuntuのアーカイブからいくつかのパッケージを入れ、ログ、ファイル、2つのプロセス、Webサーバー、2つ目のアカウントを作り、ホームフォルダにREADMEを置きます |

## プラットフォームで使う

1. モジュールに課題を追加し、**Ubuntu VMラボ**のカードを選びます。
2. サンプルを押すか、`linux-everyday.lab.yaml` の中身を貼り付けます。サンプルを使うと文章が置き換わりますが、元に戻すで自分のものに戻せます。
3. 公開して、まず自分のコピーで試します。生徒ごとに専用のVMがあり、授業をまたいで残ります。
4. ふつうの課題と同じように割り当てるか、ライブラリのレッスンを開いてコマンドの横の実行を押します。

このラボの[マニュアルのページ](https://mitsurutech.co.uk/ja/help/lab-linux-everyday)、[Ubuntu VMラボのガイド](https://mitsurutech.co.uk/ja/help/labs)、[サンプルラボのページ](https://mitsurutech.co.uk/ja/help/sample-labs)に、そのほかのことが書いてあります。学校のアカウントがまだありませんか。生徒50人まで[最初の1年は無料](https://mitsurutech.co.uk/ja/pricing)で、[登録](https://mitsurutech.co.uk/ja/signup)にはメールアドレスだけが必要です。

## ファイルの確認

pushのたびに、`.github/workflows/check.yml` が、ファイルが上のキーを持つ正しいYAMLであること、`setup` がプラットフォームの16 KBの上限に収まっていることを確かめます。VMは起動しません。それはプラットフォームのマシンで行います。

## ラボでできないこと

VMが届くのはUbuntuのパッケージアーカイブ、PyPI、npm、GitHubだけで、ほかには届きません。インターネット上のホストを相手にはできないので、Webサーバーはラボの中に置いています。

## このラボについて

[Mitsuru Technologies](https://mitsurutech.co.uk)が、学校向けにPython、Java、Go、Node、SQL、Linuxをブラウザで学べる[MitsuruTech Learning Platform](https://mitsurutech.co.uk/ja/learning)のために作りました。コンテナラボ、VMラボ、GitHubから公開するWebアプリ、自動で採点されるクイズがあります。アカウントなしで[プレイグラウンド](https://mitsurutech.co.uk/ja/playground)でコードを試せます。

同じところの他のラボ：[lab-linux-admin](https://github.com/mitsurutech/lab-linux-admin)、[lab-linux-privesc](https://github.com/mitsurutech/lab-linux-privesc)、[lab-incident-response](https://github.com/mitsurutech/lab-incident-response)、[lab-netlab](https://github.com/mitsurutech/lab-netlab)、[lab-git-gitea](https://github.com/mitsurutech/lab-git-gitea)、[lab-sample](https://github.com/mitsurutech/lab-sample)。

## ライセンス

この作品は[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)で提供されます。Mitsuru Technologies Ltdのクレジットを表示し、営利目的で使わず、これをもとに作ったものを同じライセンスで共有するなら、学習と教育のために共有・改変できます。全文は `LICENSE` ファイルにあります。

`zip`、`unzip`、`curl`、`wget`、`openssh-server`、`vim`、`python3` はVMの起動時にUbuntuのアーカイブから入れます。ここでは配布していません。
