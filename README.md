# bubbleAPI document

## 概要
[駅メモ! Our-Rails](https://game.our-rails.ekimemo.com/)のAPIの仕様について既知のものを纏める。  
エンドポイントのURIは、全てに共通する`https://game.our-rails.ekimemo.com/api`は省略する。

## ヘッダ
- 原則全てのリクエストに以下のヘッダを必要とする。  
    ```
    x-csrf-token: <アカウントトークン>
    x-requested-with: XMLHttpRequest
    ```
    アカウントトークンはCookieに保存されている`csrf_token`の値を利用する。この値は不定期に強制リセットが掛かるが、利便性の担保のためにかなり長期間、同一の値を利用することができる。  

- 原則全てのリクエストに以下のURLパラメータを必要とする。  
    ```
    ?__t=<リクエスト発行時のUNIX時 ミリ秒>&__os_id=<端末識別情報>
    ```
    `__os_id`の値については、次の`総合情報の取得`の項を参照されたし。なお、このパラメータは正しく指定せずともAPIは期待されるレスポンスを返却する。

## ユーザ系

### 総合情報の取得
```
GET /bundled/prefetch
```
以下のようなJSONが返却される。

```
{
    "contents": {
        "partner_list": [ ... ]
        "app": {
            "platform": "pwa",
            "yoshiko_style": "tiger",
            "features": { ... },
            "app_version": null,
            "firebase_config": { ... },
            "device_info": {
                "version": "10",
                "type": "ios"
            },
            "environment": {
                "user": "mf",
                "type": "production"
            }
        },
        "background": {
            "image_key": "building",
            "animation_key": "train"
        },
        "owner": {
            "user_id": 0,
            "login_continue": 0,
            "created_at": "20XX-XX-XX 00:00:00",
            "exp_booster": {
                "id": 125,
                "name": "レベルグングン",
                "effective_amount": 120,
                "effect_end_at": "20XX-XX-XX XX:XX:XX"
            },
            "energy_rest": 12,
            "partner": {
                "name_en": "rara",
                "name": "らら",
                "dress": "default",
                "theme_color": "orange"
            },
            "level": {
                "current": 0,
                "max": 400
            },
            "is_novice": false,
            "platform": {
                "id": ""
            },
            "today_checkin_count": 0,
            "friend": {
                "current": 0,
                "max": 0
            },
            "tutorial_finished_at": "20XX-XX-XX XX:XX:XX",
            "awarded_count": 0,
            "today_report": {
                "access_station_count": 0,
                "moved_distance": 0
            },
            "beginner_license_end_at": null,
            "total_score": 0,
            "outing_campaign_fg": true,
            "total_rank": "0",
            "comeback_fg": false,
            "name": "",
            "festa_radar_campaign": {
                "end_at": null
            },
            "license_end_at": "20XX-XX-XX XX:XX:XX",
            "login_total": 0,
            "exp_enhancer_count": 0,
            "review": null,
            "unread_news": [],
            "comment": "",
            "last_login_at": "20XX-XX-XX XX:XX:XX",
            "is_subscribed": false,
            "master_id": "XXXXXXXXXX",
            "rapacity_count": 0,
            "keep_station": 17,
            "visual_license_end_at": null,
            "achievement": {
                "name": "めげない気持ち",
                "count": 151
            },
            "subscription": {
                "auto_renewing_fg": false,
                "device_type": "ios",
                "expire_at": null,
                "is_free_trial": false,
                "refunded_at": null,
                "status_name_ja": "未購読",
                "status": "unsubscribed",
                "canceled_at": null,
                "user_id": 251191,
                "purchased_at": null,
                "is_subscribed": false
            }
        },
        "festa": [ ... ],
        "spot_count": {
            "near_spot_count": 0
        },
        "festa_informations": null,
        "banners": [ ... ],
        "ticker_board": {
            "message": "ようこそ！ 駅メモ！ Our Rails の世界へ"
        },
        "global_navi_banners": [
            {
                "key": "bnr_whats_nft",
                "state": "https://our-rails.ekimemo.com/station-owner/about-station-nft"
            }
        ],
        "winning_lottery": null,
        "matomete_app_list": []
    }
}
```
- ユーザのゲーム内設定、編成情報、ユーザ情報、アプリ版用と思われる定期購読フラグなどの情報が返る。`festa`の値はアワメモの「フェス」ではなく「イベント」であることに注意。
- `contents.owner.platform.id`が先述した端末識別情報である。

### ログインの実行
```
GET /actions/login
```
- 返却値はない。

### 自分の情報の取得
```
GET my/
```
- `GET /bundled/prefetch`の、アカウントに直接的に係る部分のデータが返却される。

### 警告の取得
```
GET my/warning
```
以下のようなJSONが返却される
```
{
    "contents" : {
        public_fg: true
        title: "お客様の位置登録に関する警告"
    }
}
```
- `public_fg`とあることから内部的には利用規約違反行為が疑われるユーザは非公開ながら予めマークされていることが推測できる。

### 所持アイテムの取得
```
GET my/items
```
このAPIはURLパラメータで取得したいアイテムのカテゴリ等を指定する。
|キー名|値|
|:-:|:-:|
|category|partner_hp_recover, scout_ticket, coupon, versionup_chip, radar, rapacity, exp_enhancer, gacha_ticket, dasher_lottery_ticket, license, festa, slot_extender, no_effect, fair|
|fields|campain, can_buy ...|

以下のようなJSONが返却される
```
{
    "contents" : [
        campaign: null
        can_buy: false
        category: "scout_ticket"
        count: 0
        description: ""
        description_divided_fg: false
        effective_amount: 0
        effective_amount_label: null
        effective_seconds: 0
        id: 215
        modal_force_display_fg: false
        name: "ゆるキャン△スカウトチケット"
        name_en: "yurucamp_scout_ticket"
        order_num: 1
    ]
}
```
