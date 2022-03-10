## 未分類

### 総合情報の取得
```
GET /bundled/prefetch
```

#### 詳細
ユーザ情報を含む総合情報を取得する。  
このAPIのみ正規のアプリにおいても`__os_id`の値を付加せず呼び出している。即ち、このAPIを一番最初に呼び出すべきだと考えられる。  

#### 返却例
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
#### 備考
- ユーザのゲーム内設定、編成情報、ユーザ情報、アプリ版用と思われる定期購読フラグなどの情報が返る。`festa`の値はアワメモの「フェス」ではなく「イベント」であることに注意。
- `contents.owner.platform.id`が先述した端末識別情報である。

### ログインの実行
```
GET /actions/login
```
#### 備考
- 返却値はない。

