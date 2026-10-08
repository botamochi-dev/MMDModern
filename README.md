# MMDModern

MMDModernは、MikuMikuDance 9.32（64bit版）の再生やファイル読み込みの負担を減らすツールです。描画の最適化により最大でFPSを2倍に高速化し、シーン読み込み時間を約40%削減します。カメラのキーフレームの「元に戻す」、モデルの表示名変更・複製、外部親の移行、カメラを外部親にする機能、選択キーの一括補正、WAVの開始位置調整といった編集機能も追加します。MMD本体を改造する必要はなく、2つのファイルを置くだけで利用できます。

## 免責事項

本ツールは利用者自身の責任で使用してください。本ツールの使用により生じたいかなる損害・損失・不具合についても、作者および配布者は一切の責任を負いません。これには、データの破損・消失、作業の中断、その他の直接的・間接的な損害を含みます。

## 対応環境

- WindowsのMikuMikuDance 9.32（64bit版）。
- MME・MMPlusが導入された環境で動作を確認しています。エフェクト関連の機能にはMMEが必要です。

## インストール

1. MMDを終了します。
2. `MikuMikuDance.exe`と同じフォルダーに、配布ファイルの`dsound.dll`と`MMDModern.ini`をコピーします。
3. MMDをいつもどおり起動します。通常は設定を変更する必要はありません。

更新する場合もMMDを終了し、`dsound.dll`を最新版へ置き換えてください。

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
| 最小化からの復帰を速くする | 画像の全ミップをメモリーに保持し、復帰時の再読み込み・展開を減らします。画像の変更時には読み直します。 | ON |
| AVI出力を速くする | 画像取得と次フレームの準備を並行して進め、出力中のプレビュー表示を省きます。 | ON |
| PMM保存を速くする | 小さな書き込みをまとめ、書き込み完了を確認してから保存を成功とします。EMM・モーション保存は対象外です。 | ON |
| 一部のPMX読み込み時のクラッシュを防ぐ | 表示枠やボーン指定が原因となる、特定の読み込み不具合に対処します。 | ON |
| PMM読み込み時のエフェクト割り当てを補助する | 読み込み途中でエフェクトが割り当てられ、後から読み込まれたモデルに反映されない問題に対処します。 | ON |
| DXVK使用時の表示を補助する | DXVKを使用する場合に、3D画面の表示方法を自動調整します。 | 自動 |
| ポストエフェクトの処理をさらに減らす | 画面全体にかけるエフェクトの不要な処理を減らす、試験的な機能です。 | OFF |
| モデルの変形計算を効率化する | モデルの変形計算の待ち時間を減らす、試験的な機能です。環境によってCPU負荷が増える場合があります。 | OFF |
| フレーム間隔を整える | FPS上限に達しているときの待ち時間を調整する、試験的な機能です。 | OFF |
| 動作の計測・診断 | 描画・読み込み・AVI出力の時間や、エラーの情報を調査できます。 | OFF |
| カメラのキーフレームを元に戻す | カメラモードで、カメラのキーフレームの追加・変更・削除を元に戻す／やり直しできるようにします。 | ON |
| モデルの表示名を変更する | 選択中のモデルの表示名を変更し、PMMに保存します。 | ON |
| モデルを複製する | 選択中のモデルを同じファイルから読み込み直し、キーフレームをコピーします。 | ON |
| モデルの外部親を移行する | 選択中のモデルの外部親を、別モデルの同名ボーンへまとめて移します。 | ON |
| カメラを外部親にする | モデル全体またはボーンを、カメラの位置・回転・視野角に追従させます。 | ON |
| 画面操作で選択キーを補正する | 画面上で調整したボーンやカメラの変化量を、選択したキーへまとめて反映します。 | ON |
| WAVの開始位置を調整する | 音声をフレーム数で遅らせる／先頭を詰め、通常再生とAVI出力に反映します。 | ON |

## 編集機能

### カメラのキーフレームを元に戻す

MMD本来はカメラモードで「元に戻す」が使えませんが、MMDModernを導入すると、カメラのキーフレームの追加・変更・削除を戻せるようになります。

- 「元に戻す」「やり直し」ボタン、またはCtrl+Z（元に戻す）／Ctrl+X（やり直し）で操作します。
- 戻せる回数は初期設定で30回です。`[Edit] CameraUndoSteps`で1〜1000回に変更できます。
- 照明・セルフ影・アクセサリーのキーフレームは対象外です。

### モデルの表示名の変更・複製

メニューバーに追加される「MMDModern」メニューから、選択中のモデルに対して次の操作ができます。

- **名前の変更**：モデルの表示名を変更します。変更した名前はPMMに保存され、PMMを開いたときに表示されます。PMXファイル自体は変更しません。
- **複製**：選択中のモデルを同じファイルからもう一度読み込み、ボーン・表情・表示／IK／外部親のキーフレームをコピーします。複製したモデルの名前の末尾には(2)、(3)…が付きます。描画順やMMEのエフェクト割り当てなど、モデルの設定は複製されません。

それぞれ`[Edit] CameraUndo`、`[Model] Rename`、`[Model] Duplicate`を`0`にすると無効になり、元のMMDの動作に戻ります。

### モデルの外部親を別モデルへ移行する

外部親を設定した子モデルを選び、「MMDModern」→「別モデルへ外部親を移行」から移行先モデルを指定します。現在の設定と既存の表示／IK／外部親キーにある親モデルを、移行先の同名ボーンへまとめて変更します。「親なし」の設定は保持します。

対応するボーンがない場合や、同名ボーンが重複する場合、親子関係が循環する場合は変更できません。カメラを外部親にしたモデルも移行の対象外です。直前の移行は「MMDModern」→「外部親移行を元に戻す」で取り消せます。

`[Model] ExternalParentTransfer=0`で無効にできます。

### カメラを外部親にする

MMDの外部親設定で、親モデルの候補から「カメラ」を選び、登録します。モデル全体または対象ボーンを、カメラの位置・回転に追従させられます。視野角を変えても、画面上の配置・大きさを保つように追従します。カメラの前に固定したモデルなどに利用できます。

設定はPMMに保存されます。VMDには外部親の情報が含まれないため、シーンはPMMで保存してください。解除する場合は外部親設定で「なし」を選び、登録します。カメラとモデルが互いに追従する設定は登録できません。

`[Model] CameraExternalParent=0`で無効にできます。無効時やMMDModernを導入していない環境では、保存済みのカメラ外部親は「親なし」として動作します。

### 画面操作で選択キーを一括補正する

初期設定で有効です。`[Edit] ViewportKeyframeAdjust=0`で無効にできます。

1. タイムラインで補正するボーンまたはカメラのキーを選択します。
2. 「MMDModern」→「画面操作で選択キーを補正」を開きます。
3. 画面上でボーンやカメラの位置・回転を調整します。カメラの距離・視野角も調整できます。
4. フレームを移動して動きを確認し、必要に応じて追加調整します。
5. 「確定」で選択キーへ反映します。「すべてリセット」で開始時の状態へ戻して調整を続け、「取消」で変更を取り消して終了できます。

補正されるのは開始時に選択したキーです。現在フレームに新しいキーを作らず、選択していないキーは変更しません。確定した補正は「前回の一括補正を元に戻す」「一括補正をやり直す」で戻せます。

### WAVの開始位置を調整する

初期設定で有効です。`[Edit] WavOffset=0`で無効にできます。WAVを読み込み、再生を停止してから「MMDModern」→「WAVの開始位置を調整」を開き、調整するフレーム数を入力します。

- **＋30フレーム**：先頭に1秒の無音を追加し、音声を遅らせます。
- **−30フレーム**：先頭1秒を除き、音声を早めます。

30フレームが1秒に相当し、プレビューやAVIのFPS設定とは独立しています。調整後のWAVは別名で保存して読み直すため、元のファイルは残ります。8／16ビットPCMのモノラル・ステレオWAVに対応します。

通常再生とAVI出力は同じ調整済みWAVを使用します。AVIに音声を含める場合は、MMDの音声出力設定を有効にし、0フレームから出力してください。PMMを保存すると調整済みWAVへの参照も保存されるため、シーンと一緒にそのWAVを保管してください。

繰り返し調整すると、現在読み込んでいるWAVに調整が加算されます。元に戻したい場合や調整をやり直す場合は、元のWAVを読み込んでください。

以前の`MMDModern.ini`を引き続き使う場合、利用したい機能の設定を該当する`[Model]`または`[Edit]`欄へ追加し、MMDを起動し直してください。

## 設定と問題が起きたとき

MMDを終了してから`MMDModern.ini`を編集してください。多くの設定は`1`で有効、`0`で無効になります。詳しくはini内の日本語コメントを参照してください。計測・デバッグと、効果を確認できていない試験的な機能は配布設定では無効です。

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
