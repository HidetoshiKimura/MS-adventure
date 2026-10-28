# デモデータ：ワイン（Positive）

ピーク山脈 探検記の「デモデータで遊ぶ」ボタンで読み込まれるテストデータです。GitHub にブラウザから上げられる大きさにするため、各ファイルを gzip で圧縮し、8 MB ごとに分割しています（`*.gz.part00`、`*.gz.part01` …）。ボタンを押すとページが自動でつなぎ直して展開します。

手元で使うときは、分割されたファイルをつなげて展開してください（例：`cat 〜.EIC.aef.gz.part* | gunzip > 〜.EIC.aef`。Windows の PowerShell なら `cmd /c copy /b 〜.EIC.aef.gz.part00+〜.EIC.aef.gz.part01+〜.EIC.aef.gz.part02 〜.EIC.aef.gz` のあと 7-Zip などで展開）。

## 中身

MS-DIAL 5.5（Metabolomics、ESI Positive）で解析した AlignmentResult 一式です。

| ファイル | 内容 |
|---|---|
| `*.arf2.gz.part*` | ピーク一覧（8,966 ピーク）、同定名、照合スコア |
| `*_PeakProperties.arf.gz.part*` | サンプル（6 本）ごとのピーク情報 |
| `*.dcl.gz.part*` | MS/MS |
| `*.EIC.aef.gz.part*` | EIC |
| `*_tags.xml` | タグ（このデータでは未使用） |

解析条件：MS1 tolerance 0.01 Da、MS2 tolerance 0.025 Da。同定には MS-DIAL のデモに同梱の `MSMS-Public-Pos-VS14.msp` を使い、ライブラリの保持時間は使っていません（RT tolerance 100 min）。

測定データ（`.abf`）とライブラリ（`.msp`）は含めていません。

## 出典とライセンス

元データは、MS-DIAL のチュートリアルで配布されているワインのデモデータ（`20160805-Wine-DDA-Pos-Demo files`、LC-MS/MS、データ依存取得）です。

- MS-DIAL / CompMS: https://systemsomicslab.github.io/compms/msdial/main.html
- MS-DIAL 5 tutorial（Metabolomics）: https://systemsomicslab.github.io/msdial5tutorial/metabolomics.html
- ライセンス: CompMS のファイル（MSP 形式のライブラリを含む）は CC BY 4.0 で公開されています（https://systemsomicslab.github.io/compms/license/main.html）。

このフォルダのファイルは、上のデモデータを MS-DIAL 5.5 で解析し直した結果で、元の測定データ・ライブラリから作った二次的なデータです。同じく CC BY 4.0 に従い、出典を明記して配布しています。

このデータも、アプリと同じく遊び用です。解析結果として引用しないでください。
