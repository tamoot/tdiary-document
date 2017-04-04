# 概要

GoogleMapを埋め込みます。GoogleでのAPIキー等は不要です。

以下2つの使い方があります。

- 緯度、経度を指定
- 住所または地名を指定


利用の際には、プレビュー画面での確認をお勧めします。（・∀・）

# 設置方法

1. contribから取得し、プラグインディレクトリに配置ください。
2. 設定画面で有効にしてください。

# 使い方

## 緯度、経度を指定する場合

```
 {{google_map '36.695952', '137.213677'}}
 <%= google_map '36.695952', '137.213677' %>
```

## 住所または地名を指定する場合

```
 {{google_geomap '羽田空港'}}
 <%= google_geomap '羽田空港' %>
```

## オプションを追加する場合

- 本プラグインに指定可能な最後の引数はHashとなっています。
- 省略可能です。google_map, google_geomapともに、同じオプションを指定可能です。


| シンボル | 指定する値について |
|---------|-----------------|
| `:title`   | Map中のマーカーに設定するタイトル。
| `:html`    | マーカーをクリックした際に表示される吹き出し中のhtml要素。:titleとペアで指定してください。
| `:zoom`    | GoogleMapに指定する倍率 1～16までを指定します。数字が大きいと縮尺が小さくなります。デフォルト:10
| `:width`  | 埋め込まれるGoogleMapの幅 [pixel]、デフォルト:320
| `:height`  | 埋め込まれるGoogleMapの高さ幅 [pixel]、デフォルト:240
| `:type`    | 初期表示の地図のタイプを指定可能です。シンボルを指定してください。値のチェックはしていません。 デフォルト: '':ROADMAP''
| `:overview` | オーバービュー領域を右隅に表示します。表示させたい場合は :overview => true と指定してください。

* `:type` には下記を指定可能です。( [参考](http://code.google.com/intl/ja/apis/maps/documentation/javascript/introduction.html#MapOptions) )

| 値 | 説明 |
|----|------|
| :ROADMAP   | displays the normal, default 2D tiles of Google Maps. | 
| :SATELLITE | displays photographic tiles.| 
| :HYBRID    | displays a mix of photographic tiles and a tile layer for prominent features (roads, city names). | 
| :TERRAIN   | displays physical relief tiles for displaying elevation and water features (mountains, rivers, etc.). | 


### オプション付きの使用例1

* 本当は一行です。

```
 {{google_map '36.695952', '137.213677', :title => '富山市役所', 
  :html => '<a href="http://www3.city.toyama.toyama.jp/machikado/genre/g13_s.asp?0009">展望台</a>いってきました', 
  :zoom => 10, :width => 400, :height => 300}}
```

### オプション付きの使用例2

* 本当は一行です。

```
 {{google_geomap 'フューチャーシティファボーレ', :zoom => 14, 
 :title => 'ファボーレ!', :html => '<a href="http://www.favore.jp/">アル・プラザ富山と100の専門店<br/>フューチャー シティー『ファボーレ』</a>', 
 :width => 500, :height => 500}}
```

![](http://farm2.static.flickr.com/1263/5122766352_f11ffd2bb7.jpg)

### オプション付きの使用例3

* 本当は一行です。

```
 {{google_map '36.6971', '137.2135', :zoom => 14, 
 :title => 'とやましやくしょ', :width => 500, :height => 500, :overview => true}}
```

![](http://farm7.static.flickr.com/6205/6116056737_cd45a47728_o.png)

# その他

* 以下のようにスタイルシートで位置を調整可能です。

```css
 div.gmap {
   margin-left: 2em;
 }
```


# 注意

## 住所・地名を指定する場合

* Google側で緯度経度に変換できなかった場合は、alertを表示します。プレビュー等で確認するようにしてください。

### 文字コードの問題

tDiary2.3以降のUTF8環境でないと、住所地名に日本語が利用できない恐れがあります。

大変申し訳ありませんが、古いtDiary + EUC-JP環境では試していませんm(_ _)m

### 同時呼び出しにおける Google Map API側の制限

* http://code.google.com/intl/ja/apis/maps/faq.html#geocoder_limit

試していたところ、1つの日記セクション中に 6つ以上のgeocodeリクエストを送ると、6個目がエラーとなってしまいました。
あまり利用しすぎないようにしてくださいm(_ _)m
