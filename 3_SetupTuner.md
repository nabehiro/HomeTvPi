チューナーを利用できるようにする

# ICカードリーダーのセットアップ(ACR39-NTTCom)
```
$ sudo apt-get install pcscd libpcsclite-dev libccid pcsc-tools
```

ICカードリーダーをUSB接続して、B-CASカードが認識されているか確認
```
$ pcsc_scan
Using reader plug'n play mechanism
Scanning present readers...
0: ACS ACR39U ICC Reader 00 00

Fri Oct 11 23:16:58 2019
 Reader 0: ACS ACR39U ICC Reader 00 00
  Event number: 0
  Card state: Card inserted,
  ATR: 3B F0 12 00 FF 91 81 B1 7C 45 1F 03 99

ATR: 3B F0 12 00 FF 91 81 B1 7C 45 1F 03 99
+ TS = 3B --> Direct Convention
+ T0 = F0, Y(1): 1111, K: 0 (historical bytes)
  TA(1) = 12 --> Fi=372, Di=2, 186 cycles/ETU
    21505 bits/s at 4 MHz, fMax for Fi = 5 MHz => 26881 bits/s
  TB(1) = 00 --> VPP is not electrically connected
  TC(1) = FF --> Extra guard time: 255 (special value)
  TD(1) = 91 --> Y(i+1) = 1001, Protocol T = 1
-----
  TA(2) = 81 --> Protocol to be used in spec mode: T=1 - Unable to change - defined by interface bytes
  TD(2) = B1 --> Y(i+1) = 1011, Protocol T = 1
-----
  TA(3) = 7C --> IFSC: 124
  TB(3) = 45 --> Block Waiting Integer: 4 - Character Waiting Integer: 5
  TD(3) = 1F --> Y(i+1) = 0001, Protocol T = 15 - Global interface bytes following
-----
  TA(4) = 03 --> Clock stop: not supported - Class accepted by the card: (3G) A 5V B 3V
+ Historical bytes:
+ TCK = 99 (correct checksum)

Possibly identified card (using /usr/share/pcsc/smartcard_list.txt):
3B F0 12 00 FF 91 81 B1 7C 45 1F 03 99
        Japanese Chijou Digital B-CAS Card (pay TV)
 |
```

カードリーダーに刺しているカードが
`Japanese Chijou Digital B-CAS Card (pay TV)` と認識されればよい。

参考: [年末年始に向けて家電作りに挑戦してみる \- Qiita](https://qiita.com/norifumi/items/b3e0419468cf9c9022cd#ic-%E3%82%AB%E3%83%BC%E3%83%89%E3%83%AA%E3%83%BC%E3%83%80%E3%83%BC)

# チューナーのセットアップ(PX-S1UD V2.0)
チューナーを接続する。
最初セルフパワーのUSBハブにチューナーを接続していたが
ストリーミングの品質が低かったので本体に直接刺したところ安定するようになった。

```
$ wget http://plex-net.co.jp/plex/px-s1ud/PX-S1UD_driver_Ver.1.0.1.zip
$ unzip PX-S1UD_driver_Ver.1.0.1.zip
$ sudo cp PX-S1UD_driver_Ver.1.0.1/x64/amd64/isdbt_rio.inp /lib/firmware/
```

参考: [Raspberry Pi 3\+Chinachuで地デジ録画サーバー構築 \- Qiita](https://qiita.com/shotasano/items/3809b8f3e0b62d51d3c3#%E3%83%81%E3%83%A5%E3%83%BC%E3%83%8A%E3%83%BC%E3%81%AE%E6%BA%96%E5%82%99)

# B-CASのデコード用ライブラリのインストール

libarib25 のビルド用にインストール
```
$ sudo apt-get install cmake g++
```

```shell
$ wget https://github.com/stz2012/libarib25/archive/master.zip
$ unzip master.zip
$ cd libarib25-master
$ cmake .
$ make
$ sudo make install
[ 55%] Built target arib25-objlib
[ 66%] Built target arib25-static
[ 77%] Built target arib25-shared
[100%] Built target b25
Install the project...
-- Install configuration: "Release"
-- Installing: /usr/local/bin/b25
-- Set runtime path of "/usr/local/bin/b25" to ""
-- Installing: /usr/local/lib/libarib25.a
-- Installing: /usr/local/lib/libarib25.so.0.2.5
-- Installing: /usr/local/lib/libarib25.so.0
-- Installing: /usr/local/lib/libarib25.so
-- Installing: /usr/local/include/arib25/arib_std_b25.h
-- Installing: /usr/local/include/arib25/b_cas_card.h
-- Installing: /usr/local/include/arib25/multi2.h
-- Installing: /usr/local/include/arib25/ts_section_parser.h
-- Installing: /usr/local/include/arib25/portable.h
-- Installing: /usr/local/include/arib25/arib25_api.h
-- Installing: /usr/local/lib/pkgconfig/libarib25.pc
-- Running: ldconfig
```

# 録画用コマンド recdvb インストール
mirakurun では利用しないがチューナーの検証が楽なのでインストールする。

recdvb のビルド用にインストール
```
$ sudo apt-get install autoconf automake
```

```
$ wget http://www13.plala.or.jp/sat/recdvb/recdvb-1.3.1.tgz
$ tar xvzf recdvb-1.3.1.tgz
$ cd recdvb-1.3.1
$ ./autogen.sh
$ ./configure  --enable-b25
$ make 
$ sudo make install
install -m 755 recdvb recdvbctl recdvbchksig /usr/local/bin
```

録画できるかテスト
```
$ recdvb --b25 --strip 24 10 test.m2ts
```



