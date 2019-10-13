Raspberry Pi 3 Model B で
raspbian buster で、chinachu 環境を構築します。

[Home · Chinachu/Chinachu Wiki](https://github.com/Chinachu/Chinachu/wiki)

# 目次
1. [Raspberrypi のディスク作成～接続](./1_SetupDisk.md)
2. [Raspberrypi の初期設定](./2_InitPi.md)
3. [チューナーを利用できるようにする](./3_SetupTuner.md)
4. [mirakurun, chinachu セットアップ](./4_SetupChinachu.md)
5. [TVTestビルド・接続](./5_Tvtest.md)

9. [Pi 3, Pi 4 の比較](./9_Performance.md)

# 出来るようになったこと
- PC/iPhone から、chinacchu Web インターフェース を使用したライブ視聴(但し M2TS・無変換・無変換)
- chinachu での予約録画、録画動画の視聴。(但し M2TS・無変換・無変換)
- TVTest でのライブ視聴

※ストリーミング再生プレーヤーは、m2ts対応してる VLCを利用。
※コーデックで無変換以外を指定するとまともに再生できない。負荷がかかりCPUが100%に近くなる。

# OS (Raspbian Buster Lite)
Raspbian Buster Lite
- Minimal image based on Debian Buster
- Version:September 2019
- Release date:2019-09-26
- Kernel version:4.19

# Raspberry Pi 3 Model B (not +)
- ICカードリーダー: ACR39-NTTCom
- B-CAS カード
- チューナー: PX-S1UD V2.0
- SDカード: Transcend microSDHCカード 32GB Class10 UHS-I

# Raspberry Pi 4 Model B (4GB) 
- ICカードリーダー: ACR39-NTTCom
- B-CAS カード
- チューナー: PX-S1UD V2.0
- SCカード: Samsung microSDカード32GB EVOPlus Class10 UHS-I
