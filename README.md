# HomeTvPi

2018/11/23 に作った環境の備忘録。よくわかんないで作ってるんでメモっておく。

## 雑感
- リアルタイム視聴は TVTest でする。TVTest 使いやすい　:smile:
- 録画は chinachu で行う。保存形式は chinachu では一般的(?) な m2ts 形式で保存。
- chinachu の番組表がとても使いやすい　:smile:
- 録画の閲覧は、Chinachu の wui から m2ts 形式のストリーミング閲覧可能なURLが記載された XSPF ファイルをダウンロード、VLC プレイヤーで再生してる。 :scream:  
chinachu は m2ts, mp4, WebM のコンテナ形式でストリーミングダウンロードできるが、mp4, WebM の場合 m2ts からのリアルタイム変換が必要で、raspi が非力なので変換プログラムの ffmpeg が CPU を食いまくる ＆ まともに閲覧できなかった。
- TODO: 録画終了後、m2ts から mp4 に変換するスケジューラー仕込む。chinachu wui から、変換後ファイルをストリーミングダウンロードできるようにしたい。:heart:
- TODO: もう１，２本チューナーがほしい（２，３本までなら大丈夫そう  
[ラズパイ3B\+ を地上波8ch全録サーバにできるか試してみました \- Qiita](https://qiita.com/Daigorian/items/165dd3d46663d5ddf6e0)

## サーバ環境(raspi)
- PC: Raspberry Pi 3 Model B(not +)  
- OS: RASPBIAN STRETCH LITE
- ICカード リーダーライター ACR39-NTTCom
- tuner: PX-S1UD V2.0
- B-CAS カードは以前使っていた TV のもの

## クライアント環境(windows)
- Windows 10
- TVTest 0.9.0
- BonDriver_Mirakurun

## サーバ環境の構築
基本 [ラズパイ3B\+ を地上波8ch全録サーバにできるか試してみました \- Qiita](https://qiita.com/Daigorian/items/165dd3d46663d5ddf6e0) 通り。

tuner は、PX-S1UD なので以下を参考にする。  
[Raspberry Pi 3\+Chinachuで地デジ録画サーバー構築 \- Qiita](https://qiita.com/shotasano/items/3809b8f3e0b62d51d3c3#%E3%83%81%E3%83%A5%E3%83%BC%E3%83%8A%E3%83%BC%E3%81%AE%E6%BA%96%E5%82%99)

最初は上記リンクに紹介されている 録画コマンド 
[recdvb \- Qiita](https://qiita.com/shotasano/items/3809b8f3e0b62d51d3c3#%E9%8C%B2%E7%94%BB%E7%94%A8%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB) を利用していたが、dvb-tools をインストールすると入る dvbv5-zap を使用することにより以下が改善した。  
- 録画したファイルを chinachu wui 経由で、 m2ts ストリーミング再生する時、dvbv5-zap を利用するほうが安定する。
- TVTest で チャネルスキャンをすると、recdvb だと失敗したが dvdb5-zap では成功した。

## クライアント環境の構築
### TVTest 0.9.0 のビルド
TVTest 0.9.0 は、github からもろもろソースをあつめて Visual Studio 2017 でビルドしていく。以下に従ってビルドしていく。自分は x64 でやってるくらい  
[TVTest0\.9\.0をVS2017でビルドする](https://enctools.com/tvtest-vs2017-build/)  
記事内の「ソリューション操作の再ターゲット」時に、プラットフォームツールセット「v141へのアップグレード」ドロップダウンリストがでない場合は Visual Studio 2017 のコンポーネント足りてないのでインストラーの個別コンポーネントから足す（なにか忘れたけどそれっぽい名前のやつ）

### BonDriver_Mirakurun の入手
[Releases · Chinachu/BonDriver\_Mirakurun](https://github.com/Chinachu/BonDriver_Mirakurun/releases) から最新版 v1.5 を入手し、TVTest フォルダのルートディレクトリに BonDriver_Mirakurun.dll, ホスト名を変えた BonDriver_Mirakurun.ini を配置する

### TVTest の設定
設定も EncTools 様の記事の [TVTest0\.9\.0の設定](https://enctools.com/tvtest-settings/) を参照。









