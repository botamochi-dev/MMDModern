# MMDModern

MMDModernは、MikuMikuDance 9.32（64bit版）の再生やファイル読み込みの負担を減らすツールです。描画の最適化により最大でFPSを2倍に高速化し、シーン読み込み時間を約40%削減します。MMD本体を改造する必要はなく、2つのファイルを置くだけで利用できます。

## 免責事項

本ツールは利用者自身の責任で使用してください。本ツールの使用により生じたいかなる損害・損失・不具合についても、作者および配布者は一切の責任を負いません。これには、データの破損・消失、作業の中断、その他の直接的・間接的な損害を含みます。

## 対応環境

- WindowsのMikuMikuDance 9.32（64bit版）。
- MME・MMPlusが導入された環境で動作を確認しています。エフェクト関連の機能にはMMEが必要です。

## インストール

1. MMDを終了します。
2. `MikuMikuDance.exe`と同じフォルダーに、配布ファイルの`dsound.dll`と`MMDModern.ini`をコピーします。
3. MMDをいつもどおり起動します。通常は設定を変更する必要はありません。

配置例：

```text
MMDのフォルダー/
├─ MikuMikuDance.exe
├─ dsound.dll
└─ MMDModern.ini
```

## アンインストール

1. MMDを終了します。
2. インストールした`dsound.dll`と`MMDModern.ini`を削除します。

次回起動からMMDModernは動作しなくなります。

MMDのフォルダーに作成される`MMDModern.log`、`MMDModernCache`フォルダー、`MMDModern_census_*.csv`、`MMDModern_crash_*.dmp`も、不要であれば削除できます。

## 機能一覧

| 機能 | 概要 | 初期設定 |
|---|---|---|
| 複数モデルの描画を軽くする | モデルの描画順やテクスチャの確認を効率よく行い、再生中の負担を減らします。 | ON |
| 不要な描画処理を省く | MMEが表示しないモデルやアクセサリーについて、不要な処理を減らします。 | ON |
| エフェクト処理の負担を減らす | エフェクトの確認や、使われないMMD標準エフェクトの処理を減らします。 | ON |
| エフェクトの再読み込みを速くする | 一度読み込んだエフェクトの準備結果を保存し、次回以降の読み込みに利用します。 | ON |
| モデル・モーションなどの読み込みを軽くする | ファイルの読み方を効率化し、読み込み時の負担を減らします。 | ON |
| 一部のPMX読み込み時のクラッシュを防ぐ | 表示枠やボーン指定が原因となる、特定の読み込み不具合に対処します。 | ON |
| PMM読み込み時のエフェクト割り当てを補助する | 読み込み途中でエフェクトが割り当てられ、後から読み込まれたモデルに反映されない問題に対処します。 | ON |
| DXVK使用時の表示を補助する | DXVKを使用する場合に、3D画面の表示方法を自動調整します。 | 自動 |
| ポストエフェクトの処理をさらに減らす | 画面全体にかけるエフェクトの不要な処理を減らす、試験的な機能です。 | OFF |
| モデルの変形計算を効率化する | モデルの変形計算の待ち時間を減らす、試験的な機能です。環境によってCPU負荷が増える場合があります。 | OFF |
| フレーム間隔を整える | FPS上限に達しているときの待ち時間を調整する、試験的な機能です。 | OFF |
| 動作の計測・診断 | 描画・読み込み・AVI出力の時間や、エラーの情報を調査できます。 | OFF |

## 設定と問題が起きたとき

MMDを終了してから`MMDModern.ini`を編集してください。多くの設定は`1`で有効、`0`で無効になります。詳しくはini内の日本語コメントを参照してください。試験的な機能は初期設定では無効です。

- 表示がおかしい、または動作が不安定な場合は、変更した設定を戻してください。`dsound.dll`を取り外して、MMDModernなしで再現するか確認することもできます。
- エフェクトを編集する場合、変更の反映に最大約1秒の遅れが生じます。すぐに反映させたい場合は`[MME] FileCheckIntervalMs=0`にします。
- エフェクトのキャッシュは初回読み込み時に作成されます。キャッシュを作り直す場合は、MMDを終了して`MMDModernCache`を削除してください。

多様なシーンでの長期安定性や、すべての描画結果の完全一致は検証中です。大切なプロジェクトはバックアップして利用してください。


## ライセンス

MMDModern独自の部分はMITライセンスで提供します。全文は同梱の[LICENSE](LICENSE)を参照してください。著作権表示とライセンス本文を保持することを条件に、商用利用・改変・再配布が可能です。

再配布する際は、`LICENSE`と、以下の第三者ライセンス表記を含む`README.md`を同梱してください。第三者のコードには、それぞれのライセンスが適用されます。

## 第三者ライセンス

MMDModernはMinHookを使用しています。バイナリ配布に必要な著作権・ライセンス表記を以下に掲載します。この表記はMinHookと同梱のHacker Disassembler Engineに関するものです。

```text
MinHook - The Minimalistic API Hooking Library for x64/x86
Copyright (C) 2009-2017 Tsuda Kageyu.
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions
are met:

 1. Redistributions of source code must retain the above copyright
    notice, this list of conditions and the following disclaimer.
 2. Redistributions in binary form must reproduce the above copyright
    notice, this list of conditions and the following disclaimer in the
    documentation and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
"AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED
TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A
PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER
OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

================================================================================
Portions of this software are Copyright (c) 2008-2009, Vyacheslav Patkov.
================================================================================
Hacker Disassembler Engine 32 C
Copyright (c) 2008-2009, Vyacheslav Patkov.
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions
are met:

 1. Redistributions of source code must retain the above copyright
    notice, this list of conditions and the following disclaimer.
 2. Redistributions in binary form must reproduce the above copyright
    notice, this list of conditions and the following disclaimer in the
    documentation and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
"AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED
TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A
PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE REGENTS OR
CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

-------------------------------------------------------------------------------
Hacker Disassembler Engine 64 C
Copyright (c) 2008-2009, Vyacheslav Patkov.
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions
are met:

 1. Redistributions of source code must retain the above copyright
    notice, this list of conditions and the following disclaimer.
 2. Redistributions in binary form must reproduce the above copyright
    notice, this list of conditions and the following disclaimer in the
    documentation and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
"AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED
TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A
PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE REGENTS OR
CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```
