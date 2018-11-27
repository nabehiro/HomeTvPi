# HomeTvPi

2018/11/23 に作った環境の備忘録。よくわかんないで作ってるんでメモっておく。

## 雑感
- リアルタイム視聴は TVTest でする。TVTest 使いやすい　:smile:
- 録画は chinachu で行う。保存形式は chinachu では一般的(?) な m2ts 形式で保存。
- chinachu の番組表がとても使いやすい　:smile:
- 録画の閲覧は、Chinachu の wui から m2ts 形式のストリーミング閲覧可能なURLが記載された XSPF ファイルをダウンロード、VLC プレイヤーで再生していて面倒。。 :scream:  
chinachu は m2ts, mp4, WebM のコンテナ形式でストリーミングダウンロードできるが、mp4, WebM の場合 m2ts からのリアルタイム変換が必要で、raspi が非力なので変換プログラムの ffmpeg が CPU を食いまくる ＆ まともに閲覧できなかった。

## 改善点 :heart:
- もう１，２本チューナーがほしい（２，３本までなら大丈夫そう [ラズパイ3B\+ を地上波8ch全録サーバにできるか試してみました \- Qiita](https://qiita.com/Daigorian/items/165dd3d46663d5ddf6e0)
- m2ts をもろもろデフォルトにする

## サーバ環境(raspi)
- Raspberry Pi 3 Model B(not +)  
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

### 録画コマンド
tuner は、PX-S1UD なので以下を参考にする。  
[Raspberry Pi 3\+Chinachuで地デジ録画サーバー構築 \- Qiita](https://qiita.com/shotasano/items/3809b8f3e0b62d51d3c3#%E3%83%81%E3%83%A5%E3%83%BC%E3%83%8A%E3%83%BC%E3%81%AE%E6%BA%96%E5%82%99)

最初は上記リンクに紹介されている 録画コマンド 
[recdvb \- Qiita](https://qiita.com/shotasano/items/3809b8f3e0b62d51d3c3#%E9%8C%B2%E7%94%BB%E7%94%A8%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB) を利用していたが、dvb-tools をインストールすると入る dvbv5-zap を使用することにより以下が改善した。  
- 録画したファイルを chinachu wui 経由で、 m2ts ストリーミング再生する時、dvbv5-zap を利用するほうが安定する。
- TVTest で チャネルスキャンをすると、recdvb だと失敗したが dvdb5-zap では成功した。

### ffmpeg, ffprobe...
chinachu に同梱されている動画変換ソフトの ffmpeg は、
[Chinachu/chinachu at 09edc70e6a952c130ca294a6ea3c1607653bf08c · Chinachu/Chinachu](https://github.com/Chinachu/Chinachu/blob/09edc70e6a952c130ca294a6ea3c1607653bf08c/chinachu#L178) にあるように
[FFmpeg Static Builds](https://www.johnvansickle.com/ffmpeg/) から取得している。installer が取得している ffmpeg は、arm である raspberry pi 3 では利用できないビルドなので arm x86 用(armhf: ffmpeg-release-armhf-static.tar.xz)の ビルドを取得して chinachu/usr/bin 内のファイルを置換ないしシンボリックリンクを作成すればよい。 これで、chihachu wui 上で ストリーム再生はできるようになる。    
参考: [Raspbian\(Raspberry PI 0/1/2/3\)にFFmpeg 4\.x を導入するには \- Qiita](https://qiita.com/hirohiro77/items/14ca3ad0c593fc4990af)

[Raspberry Pi 3 Model Bで動画処理アプリ FFmpegをコンパイルする方法 \(ラズパイ３で動画音声変換処理プログラム FFmpegをセルフコンパイルしてインストールする方法\)](http://www.neko.ne.jp/~freewing/raspberry_pi/raspberry_pi_3_compile_ffmpeg/)

[Raspberry Pi 3でx264とハードウエアエンコーダが使えるFFmpegをビルドする](https://signal-flag-z.blogspot.com/2017/05/raspberry-pix264ffmpeg.html)

## クライアント環境の構築
### TVTest 0.9.0 のビルド
TVTest 0.9.0 は、github からもろもろソースをあつめて Visual Studio 2017 でビルドしていく。以下に従ってビルドしていく。自分は x64 でやってるくらい  
[TVTest0\.9\.0をVS2017でビルドする](https://enctools.com/tvtest-vs2017-build/)  
記事内の「ソリューション操作の再ターゲット」時に、プラットフォームツールセット「v141へのアップグレード」ドロップダウンリストがでない場合は Visual Studio 2017 のコンポーネント足りてないのでインストラーの個別コンポーネントから足す（なにか忘れたけどそれっぽい名前のやつ）

### BonDriver_Mirakurun の入手
[Releases · Chinachu/BonDriver\_Mirakurun](https://github.com/Chinachu/BonDriver_Mirakurun/releases) から最新版 v1.5 を入手し、TVTest フォルダのルートディレクトリに BonDriver_Mirakurun.dll, ホスト名を変えた BonDriver_Mirakurun.ini を配置する

### TVTest の設定
設定も EncTools 様の記事の [TVTest0\.9\.0の設定](https://enctools.com/tvtest-settings/) を参照。









