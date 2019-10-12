mirakurun, chinachu セットアップ

# node.js 環境の用意
node.js バージョンは　[Gamma Installation V2 · Chinachu/Chinachu Wiki](https://github.com/Chinachu/Chinachu/wiki/Gamma-Installation-V2) を参考に、 v10 とする。

```sh
$ sudo apt-get install build-essential curl git-core vainfo

# nodejs v10 があるパッケージリポジトリ追加
$ curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -

# nodejs install
$ sudo apt-get install nodejs

# pm2 install
$ sudo npm install pm2 -g
$ sudo pm2 startup
```

# 録画用コマンドが含まれる dvb-tools インストール
mirakurun で利用する録画コマンド dvbv5-zap が含まれる dvb-tools をインストール
```
$ sudo apt-get install dvb-tools
```

周波数設定ファイルダウンロード
```sh
$ cd /usr/local
$ sudo git clone https://github.com/Chinachu/dvbconf-for-isdb.git
$ cat /usr/local/dvbconf-for-isdb/conf/dvbv5_channels_isdbt.conf
```

# decoder インストール
```
$ sudo npm install arib-b25-stream-test -g --unsafe
```

# mirakurun インストール
```sh
# Quick
$ sudo npm install mirakurun -g --unsafe-perm --production
```
mirakurun-server が deamon 化される。

## 設定
設定ファイルは /usr/local/etc/mirakurun に配置される
### tuners
```
$ sudo mirakurun config tuners
以下を最後に追加

- name: PX-S1UD-1
  types:
    - GR
  command: dvbv5-zap -a 0 -c /usr/local/dvbconf-for-isdb/conf/dvbv5_channels_isdbt.conf -r -P <channel>
  dvbDevicePath: /dev/dvb/adapter0/dvr0
  decoder: arib-b25-stream-test
  isDisabled: false
```
mirakurun 再起動
```sh
$ sudo mirakurun restart
```

### channels
mirakurun にチャネルスキャンをさせる。
局名出るまで、何度かmirakurunのインストールをトライする必要あり。
```sh
$ curl -X PUT "http://localhost:40772/api/config/channels/scan"
```
参考: [Mirakurun/Platforms\.md at master · Chinachu/Mirakurun](https://github.com/Chinachu/Mirakurun/blob/master/doc/Platforms.md)  
参考: [ラズパイ３ に chinachu\-γ ＋ Mirakurun ＋ Samba で超廉価なTV録画サーバーが出来た！！、追加ハードは外付HD、USB\-TVチューナー、B\-CAS読取機 \- ラズパイ って何だべ～？ 私設 基板実験室](https://www.m-miura.tech/entry/2018/11/08/015347)


# chinachu γ インストール
```sh
$ git clone git://github.com/kanreisa/Chinachu.git ~/chinachu
$ cd ~/chinachu/
$ ./chinachu installer
# Auto を選択 (ARM の場合は Node.js のインストールはできません)
```

## config.json
chinachu の設定ファイル

```sh
$ cp config.sample.json config.json
$ vim config.json
以下の部分を変更
  "uid": "pi"
  "recordedDir" : "/mnt/hdd1/shared/recorded/"
```
# rule.json

```sh
$ echo [] > rules.json
```

## 動作テスト
```sh
$ ./chinachu service wui execute
# 問題なく起動できたらCtrl+\で終了

$ ./chinachu update
# EPG取得テスト（エラーが出た場合は恐らく Mirakurun に接続できていません）
```

## サービス化
```sh
$ sudo pm2 start processes.json
# 実行すると「Interpreter .nave/node is NOT AVAILABLE in PATH.」というエラーが発生する
# process.json の "exec_interpreter": ".nave/node", の行を削除する
# chinachu auto でインストールできる環境だと、 nave が自動インストールされるのでうまくいくのかも？

$ sudo pm2 save
```

## ffmpeg
chinachu に同封される ffmpeg は、arm 用ではないのでインストールして
chinachu の利用する ffmpeg 向き先を調整する。
ffmpeg は、chinachu wui(Web User Interface) の番組のサムネイル生成で多分使われていたいます。
```sh
$ sudo apt-get install ffmpeg

# ffmpeg 入替
$ cd ~/chinachu/usr/bin

$ mv ffmpeg ffmpeg.bak
$ mv ffprobe ffprobe.bak
$ mv qt-faststart qt-faststart.bak

$ ln -s /usr/bin/ffmpeg ./ffmpeg
$ ln -s /usr/bin/ffprobe ./ffprobe
$ ln -s /usr/bin/qt-faststart ./qt-faststart
```
