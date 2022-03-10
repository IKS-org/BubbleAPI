# bubbleAPI document

## 概要
[駅メモ! Our-Rails](https://game.our-rails.ekimemo.com/)のAPIの仕様について既知のものを纏める。  
エンドポイントのURIは、全てに共通する`https://game.our-rails.ekimemo.com/api`は省略する。

## ヘッダ & 基本パラメータ
- 原則全てのリクエストに以下のヘッダを必要とする。  
    ```
    x-csrf-token: <アカウントトークン>
    x-requested-with: XMLHttpRequest
    ```
    アカウントトークンはCookieに保存されている`csrf_token`の値を利用する。この値は不定期に強制リセットが掛かるが、利便性の担保のためにかなり長期間、同一の値を利用することができる。  

- 原則全てのリクエストに以下のURLパラメータを必要とする。  
    ```
    ?__t=[リクエスト発行時のUNIX時 ミリ秒]&__os_id=[端末識別情報]
    ```
    `__os_id`の値については、次の`総合情報の取得`の項を参照されたし。なお、このパラメータは正しく指定せずともAPIは期待されるレスポンスを返却する。
- 上記2つは以後、要求本文やパラメータの説明において「既定値」と記す。

## 目次
- 未分類
    - [総合](general.md)
- ユーザ
    - [総合](/my/general.md)
    - [マップ](/my/map)
