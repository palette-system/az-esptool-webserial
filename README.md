# 説明
自分がコンパイルしたbinファイルをChrome の Web Serial 経由でESPに書込みを行うライブラリです。

サーバー上にアップすれば、binファイルをダウンロードせずにブラウザから直接ファームウェアの書き込みが行えます。

- WEBサーバー上にbinファイルとjsを置くだけ
- シリアル通信の速度をパラメーターで指定できる
- 書込み終了後ESPの再起動をする
- ファイルではなくbinコンバーターでコンバートしたJSファイルを書き込むこともできる

<br>

# 動作サンプル

ライターサンプル
　　https://azkey.jp/az-esptool-webserial/

binファイルコンバーター
　　https://azkey.jp/az-esptool-webserial/bin_converter.html

<br>

# 使い方

１．Adafruit_WebSerial_ESPTool のリポジトリから下記をダウンロードしてサーバーに設置します

https://github.com/adafruit/Adafruit_WebSerial_ESPTool

- js/esptool.js
- js/utilities.js
- stubs/ の下全て

２．az-esptool-webserial のリポジトリの下記ファイルもサーバーの同じディレクトリに設置します

- js/az_esploader.js
- data/ の下全て


３．writer.html の 45行目の espTool.writeFlash に書き込みたいファイルのパスとアドレスを指定します

```
await espTool.writeFlash([
	{"address": 0x8000, "data": "./data/m5stac_lcd_test.ino.partitions.bin"},
	{"address": 0x10000, "data": "./data/m5stac_lcd_test.ino.bin"}
], 921600);
```

４．書き終えたらファイル名を index.html に変更してサーバー上の同じディレクトリに設置します。

以上で、設置完了です。

<br>

# パターン別書き方

■　一つだけの例
```
await espTool.writeFlash([
	{"address": 0x8000, "data": "./data/m5stac_lcd_test.ino.partitions.bin"}
], 921600);
```

■　転送速度 115200 にする例
```
await espTool.writeFlash([
	{"address": 0x8000, "data": "./data/m5stac_lcd_test.ino.partitions.bin"}
], 115200);
```

■　bin converter でファイルではなくjsのソース上に書いたファイルを指定する

　(作成したjsをHTMLヘッダで<script src=""></script>で読み込んでおく )
```
await espTool.writeFlash([
	{"address": 0x8000, "data": m5stac_lcd_test_ino_bin}
], 115200);
```

<br>

# 必要なライブラリ

■　Adafruit_WebSerial_ESPTool

https://github.com/adafruit/Adafruit_WebSerial_ESPTool
