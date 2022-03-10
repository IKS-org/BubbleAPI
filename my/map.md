## マップ
### 全駅座標の取得
```
GET my/map/all_station
```
#### 詳細
全駅の座標を取得する。駅名との紐付けにはIDを参照する。

#### パラメータ
既定値
#### 返却例  
```
{
  "contents": {
    "locations": [
      0: {
        "id": 9103,
        "lat": 26.193289,
        "lng": 127.660348,
      },
      ...
    ]
  }
}
```

### 都道府県別アクセス状況の取得
```
GET my/map/station_status
```
#### 詳細
全都道府県の座標及び各都道府県ごとの駅アクセス状況を取得する
#### パラメータ
既定値
#### 返却例
```
{
  "contents": {
    "accessed_prefecture_count": {
      "max": 47,
      "current": 0,
    },
    "accessed_station_count": {
      "max": 9334,
      "current": 0,
    },
    "locations": [
      0:{
        "status": "prefecture_detail",
        "pref_id": 1,
        "lat": 43.068612,
        "lng": 141.350768,
        "prefecture": {
          "accessed_station": 0,
          "name_ja": "北海道",
          "total_station": 560
        }
      },
      ...
    ]
  }
}
```

### 付近の駅のアクセス状況の取得
```
POST my/map/station/near_station_status
```
#### パラメータ
既定値

#### 要求本文
|名前|タイプ|説明|例|
|:-:|:-:|:-:|:-:|
|station_id_list|配列|駅IDを文字列で列挙する。マップの拡大率によって要素数は変動する。|["1", "2", "3"]|

#### 返却例
```
{
  "contents": {
    "locations": [
      {
        "id": 1,
        "status": "new_station"
      },
      ...
    ]
  }
}
```

#### 備考
「付近の駅のアクセス状況」とは実際に利用されている用途とエンドポイントからそのように呼称しているだけであり、実際には要求本文の通りステータスを取得したい駅IDを列挙してリクエストするため、位置情報とは関係がない。
