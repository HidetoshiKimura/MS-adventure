# ピーク山脈 探検記

[English](#english) | 日本語

**▶ [ここで遊べます](https://hidetoshikimura.github.io/MS-adventure/)**：<https://hidetoshikimura.github.io/MS-adventure/>（インストール不要。PC・携帯のブラウザで開けます）

MS-DIAL 5 のアライメント結果（AlignmentResult）を読み込んで、LC-MS データを歩いて回れる 3D の山脈にするブラウザアプリです。東西が RT、南北が m/z、山の高さがピーク強度（log）です。山頂の結晶に近づくと同定結果がわかり、図鑑に記録されます。

> **遊び用です。学術論文・学会発表・定量などには使わないでください。**
> 山の形は見やすさのために作り直したもので、実際のピークの形ではありません。くわしくは下の「注意：山の形について」を読んでください。解析には MS-DIAL を使ってください。

## 使い方

MS-DIAL のデータが手元になくても、公開ページの「デモデータ（ワイン）で遊ぶ」ボタンで、すぐに試せます（`demo/wine-pos/`、MS-DIAL チュートリアルのデモデータを解析したもの。出典は `demo/wine-pos/README.md`）。

自分のデータで遊ぶときは：

1. `index.html` をブラウザ（Chrome / Edge 推奨）で開く。GitHub Pages で公開している場合は、そのページを開く
2. 「フォルダごと選ぶ」で MS-DIAL のプロジェクトフォルダを選ぶ（または下のファイルを選ぶ／ドラッグ＆ドロップ）
3. 「POS 大陸へ」などのボタンを押す

| ファイル | 必須 | 使いみち |
|---|---|---|
| `AlignmentResult_*.arf2` | 必須 | 山（RT・m/z・強度）、同定名、照合スコア |
| `AlignmentResult_*_PeakProperties.arf` | 任意 | サンプル名 |
| `AlignmentResult_*.EIC.aef` | 任意 | EIC |
| `AlignmentResult_*.dcl` | 任意 | MS/MS、フラグメント検索 |
| `AlignmentResult_*_tags.xml` | 任意 | MS-DIAL で付けたタグでの絞り込み |

画面は日本語と英語に対応しています。ブラウザの言語で自動的に選ばれ、スタート画面右上の「日本語 / English」で切り替えられます（URL に `?lang=ja` / `?lang=en` を付けても指定できます）。

数 GB の `.EIC.aef` でも、必要なピークの部分だけを読むので動きます。MS-DIAL 5.5 のファイルで確認しています。

## 操作

| PC | 携帯 | 動作 |
|---|---|---|
| 画面をクリック → マウス | 指でドラッグ | 向き・視点（Esc で解除） |
| W / S、A / D | ▲▼、◀▶ | 前後、左右（携帯の◀▶は向き） |
| Space | — | ジャンプ |
| Space を2回 | 「上昇」 | 空を飛ぶ（Space 上昇・Shift 下降、地面に着くと解除） |
| Shift | — | 走る |
| V | — | 一人称・三人称 |
| ホイール | 2本指 | ズーム |
| F | 「マント」 | アラインメントID・RT と m/z・地図クリックで指定した場所へ飛ぶ |
| N | 「絞り込み」 | Peak spot navigator（Ref. matched・MS2 acquired・タグ・フラグメント検索など） |
| J | 「図鑑」 | 見つけたピークの一覧 |
| E | 「グラフ」 | EIC・MS/MS 欄の表示切替 |
| M・地図のボタン | 地図のボタン | 地図の拡大（ホイール・ピンチ）、移動（ドラッグ）、スポットを選んで「ここへ飛ぶ」「グラフ」、ダブルクリックで飛ぶ、⤢ で大きく表示 |

## データの扱い

- 選んだファイルは、ブラウザの中だけで読み込みます。どこにも送信せず、ファイルを書き換えることもありません。
- 図鑑の記録（見つけたピークの ID）は、そのブラウザの localStorage にだけ保存されます。
- このリポジトリには測定データを含めていません。データを含むファイルを入れないよう、`.gitignore` で除外しています。

## 注意：山の形について（遊び用です）

このアプリは、データを眺めて遊ぶためのものです。見やすさのために、MS-DIAL の値から山の形を作り直しています。次の点で実際のデータとは違うので、**学術論文・学会発表の図、定量、同定の判断には使わないでください。**

- **ピークの幅：** 実際のピーク幅は使っていません。すべてのピークを、同じ幅の山（RT 方向・m/z 方向とも固定の幅）として描いています。地図の大きさがデータの範囲に合わせて伸び縮みするので、山の幅が表す RT や m/z の幅もデータごとに変わります。
- **山の高さ：** MS-DIAL の最大ピーク高さ（HeightMax）の log をとって高さにしています。強度が小さいピーク（およそ 200 未満）は平地になります。
- **重なり：** 近くにあるピークの山は足し合わせず、高いほうの山だけが見えます。低いピークは隠れることがあります。
- **「標高」の表示：** 画面左上の値は、地形の高さから逆算した目安です。山頂以外では、そのピークの強度とは一致しません。正確な値は、山に登ったときに出る「最大強度」を見てください。
- **山の色：** MS-DIAL の Ontology（化合物クラス）で塗り分けています。ピーク数の多いクラスから順に上位 10 クラス（画面右上で 5〜20・全部に変更可）に色を付け、残りは「その他」の色です。Ontology がないピークは、名前から脂質クラスが分かるときだけその名前で分類します。
- **絞り込み：** MS-DIAL の Peak spot navigator に合わせていますが、同じ結果になるとは限りません。「Peak spots %」は相対強度の順位で、「Unique ions」はこのアプリ独自のフラグメント検索です。
- **EIC・MS/MS：** MS-DIAL のファイルの値をそのまま描いています。ただし MS/MS は、強度の上位 30 本だけを表示しています。

## 貢献

- 地図の拡大とスポット選択：[@TaiseiNaobayashi](https://github.com/TaiseiNaobayashi)（PR #1）

## ライセンス

MIT License（`LICENSE` を参照）。`index.html` には three.js r128（MIT License, Copyright 2010-2021 three.js authors）を同梱しています。

---

## English

**Peak Ridge Expedition** (ピーク山脈 探検記)

**▶ [Play here](https://hidetoshikimura.github.io/MS-adventure/?lang=en)**: <https://hidetoshikimura.github.io/MS-adventure/?lang=en> (no installation; works in desktop and mobile browsers)

A browser app that loads MS-DIAL 5 alignment results (AlignmentResult) and turns your LC-MS data into a 3D mountain range you can walk around. East–west is RT, north–south is m/z, and mountain height is peak intensity (log). Walk up to the crystal on a summit to see its annotation and record it in your field guide.

> **This is just for fun. Do not use it for papers, presentations or quantification.**
> The mountains are redrawn for readability and are not the real peak shapes. See "Note: mountain shapes" below. Use MS-DIAL for analysis.

The interface is available in Japanese and English. The language is chosen from your browser settings and can be switched with the "日本語 / English" buttons at the top right of the start screen (or with `?lang=en` / `?lang=ja` in the URL).

### How to use

No MS-DIAL data at hand? Press **"Try the demo data (wine)"** on the public page (`demo/wine-pos/`: the MS-DIAL tutorial demo data, reanalyzed; see `demo/wine-pos/README.md` for the source).

To use your own data:

1. Open `index.html` in a browser (Chrome / Edge recommended), or open the GitHub Pages site
2. Press "Choose a folder" and select your MS-DIAL project folder (or choose the files below / drag & drop them)
3. Press a button such as "Go to POS Continent"

| File | Required | Used for |
|---|---|---|
| `AlignmentResult_*.arf2` | Yes | Mountains (RT, m/z, intensity), annotations, match scores |
| `AlignmentResult_*_PeakProperties.arf` | No | Sample names |
| `AlignmentResult_*.EIC.aef` | No | EIC |
| `AlignmentResult_*.dcl` | No | MS/MS, fragment search |
| `AlignmentResult_*_tags.xml` | No | Filtering by tags set in MS-DIAL |

Even multi-GB `.EIC.aef` files work, because only the parts needed for nearby peaks are read. Tested with MS-DIAL 5.5 files.

### Controls

| PC | Mobile | Action |
|---|---|---|
| Click the screen → mouse | Drag with a finger | Look around (Esc to release) |
| W / S, A / D | ▲▼, ◀▶ | Forward/back, left/right (◀▶ turns on mobile) |
| Space | — | Jump |
| Space twice | "Up" | Fly (Space up, Shift down; lands when you touch the ground) |
| Shift | — | Run |
| V | — | First / third person |
| Wheel | Two fingers | Zoom |
| F | "Cape" | Fly to an alignment ID, an RT and m/z, or a spot picked on the map |
| N | "Filter" | Peak spot navigator (Ref. matched, MS2 acquired, tags, fragment search, etc.) |
| J | "Field guide" | List of peaks you have found |
| E | "Spectra" / "Plots" | Show/hide the EIC and MS/MS panel |
| M / map buttons | Map buttons | Map: zoom (wheel/pinch), pan (drag), pick a spot then "Fly here" or "Plots", double-click to fly, ⤢ to enlarge |

### Your data

- Selected files are read only inside your browser. Nothing is uploaded, and files are never modified.
- Field-guide records (IDs of peaks you found) and your language choice are stored only in that browser's localStorage.
- This repository contains no measurement data except the attributed demo data; data files are excluded by `.gitignore`.

### Note: mountain shapes (just for fun)

The mountains are rebuilt from MS-DIAL values to be easy to look at. They differ from the real data as follows, so **do not use them for figures in papers or presentations, quantification, or annotation decisions.**

- **Peak width:** Real peak widths are not used. Every peak is drawn as a mountain of the same width (fixed in both RT and m/z). Because the map is stretched to fit the data range, the RT/m/z width a mountain represents also changes between datasets.
- **Height:** The log of MS-DIAL's maximum peak height (HeightMax). Weak peaks (below about 200) become flat ground.
- **Overlap:** Nearby mountains are not added together; only the taller one is shown, so smaller peaks can be hidden.
- **"Altitude":** The value at the top left is a rough estimate back-calculated from the terrain height. Except on a summit, it does not match the peak's intensity. For the exact value, see "max intensity" shown when you climb a mountain.
- **Colors:** Mountains are colored by MS-DIAL Ontology (compound class). The top 10 classes by peak count (5–20 or all, changeable at the top right) get colors; the rest share the "Others" color. Peaks without an Ontology are classified by name only when the lipid class can be inferred from it.
- **Filter:** Modeled on MS-DIAL's Peak spot navigator, but the results may differ. "Peak spots %" uses the rank of relative abundance, and "Unique ions" is this app's own fragment search.
- **EIC and MS/MS:** Drawn directly from the values in the MS-DIAL files, except that only the 30 most intense MS/MS peaks are shown.

### Contributors

- Map zoom and spot selection: [@TaiseiNaobayashi](https://github.com/TaiseiNaobayashi) (PR #1)

### License

MIT License (see `LICENSE`). `index.html` bundles three.js r128 (MIT License, Copyright 2010-2021 three.js authors).
