

# Raspberry Pi 3 Model B

## Distribution
```
$ lsb_release -a
No LSB modules are available.
Distributor ID: Raspbian
Description:    Raspbian GNU/Linux 10 (buster)
Release:        10
Codename:       buster
```

## vcgencmd
```sh
# CPU温度
$ vcgencmd measure_temp
temp=60.7C

# 周波数
$ vcgencmd measure_clock arm
frequency(45)=600000000

# 電圧
$ vcgencmd measure_volts
volt=1.2000V

# CPUメモリ
$ vcgencmd get_mem arm
arm=948M

# GPUメモリ
＄vcgencmd get_mem gpu
gpu=76M
```

## UnixBench
[CPUやメモリなどのシステム性能を比較するベンチマークツール 2ページ \| さくらのナレッジ](https://knowledge.sakura.ad.jp/1048/2/)

```sh
# クローン
$ git clone https://github.com/kdlucas/byte-unixbench
$ cd byte-unixbench/UnixBench/
$ ./run
```

unixbench 後の、CPU温度=61.2C だった。  
```
=======================================================================
   BYTE UNIX Benchmarks (Version 5.1.3

   System: rasp-01: GNU/Linu
   OS: GNU/Linux -- 4.19.75-v7+ -- #1270 SMP Tue Sep 24 18:45:11 BST 201
   Machine: armv7l (unknown
   Language: en_US.utf8 (charmap="ANSI_X3.4-1968", collate="ANSI_X3.4-1968"
   CPU 0: ARMv7 Processor rev 4 (v7l) (0.0 bogomips

   CPU 1: ARMv7 Processor rev 4 (v7l) (0.0 bogomips

   CPU 2: ARMv7 Processor rev 4 (v7l) (0.0 bogomips

   CPU 3: ARMv7 Processor rev 4 (v7l) (0.0 bogomips

   18:19:09 up 9 min,  1 user,  load average: 1.21, 0.82, 0.40; runlevel Oc

-----------------------------------------------------------------------
Benchmark Run: 日 10月 13 2019 18:19:09 - 18:47:2
4 CPUs in system; running 1 parallel copy of test

Dhrystone 2 using register variables        4372535.5 lps   (10.0 s, 7 samples
Double-Precision Whetstone                     1204.0 MWIPS (9.8 s, 7 samples
Execl Throughput                                730.4 lps   (29.9 s, 2 samples
File Copy 1024 bufsize 2000 maxblocks        116432.4 KBps  (30.0 s, 2 samples
File Copy 256 bufsize 500 maxblocks           36877.5 KBps  (30.0 s, 2 samples
File Copy 4096 bufsize 8000 maxblocks        302928.7 KBps  (30.0 s, 2 samples
Pipe Throughput                              200644.4 lps   (10.0 s, 7 samples
Pipe-based Context Switching                  30082.6 lps   (10.0 s, 7 samples
Process Creation                               1184.6 lps   (30.0 s, 2 samples
Shell Scripts (1 concurrent)                    984.7 lpm   (60.0 s, 2 samples
Shell Scripts (8 concurrent)                    257.6 lpm   (60.1 s, 2 samples
System Call Overhead                         386329.3 lps   (10.0 s, 7 samples

System Benchmarks Index Values               BASELINE       RESULT    INDE
Dhrystone 2 using register variables         116700.0    4372535.5    374.
Double-Precision Whetstone                       55.0       1204.0    218.
Execl Throughput                                 43.0        730.4    169.
File Copy 1024 bufsize 2000 maxblocks          3960.0     116432.4    294.
File Copy 256 bufsize 500 maxblocks            1655.0      36877.5    222.
File Copy 4096 bufsize 8000 maxblocks          5800.0     302928.7    522.
Pipe Throughput                               12440.0     200644.4    161.
Pipe-based Context Switching                   4000.0      30082.6     75.
Process Creation                                126.0       1184.6     94.
Shell Scripts (1 concurrent)                     42.4        984.7    232.
Shell Scripts (8 concurrent)                      6.0        257.6    429.
System Call Overhead                          15000.0     386329.3    257.
                                                                   =======
System Benchmarks Index Score                                         221.

-----------------------------------------------------------------------
Benchmark Run: 日 10月 13 2019 18:47:23 - 19:15:5
4 CPUs in system; running 4 parallel copies of test

Dhrystone 2 using register variables        7298500.1 lps   (10.0 s, 7 samples
Double-Precision Whetstone                     2072.5 MWIPS (9.2 s, 7 samples
Execl Throughput                                982.4 lps   (29.8 s, 2 samples
File Copy 1024 bufsize 2000 maxblocks         92359.4 KBps  (30.0 s, 2 samples
File Copy 256 bufsize 500 maxblocks           25530.4 KBps  (30.0 s, 2 samples
File Copy 4096 bufsize 8000 maxblocks        256226.7 KBps  (30.0 s, 2 samples
Pipe Throughput                              469260.9 lps   (10.0 s, 7 samples
Pipe-based Context Switching                  70258.5 lps   (10.0 s, 7 samples
Process Creation                               3407.1 lps   (30.0 s, 2 samples
Shell Scripts (1 concurrent)                   2201.2 lpm   (60.1 s, 2 samples
Shell Scripts (8 concurrent)                    264.2 lpm   (60.5 s, 2 samples
System Call Overhead                        1680534.5 lps   (10.0 s, 7 samples

System Benchmarks Index Values               BASELINE       RESULT    INDE
Dhrystone 2 using register variables         116700.0    7298500.1    625.
Double-Precision Whetstone                       55.0       2072.5    376.
Execl Throughput                                 43.0        982.4    228.
File Copy 1024 bufsize 2000 maxblocks          3960.0      92359.4    233.
File Copy 256 bufsize 500 maxblocks            1655.0      25530.4    154.
File Copy 4096 bufsize 8000 maxblocks          5800.0     256226.7    441.
Pipe Throughput                               12440.0     469260.9    377.
Pipe-based Context Switching                   4000.0      70258.5    175.
Process Creation                                126.0       3407.1    270.
Shell Scripts (1 concurrent)                     42.4       2201.2    519.
Shell Scripts (8 concurrent)                      6.0        264.2    440.
System Call Overhead                          15000.0    1680534.5   1120.
                                                                   =======
System Benchmarks Index Score                                         354.
```

## 動画変換(m2ts => mp4)
m2ts 用意。NHKを10秒録画。
```
$ recdvb --b25 --strip 24 10 test.m2ts
```

test.m2ts の情報
```
$ ffprobe test.m2ts
...
Input #0, mpegts, from 'test.m2ts':
  Duration: 00:00:10.45, start: 50630.497722, bitrate: 14782 kb/s
  Program 1064
    Metadata: 
      service_name    : ?|���D+F|
      service_provider:
    Stream #0:0[0x111]: Video: mpeg2video (Main) ([2][0][0][0] / 0x0002), yuv420p(tv, bt709, top first), 1440x1080 [SAR 4:3 DAR 16:9], 29.97 fps, 29.97 tbr, 90k tbn, 59.94 tbc
    Stream #0:1[0x112]: Audio: aac (LC) ([15][0][0][0] / 0x000F), 48000 Hz, stereo, fltp, 192 kb/s
...
```

m2ts から mp4(映像: H.264、音声:mp3)に変換。※オプション未指定の場合と同様  
fps 2.5。動画変換に約２分かかる。
```
$ ffmpeg -i test.m2ts output.mp4 -vcodec libx264 -acodec libmp3lame
...
frame=  296 fps=2.5 q=-1.0 Lsize=    5358kB time=00:00:09.77 bitrate=4489.5kbits/s dup=24 drop=0 speed=0.0826x
video:5195kB audio:152kB subtitle:0kB other streams:0kB global headers:0kB muxing overhead: 0.210654%
...
```

output.mp4 の情報
```
$ ffprobe output.mp4
...
Input #0, mov,mp4,m4a,3gp,3g2,mj2, from 'output.mp4':
  Metadata:
    major_brand     : isom
    minor_version   : 512
    compatible_brands: isomiso2avc1mp41
    encoder         : Lavf58.20.100
  Duration: 00:00:09.88, start: 0.000000, bitrate: 4443 kb/s
    Stream #0:0(und): Video: h264 (High) (avc1 / 0x31637661), yuv420p, 1440x1080 [SAR 4:3 DAR 16:9], 4308 kb/s, 29.97 fps, 29.97 tbr, 30k tbn, 59.94 tbc (default)
    Metadata:
      handler_name    : VideoHandler
    Stream #0:1(und): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 130 kb/s (default)
    Metadata:
      handler_name    : SoundHandler
...
```

m2ts から　mp4 に変換。（オプション無し）
```
$ ffmpeg -i test.m2ts output2.mp4
...
frame=  296 fps=2.5 q=-1.0 Lsize=    5358kB time=00:00:09.77 bitrate=4489.5kbits/s dup=24 drop=0 speed=0.0841x
video:5195kB audio:152kB subtitle:0kB other streams:0kB global headers:0kB muxing overhead: 0.210654%
...
```

output2.mp4 の情報
```
$ ffprobe output2.mp4
...
Input #0, mov,mp4,m4a,3gp,3g2,mj2, from 'output2.mp4':
  Metadata:
    major_brand     : isom
    minor_version   : 512
    compatible_brands: isomiso2avc1mp41
    encoder         : Lavf58.20.100
  Duration: 00:00:09.88, start: 0.000000, bitrate: 4443 kb/s
    Stream #0:0(und): Video: h264 (High) (avc1 / 0x31637661), yuv420p, 1440x1080 [SAR 4:3 DAR 16:9], 4308 kb/s, 29.97 fps, 29.97 tbr, 30k tbn, 59.94 tbc (default)
    Metadata:
      handler_name    : VideoHandler
    Stream #0:1(und): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 130 kb/s (default)
    Metadata:
      handler_name    : SoundHandler
```

# Raspberry Pi 4 Model B (4GB)

※冷却ファン付き アルミニウム合金ケースを使用している。

## Distribution
```
$ lsb_release -a
No LSB modules are available.
Distributor ID: Raspbian
Description:    Raspbian GNU/Linux 10 (buster)
Release:        10
Codename:       buster
```

## vcgencmd
```sh
# CPU温度
$ vcgencmd measure_temp
temp=46.0C

# 周波数
$ vcgencmd measure_clock arm
frequency(48)=1500398464

# 電圧
$ vcgencmd measure_volts
volt=0.8455V

# CPUメモリ
$ vcgencmd get_mem arm
arm=948M

# GPUメモリ
＄vcgencmd get_mem gpu
gpu=76M
```

## UnixBench
```sh
# クローン
$ git clone https://github.com/kdlucas/byte-unixbench
$ cd byte-unixbench/UnixBench/
$ ./Run
```

unixbench 後の、CPU温度=46.0C だった。
```
========================================================================
   BYTE UNIX Benchmarks (Version 5.1.3)

   System: rasp-03: GNU/Linux
   OS: GNU/Linux -- 4.19.75-v7l+ -- #1270 SMP Tue Sep 24 18:51:41 BST 2019
   Machine: armv7l (unknown)
   Language: en_US.utf8 (charmap="ANSI_X3.4-1968", collate="ANSI_X3.4-1968")
   CPU 0: ARMv7 Processor rev 3 (v7l) (0.0 bogomips)

   CPU 1: ARMv7 Processor rev 3 (v7l) (0.0 bogomips)

   CPU 2: ARMv7 Processor rev 3 (v7l) (0.0 bogomips)

   CPU 3: ARMv7 Processor rev 3 (v7l) (0.0 bogomips)

   23:38:32 up  1:22,  1 user,  load average: 0.44, 0.94, 1.08; runlevel Oct

------------------------------------------------------------------------
Benchmark Run: 日 10月 13 2019 23:38:32 - 00:06:32
4 CPUs in system; running 1 parallel copy of tests

Dhrystone 2 using register variables       10123054.6 lps   (10.0 s, 7 samples)
Double-Precision Whetstone                     2365.1 MWIPS (9.4 s, 7 samples)
Execl Throughput                                825.1 lps   (29.7 s, 2 samples)
File Copy 1024 bufsize 2000 maxblocks        108608.8 KBps  (30.0 s, 2 samples)
File Copy 256 bufsize 500 maxblocks           30904.5 KBps  (30.0 s, 2 samples)
File Copy 4096 bufsize 8000 maxblocks        301953.2 KBps  (30.0 s, 2 samples)
Pipe Throughput                              157166.8 lps   (10.0 s, 7 samples)
Pipe-based Context Switching                  43586.2 lps   (10.0 s, 7 samples)
Process Creation                               1596.9 lps   (30.0 s, 2 samples)
Shell Scripts (1 concurrent)                   2590.2 lpm   (60.0 s, 2 samples)
Shell Scripts (8 concurrent)                    685.7 lpm   (60.1 s, 2 samples)
System Call Overhead                         480465.9 lps   (10.0 s, 7 samples)

System Benchmarks Index Values               BASELINE       RESULT    INDEX
Dhrystone 2 using register variables         116700.0   10123054.6    867.4
Double-Precision Whetstone                       55.0       2365.1    430.0
Execl Throughput                                 43.0        825.1    191.9
File Copy 1024 bufsize 2000 maxblocks          3960.0     108608.8    274.3
File Copy 256 bufsize 500 maxblocks            1655.0      30904.5    186.7
File Copy 4096 bufsize 8000 maxblocks          5800.0     301953.2    520.6
Pipe Throughput                               12440.0     157166.8    126.3
Pipe-based Context Switching                   4000.0      43586.2    109.0
Process Creation                                126.0       1596.9    126.7
Shell Scripts (1 concurrent)                     42.4       2590.2    610.9
Shell Scripts (8 concurrent)                      6.0        685.7   1142.9
System Call Overhead                          15000.0     480465.9    320.3
                                                                   ========
System Benchmarks Index Score                                         308.6

------------------------------------------------------------------------
Benchmark Run: 月 10月 14 2019 00:06:32 - 00:34:39
4 CPUs in system; running 4 parallel copies of tests

Dhrystone 2 using register variables       36763438.3 lps   (10.0 s, 7 samples)
Double-Precision Whetstone                     8499.7 MWIPS (9.7 s, 7 samples)
Execl Throughput                               2332.6 lps   (29.6 s, 2 samples)
File Copy 1024 bufsize 2000 maxblocks        197533.1 KBps  (30.0 s, 2 samples)
File Copy 256 bufsize 500 maxblocks           55015.8 KBps  (30.0 s, 2 samples)
File Copy 4096 bufsize 8000 maxblocks        574217.5 KBps  (30.0 s, 2 samples)
Pipe Throughput                              554865.0 lps   (10.0 s, 7 samples)
Pipe-based Context Switching                 155417.9 lps   (10.0 s, 7 samples)
Process Creation                               4251.2 lps   (30.0 s, 2 samples)
Shell Scripts (1 concurrent)                   5438.2 lpm   (60.0 s, 2 samples)
Shell Scripts (8 concurrent)                    726.2 lpm   (60.1 s, 2 samples)
System Call Overhead                        1697096.3 lps   (10.0 s, 7 samples)

System Benchmarks Index Values               BASELINE       RESULT    INDEX
Dhrystone 2 using register variables         116700.0   36763438.3   3150.3
Double-Precision Whetstone                       55.0       8499.7   1545.4
Execl Throughput                                 43.0       2332.6    542.5
File Copy 1024 bufsize 2000 maxblocks          3960.0     197533.1    498.8
File Copy 256 bufsize 500 maxblocks            1655.0      55015.8    332.4
File Copy 4096 bufsize 8000 maxblocks          5800.0     574217.5    990.0
Pipe Throughput                               12440.0     554865.0    446.0
Pipe-based Context Switching                   4000.0     155417.9    388.5
Process Creation                                126.0       4251.2    337.4
Shell Scripts (1 concurrent)                     42.4       5438.2   1282.6
Shell Scripts (8 concurrent)                      6.0        726.2   1210.4
System Call Overhead                          15000.0    1697096.3   1131.4
                                                                   ========
System Benchmarks Index Score                                         771.6
```

## 動画変換(m2ts => mp4)
3 の時に使用した時と同様の 10秒の m2tsファイルを利用

m2ts から mp4(映像: H.264、音声:mp3)に変換。※オプション未指定の場合と同様  
fps 8.4。動画変換に約40秒かかる。 3 に比べ３倍近い速度に！
```
$ ffmpeg -i test.m2ts output.mp4 -vcodec libx264 -acodec libmp3lame
...
frame=  296 fps=8.4 q=-1.0 Lsize=    5358kB time=00:00:09.77 bitrate=4489.5kbits/s dup=24 drop=0 speed=0.276x
video:5195kB audio:152kB subtitle:0kB other streams:0kB global headers:0kB muxing overhead: 0.210654%
...
```

output.mp4 の情報
```
$ ffprobe output.mp4
...
Input #0, mov,mp4,m4a,3gp,3g2,mj2, from 'output.mp4':
  Metadata:
    major_brand     : isom
    minor_version   : 512
    compatible_brands: isomiso2avc1mp41
    encoder         : Lavf58.20.100
  Duration: 00:00:09.88, start: 0.000000, bitrate: 4443 kb/s
    Stream #0:0(und): Video: h264 (High) (avc1 / 0x31637661), yuv420p, 1440x1080 [SAR 4:3 DAR 16:9], 4308 kb/s, 29.97 fps, 29.97 tbr, 30k tbn, 59.94 tbc (default)
    Metadata:
      handler_name    : VideoHandler
    Stream #0:1(und): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 130 kb/s (default)
    Metadata:
      handler_name    : SoundHandler
...
```

m2ts から　mp4 に変換。（オプション無し）
```
$ ffmpeg -i test.m2ts output2.mp4
...
frame=  296 fps=8.3 q=-1.0 Lsize=    5358kB time=00:00:09.77 bitrate=4489.5kbits/s dup=24 drop=0 speed=0.273x
video:5195kB audio:152kB subtitle:0kB other streams:0kB global headers:0kB muxing overhead: 0.210654%
...
```

output2.mp4 の情報
```
$ ffprobe output2.mp4
...
Input #0, mov,mp4,m4a,3gp,3g2,mj2, from 'output2.mp4':
  Metadata:
    major_brand     : isom
    minor_version   : 512
    compatible_brands: isomiso2avc1mp41
    encoder         : Lavf58.20.100
  Duration: 00:00:09.88, start: 0.000000, bitrate: 4443 kb/s
    Stream #0:0(und): Video: h264 (High) (avc1 / 0x31637661), yuv420p, 1440x1080 [SAR 4:3 DAR 16:9], 4308 kb/s, 29.97 fps, 29.97 tbr, 30k tbn, 59.94 tbc (default)
    Metadata:
      handler_name    : VideoHandler
    Stream #0:1(und): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 130 kb/s (default)
    Metadata:
      handler_name    : SoundHandler
```
