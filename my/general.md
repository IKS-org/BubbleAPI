## ユーザ
### 自分の情報の取得
```
GET my/
```
#### 詳細
`GET /bundled/prefetch`の、アカウントに直接的に係る部分のデータが返却される。
#### パラメータ
既定値
#### 返却例
(省略)

### 警告の取得
```
GET my/warning
```
#### パラメータ
既定値

#### 返却例
```
{
    "contents" : {
        public_fg: true
        title: "お客様の位置登録に関する警告"
    }
}
```
#### 備考
`public_fg`とあることから内部的には利用規約違反行為が疑われるユーザは非公開ながら予めマークされていることが推測できる。

### 所持アイテムの取得
```
GET my/items
```

#### パラメータ
このAPIは既定値に加えURLパラメータで取得したいアイテムのカテゴリ等を指定する。
|名前|値|
|:-:|:-:|
|category|partner_hp_recover, scout_ticket, coupon, versionup_chip, radar, rapacity, exp_enhancer, gacha_ticket, dasher_lottery_ticket, license, festa, slot_extender, no_effect, fair|
|fields|campain, can_buy ...|

#### 返却例
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
