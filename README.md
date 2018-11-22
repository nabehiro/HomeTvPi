# HomeTvPi

2018/11/23 に作った環境のメモ。

## 雑感
- リアルタイム視聴は TVTest でする。TVTest 使いやすい。
- 録画は chinachu で行う。保存形式は chinachu では一般的(?) な m2ts 形式で保存。
- 録画の閲覧は、Chinachu の wui から ストリーミング視聴で今はしてる。  
chinachu は m2ts, mp4, WebM のコンテナ形式でストリーミングダウンロードできるが、mp4, WebM は m2ts からの変換がリアルタイムで必要で、
raspi が非力なので変換プログラムの ffmpeg が CPU を食いまくる ＆ まともに閲覧できなかった。
- TODO: 録画終了後、m2ts から mp4 に変換するスケジューラー仕込む。chinachu wui から、変換後ファイルをストリーミングダウンロードできるようにしたい。
- TODO: もう１，２本チューナーがほしい（２，３本までなら大丈夫そう  
[ラズパイ3B\+ を地上波8ch全録サーバにできるか試してみました \- Qiita](https://qiita.com/Daigorian/items/165dd3d46663d5ddf6e0)

## 環境

