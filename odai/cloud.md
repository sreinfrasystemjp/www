---
layout: post
title: "クラウド選定基準 in Japan"
permalink: /odai/cloud
image: /images/ms/cloud.png
---

<p class="breadcrumb">
  <a href="/">TOP</a> ＞ お題 ＞ {{ page.title }}
</p>

# クラウド選定基準 in Japan

<p class="author">
  Last Update: 2017-12-07 <a href="https://github.com/ihironao">i.hironao</a>
</p>

## 選定基準 201712版

- 問１：堅実派／チャレンジ派

  あなたのプロジェクトの社風は、

  1 . MySQLは心配だからOracleデータベース使う  
  2 . MySQLで必要十分

  のどちらですか？

  1の場合 → AWS一択です。  
  2の場合 → GCPが最強です。

- 問２：社内向けシステム／社外向けシステム

  あなたのプロジェクトのサービス内容は、

  1 . 社内システム：社員１万人〜  
  2 . 社内システム：社員50人以下  
  3 . 社外システム：ECサイト等

  のどちらですか？

  1の場合 → Microsoft Azure でActive Directory 認証使いましょう。  
  2、3の場合 → GCP ＆ g suite (gmail) 認証使いましょう。

- 問３：モノシリック／マイクロサービス

  あなたのプロジェクトは、(phpの場合)
  
  1 . SymfonyやLaravelによるモノシリックアプリケーション  
  2 . lumenやslim3によるマイクロサービス

  のどちらですか？

  1の場合 → AWSが一番使い勝手がよいです。  
  2の場合 → GCP ＆ GAE & GKE 使いましょう。

- 問４：国内派／国外OK派

  あなたのプロジェクトは、
  
  1 . データは全部国内必須。  
  2 . データは海外でもかまわない。

  のどちらですか？

  1の場合 → Microsoft Azureの「東日本リージョン」「西日本リージョン」で冗長化しましょう。  
  2の場合 → GCPの「東京リージョン」「オレゴンリージョン」で冗長化しましょう。同一LAN内のように使えます。

## 何故クラウドが必須なのか

例：画像処理  
　これまで： 投稿記事に写真をuploadします。  
　これから： 投稿記事にuploadされた写真を、アダルト画像判定＆公開可否を判定後登録します。 

といった機能の標準装備が必要です。  
これができなかったのがオンプレ、できるようになったのがクラウドです。

## クラウドのシェア

[世界のクラウド市場シェアのNo１は？](http://cloudnights.net/cloud/cloud_research/)  
の記事(2017年第2四半期)によると、

||AWS|Microsft<br>Azure|IBM|GCP|Next10|他|
|---|---|---|---|---|---|---|
|2017Q2|34%|11%|8%|5%|19%|23%|
|1年の成長率|+1%|+3%|0%|+1%|-1%|-5%|

- AWS一強
- 今後の成長が見込めるのはAWS,Microsft Azure,GCPの３クラウドのみ

です。

クラウドビジネスは規模＆開発力勝負のビジネスです。何年か後に、

- 「AWSと同じようなサービス提供」のクラウドは生き残り
- 「AWSに満たないサービス提供」のクラウドは無くなる

と思っていてよいです。

## 各クラウド寸評

- AWS

  - No1ブランドです。
  - 一番歴史があります。
  - 既に技術的負債がたくさんあります。(例：EC2ガチャ [AWSバッドノウハウ集 2017/02](https://qiita.com/yayugu/items/de23747b39ed58aeee8a) )
  - 隠れ運用負荷が多いです。
  - 豊富すぎる機能があります。
  - IT系求人サイト上では、AWSオンリーです。
  - オンプレでも、「バックアップ先はS3」「DNS(GSLB)はRoute53」のように一部機能のみ使用される事も多いです。

- Microsoft Azure

  - Windows系システムに一番やさしいクラウドです。
  - 日本に「東日本リージョン」「西日本リージョン」の２つがあり、国内でマルチリージョンが可能です。
  - 自社所有日米間海底ケーブル回線太さは世界で２番めです(一番は米軍)
  - 2016年頃に、いろんな機能が再開発されました。旧機能は技術的負債の塊です。
  - オンラインマニュアルの日本語版に、旧機能の説明が残っている事が多く、「Microsoft Azureを本格活用したいならもう２年待て」感が強いです。
  - ファイルサーバ(cifsマウント)があるのはMicrosoft Azureのみです。

- GCP

  - 一番お財布にやさしいクラウドです。（だいたい他クラウドの7割）
  - 2016-11に、東京リージョンがオープンし、第１選択肢になりました。
  - bigqueryのように、まだ日本に来ていないサービスがあります。
  - 隠れ運用負荷が一番小さいクラウドです。（ハードウェア交換時無停止、オンラインディスク拡張）
  - 機能が少ないため、（オンプレ同様の）自力準備が必要な部分があります。(memcachedとか、NFSサーバとか...)
  - bigqueryだけは他のクラウドの代替機能が実質存在しません。AWS使用時、「集計だけはbigquery」の場合があります。
  - クラウドの中で、「事前申請なく負荷試験OK」なのはGCPだけです。これ、ネットワーク基盤の実力が、「他のクラウド ＜＜＜ (超えられない壁) ＜＜＜ GCP」という話...

- 他のクラウド

  開発力が上の３社に満たないクラウドは、ニッチ分野でしか生き残れません。

  [Googleの採用担当が明かす、逸材を採用する4つの法則とは「面接は複数で行う」](http://news.livedoor.com/article/detail/10001864/)  
  によると、googleの採用は

  - 年間200万人を超える応募者
  - 1年に数千人採用

  という規模感です。

  このうち、どれくらいの人数が GCP の技術者として働くのかはわかりませんが、  
  国内クラウド業者の「技術者全部で10名」みたいな規模感では太刀打ちできません...
