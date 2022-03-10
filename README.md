# slack_reaction_statistics

Slackでリアクション(スタンプ)が多くついた投稿をピックアップするボットです。

例えば、10日前から1日前までの公開チャンネルでたくさんリアクション（スタンプ）のついた投稿上位10件を抽出して、そのリンクを投稿します。

```
皆さんこんにちは。
04月01日から04月07日の間で、注目を集めたメッセージをお知らせします。

注目を集めたメッセージは......!!

.... // 以下、展開されるリンク
```

[紹介記事](https://hiroyky.hatenablog.com/entry/2020/05/13/015636)

## 使い方

### 設定
.envファイルに設定を書きます。
```sh
cp .env.exsample .env
```

| 項目 | 概要 | 例 |
| --- | --- | --- |
| SLACK_TOKEN | APIのリクエストを許可するトークン | xoxb-xxxx.. |
| POST_CHANNEL | 投稿先のチャンネルID | C010WGM29XX |
| FROM_DAYS | 何日前からの投稿を対象にするか | 8 |
| TO_DAYS | 何日前までの投稿を対象にするか | 1 |
| NUM_FEATURES | 上位何件を特殊投稿するか | 10 |
| INCLUDE_CHANNELS | 対象とするチャンネルを限定する場合はチャンネルIDを指定、複数の場合はコンマ区切り | |
| EXCLUDE_CHANNELS | 除外したいチャンネルがある場合はチャンネルIDを指定、複数の場合はコンマ区切り | |
| EXCLUDE_WORDS | 除外したい単語（完全一致）を指定、複数の場合はコンマ区切り | |
| DEBUG_MODE | 集計のみ行い、チャンネルへの投稿を行わない場合に true を設定 | true |

例えば、FROM_DAYS=8, TO_DAYS=1で8日前から1日前までの投稿を探索対象にできます。

### 準備
```sh
yarn install
yarn build
```

### 実行
```sh
yarn run start
```

## Slack API
### 必要な権限
いずれもbotトークンとして

- channels.join
- channels.read
- channels.history
- chat.write
- chat.write.customize

### 使用するAPIメソッド

- [conversations.list](https://api.slack.com/methods/conversations.list)
- [conversations.history](https://api.slack.com/methods/conversations.history)
- [conversations.join](https://api.slack.com/methods/conversations.join)
- [chat.postMessage](https://api.slack.com/methods/chat.postMessage)
- [chat.getPermalink](https://api.slack.com/methods/chat.getPermalink)
