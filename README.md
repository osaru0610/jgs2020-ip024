# JGS 2020 IP-024 Meeting Police

<img src="https://user-images.githubusercontent.com/23325882/86427041-21194d00-bd24-11ea-8480-11e34c0ca1fe.gif" alt="Meeting Police Screen Image" width="576" height="360">

## 概要

このコードは、[日本 GUIDE/SHARE 委員会](http://www.uken.or.jp/jgs/news/index.html)の 2020 年タスク活動での検証を目的に作成したアプリケーションです。
企業の社内研修で、研修講師が話した声をリアルタイムに音声認識させ、受講者が匿名で音声テキストに対して「いいね」や「分からない」と反応したり、チャットボックスにテキストで質問をすることで、講師と受講者の間のコミュニケーションを促進し、受講者の理解度に合わせた研修運営を行うことを支援します。

## 説明

- 音声認識技術は、[Web Speech API](https://developer.mozilla.org/ja/docs/Web/API/Web_Speech_API)を使用しています。Web Speech API は、現時点では Google Chrome ブラウザでのみサポートされているため、それ以外のブラウザでは音声認識機能は利用できません。Google Chrome ブラウザはデスクトップ版でのみ動作検証を行っており、モバイル版では動作検証は行っておりません。**音声認識させたい講師は、Google Chrome がインストールされて、マイク等で音声入力が可能な PC を使用してください**。音声認識機能を利用しない場合は、Google Chrome 以外の主要ブラウザでも利用可能です。
- 講師が発話した内容の音声テキスト、いいねボタンや分からないボタンのクリック情報、チャットボックスに入力したテキストは、[Node.js](https://nodejs.org/ja/)の[Socket.IO](https://socket.io/)エンジンを利用して、リアルタイムに共有（アプリケーションを表示している全員に対してブロードキャスト）されます。**アプリケーションは、講師および受講者が参照可能な Web アプリケーション・サーバーで動作させてください**。私たちのタスクでは、IBM Cloud の[Cloud Foundry Public](https://www.ibm.com/jp-ja/cloud/cloud-foundry)でアプリケーションを動作させました。
- 画面に出力された音声テキストやチャットメッセージとその投稿日時、いいねボタンや分からないボタンが実行された回数は、クリップボードに CSV 形式でコピーすることが出来ます（Click to Copy Voice Text to Clipboard ボタン）。ログを残したい場合はご利用くだっさい。画面に出力されている情報を取得しているだけですので、自分が画面を表示する前のログを遡って取得することは出来ません。

## 使用手順

Node.js が利用可能であること、Git が利用可能であること

.env.sample を.env にファイル名変更してください。.env には、Basic 認証の ID とパスワードが記載されています。任意で変更してください。

```
mv .env.sample .env
```

（オプション）IBM Cloud の Cloud Foundry Public にデプロイする場合は、manifest.yml.sample を manifest.yml にファイル名変更し、内容を適宜カスタマイズしてください。

## 注意事項

- 音声認識対象とする音声には業務上の秘密などを含めないことをお勧めします。
- タスク活動での限定的な検証を目的に作成したアプリケーションですので、本番環境での本格活用などは想定しておりません。
