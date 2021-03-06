---
copyright:
  years: 2014, 2018
lastupdated: "2018-01-26"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# FAQ: MySQL

## MySQL サーバーをどのような方法でモニターできますか

Linux アプリケーションの _mytop_ は近似時間モニター (UNIX ユーティリティーの「top」に似ています) で、具体的には {{site.data.keyword.mysql}} サーバーが何を実行しているかをモニターします。_mytop_ は、数秒ごとに更新されるため、SQL のパフォーマンスを十分に確認できます。 _mytop_ は、大量の情報を表示することもできます。 また、ユーザーは、ローカル・ホスト上の {{site.data.keyword.mysql}} サーバーに root ユーザーとしてパスワードを使用せずに接続していることを前提としています。 資格情報は、スクリプト自体またはコマンド・ラインで変更できます。

## MySQL のルート・パスワードは何ですか

* サーバーが {{site.data.keyword.mysql}} を使用して自動プロビジョンされた場合、ルート・パスワードはサーバー・ルート・パスワードと同じです。
* サーバー上で Plesk が自動プロビジョンされた場合、「admin」と Plesk の管理パスワードを使用します。
* source、RPM、または up2date を使用して {{site.data.keyword.mysql}} をインストールした場合、初期 root アカウント・パスワードは空です。 {{site.data.keyword.mysql}} のインストール中またはインストール後にルート・パスワードを設定しない限り、すべてのユーザーがパスワードなしに root として {{site.data.keyword.mysql}} サーバーに接続することができ、すべての特権が付与されます。

## MySQL に関する情報の最良のオンライン・リソースは何ですか

[{{site.data.keyword.mysql}} Web サイト ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://dev.mysql.com/doc/){: new_window} に詳細なリファレンス・マニュアルがあり、検索機能を使用できます。

この資料は、基本的なインストールから、SQL 構文、複製やクラスター化などの高度な使用方法に至るまで、あらゆる情報をカバーしています。 また、このリファレンス・マニュアルのドイツ語、フランス語、日本語、ポルトガル語、ロシア語の翻訳版も用意されています。
