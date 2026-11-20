[简体中文](README.md) ｜ [繁體中文](README.zh-Hant.md) ｜ [English](README.en.md) ｜ **日本語**

# 西安方言入力法 · Android 直装版 · android-xinganhua

> 西安方言入力法を Android の直装（すぐ使える）パッケージにしました。**Fcitx5 for Android**（小企鹅输入法）の**本体**と **Rime プラグイン**を入れ、「中州韵」から「西安話城區音」または「西安話南郊音」を選べば、西安方言ピンインでそのまま打てます。方案ファイルを自分で端末に読み込む必要はありません。

- **対応**：Android 6.0 以降（minSdk 23）。ABI は `arm64-v8a` / `armeabi-v7a` / `x86` / `x86_64` の 4 種
- **公開物**：APK 8 個 = 本体 × 4 ABI ＋ Rime プラグイン × 4 ABI。すべて同じ鍵で署名
- **内蔵方案**：`chengqyu`（西安方言城区音）、`nanjiao`（西安方言南郊音）。プラグインが `rime-data` に入れ、方案メニューの先頭に置く
- **パッケージ名**：`org.fcitx.fcitx5.android`（公式版と同じ、署名は別。先に公式版を削除）
- **方案の原本**：[xinganhua-fuvufa](https://github.com/SiqYin/xinganhua-fuvufa)（参照のみ。本リポジトリでは方案を変更しない）
- **四言語**：簡体中文 / 繁體中文 / English / 日本語。上のリンクで切り替え。内容は四版とも同じで、簡体版を正とします

---

## 目次

1. [西安方言ピンインの方案](#s1)
2. [これは何か](#s2)
3. [ダウンロードとインストール](#s3)
4. [方案の組み込み方](#s4)
5. [方案リポジトリとの関係](#s5)
6. [自分でビルドする](#s6)
7. [上流と謝辞](#s7)
8. [ライセンス](#s8)

---

<a id="s1"></a>

## 1. 西安方言ピンインの方案

スマートフォンのこのパッケージも、パソコンの Rime も、二つの Web リポジトリも、すべて同じ**西安方言ピンイン**（城区音・南郊音それぞれ一套）を使います。1 音節は「声母＋韻母＋声調番号」で、たとえば `ba1` 巴、`bfeng4` 中、`jyuen1` 軍：

- **声母**：両系統に共通する 24 個（零声母を含む）＋城区音だけの `bf`・`pf`（計 26 個）、南郊音だけの `rh`（計 25 個）：`b p m f v bf pf d t n l z c s rh j q x zh ch sh r g k h ng`
- **韻母**：共通する 38 個（開 15 ／ 斉 8 ／ 合 9 ／ 撮 6）＋城区音だけの `uu`・`iai`（計 40 個：開 16 ／ 斉 9 ／ 合 9 ／ 撮 6）
- **四声**：陰平 21、陽平 24、上声 53、去声 44。入声はすでにこの四声に統合
- **声調番号は音節の直後**に、空白を入れずに置く：`bfeng4` 中、`jyuen1` 軍
- **音節の境界は撇号（アポストロフィ）**：`xi'ngan1` 西安（そのまま書くと xin 心 ＋ gan 干 に切られる）
- **簡拼**：入力側では `in / ing / iu / ui / un / ung / yun / yung` が使えます（それぞれ `ien / ieng / iou / uei / uen / uong / yuen / yuong` に対応。零声母は `yuen`・`yuong` のみ）。声調番号は入力しません。

以下の五枚で方案の全体が分かります。ほかの二つのリポジトリと同じ図を言語ごとに用意したもので、内容は各言語版で一致しています：

![西安方言の声母（城区音 26；南郊音 25——rh あり、bf・pf なし）](figures/onsets.ja.svg)

![西安方言の韻母（城区音 40；南郊音 38、uu・iai なし）](figures/rhymes.ja.svg)

![西安方言の四声](figures/tones.ja.svg)

![音節の構造：声母＋韻母＋声調番号](figures/syllable.ja.svg)

![入力側の略式綴り（8 つのルール）](figures/abbrev.ja.svg)

声母・韻母の分布規則、正書法の細則、普通話ピンインとの項目別の対照、使える簡拼まで含む完全な説明は、入力法リポジトリの [README](https://github.com/SiqYin/xinganhua-fuvufa)（[简体](https://github.com/SiqYin/xinganhua-fuvufa/blob/main/README.md) ／ [繁體](https://github.com/SiqYin/xinganhua-fuvufa/blob/main/README.zh-Hant.md) ／ [English](https://github.com/SiqYin/xinganhua-fuvufa/blob/main/README.en.md) ／ [日本語](https://github.com/SiqYin/xinganhua-fuvufa/blob/main/README.ja.md)）を参照してください。字音は[字音検索サイト](https://siqyin.github.io/xinganhua-ziyencaxin/)で引けます。

---

<a id="s2"></a>

## 2. これは何か

本リポジトリは [fcitx5-android](https://github.com/fcitx5-android/fcitx5-android)（小企鹅输入法）のカスタム分支で、西安方言の直装パッケージ専用です。

Fcitx5 for Android は入力法の**枠組み**です。キーボード・候補バー・テーマを持ち、中国語入力はプラグインに任せます：ピンイン、双拼、五筆、倉頡、そして任意の Rime 方案を読み込める **Rime プラグイン（中州韵）**です。

ここでは入力法を書き直しません。やることは三つだけ：

1. **方案をプラグインに入れる**：`chengqyu`・`nanjiao` の六つのファイルを Rime プラグインに同梱して `rime-data` へ入れ、`default.yaml` の `schema_list` の先頭に置く
2. **署名を揃える**：本体とプラグインを同じ公開鍵で署名する。揃っていないと本体がプラグインを認識しない
3. **二つを配る**：ビルドするのは本体と Rime プラグインだけ、ABI ごとに 4 つずつ。この導入説明を添えて公開する

つまり公開しているのは、**西安方言の方案を組み込んだ Fcitx5 for Android の本体** ＋ **同じ Rime プラグイン** ＋ **導入と使い方の案内**です。中身はあくまで Fcitx5 for Android で、箱を開けたら西安方言が打てる、という違いだけです。

---

<a id="s3"></a>

## 3. ダウンロードとインストール

### 3.1 ファイルを取る

- **Releases**（推奨）：<https://github.com/SiqYin/android-xinganhua/releases> 。最新版（執筆時点は `v1.1.1`）に APK が 8 個あります：
  - 本体：`org.fcitx.fcitx5.android-…-<abi>-release.apk`
  - プラグイン：`org.fcitx.fcitx5.android.plugin.rime-…-<abi>-release.apk`
- **Actions**：`Build Custom APK` ワークフローの成果物では、`fcitx5-android-custom` が本体、`fcitx5-plugins` に Rime プラグインが入っています。

ABI の選び方：現在のスマートフォンはほぼ **`arm64-v8a`**。古い 32 bit 機は `armeabi-v7a`、エミュレータは環境に合わせて `x86` / `x86_64`。**本体とプラグインは同じ ABI** でないとプラグインが読み込まれません。

### 3.2 先に公式版を削除する

本パッケージは公式の Fcitx5 for Android と**同じパッケージ名**（`org.fcitx.fcitx5.android`）で**署名が異なります**。共存も上書き更新もできません。インストール前に、端末にある公式版（および他の改変版）を削除してください。

### 3.3 インストールの順序

1. **本体**（`org.fcitx.fcitx5.android-…`）を入れる
2. **Rime プラグイン**（`org.fcitx.fcitx5.android.plugin.rime-…`）を入れる
3. 両方入れてからキーボードを開く。プラグインが先でも構いませんが、**どちらも必要**です

### 3.4 キーボードを有効にする

設定 →「言語と入力」→「画面キーボード / キーボードの管理」→ **Fcitx5** をオン → 入力法の選択で Fcitx5 に切り替え。メーカーによって経路が違うので、「入力法」で検索すると早いです。

### 3.5「中州韵」を追加し、「西安話城區音」または「西安話南郊音」を選ぶ

1. Fcitx5 for Android のアプリを開き、「入力法」の画面で「＋」を押して **中州韵（Rime）** を追加
2. Rime の設定で **デプロイ**（Deploy）を一度押す。プラグインが `rime-data` の方案をコンパイルします
3. キーボードに戻り、方案メニュー（〔方案選單〕、または `Ctrl` + `` ` ``、`F4`）で **西安話** を選ぶ
4. あとは打つだけ：`ba1` → 巴、`bfeng4` → 中、`nge3` → 我。声調番号は省略可で、`ba` なら四声すべて出ます

### 3.6 西安方言が出てこないとき

| 症状 | まず見る |
|---|---|
| 入力法の一覧に「中州韵」がない | プラグイン未導入、または別 ABI を入れた。同じ ABI の Rime プラグインを追加 |
| 「中州韵」はあるが「西安話城區音」がない | デプロイを押していない、または失敗。Rime の設定で再デプロイ |
| 英語は打てるが中国語が出ない | キーボードが Rime になっていない（スペースキー横の方案名を確認） |
| 逆引き（`q` ＋普通話ピンイン、`x` ＋画数）が使えない | `luna_pinyin` / `stroke` が入っていない。同じ版の Rime プラグインを入れ直す |

---

<a id="s4"></a>

## 4. 方案の組み込み方

```
plugin/rime/src/main/cpp/rime-xinganhua/   二套の方案（xinganhua-fuvufa からコピー）
├── chengqyu.schema.yaml                   西安方言城区音：字母表、簡拼の演算、逆引き Q/X
├── chengqyu.dict.yaml                     城区音の主辞書。import_tables が字音表を指す
├── chengqyu.word.dict.yaml                城区音字音表 3,648 件
├── nanjiao.schema.yaml                    西安方言南郊音（声母 25——rh を含む、韻母 38）
├── nanjiao.dict.yaml                      南郊音の主辞書
└── nanjiao.word.dict.yaml                 南郊音字音表 4,350 件
plugin/rime/src/main/cpp/default.yaml      schema_list の先頭が chengqyu、nanjiao
plugin/rime/src/main/cpp/CMakeLists.txt    六つのファイルを rime-data へインストール
.github/workflows/build-custom.yml         :app と :plugin:rime だけをビルドし、APK 8 個を出す
```

- 方案は**コピー**で取り込んでおり、submodule ではありません。方案リポジトリが更新されたら、六つのファイルを同期し直して再ビルドが必要です。自動では追随しません。
- 逆引きは `luna_pinyin`（普通話）と `stroke`（画数）に依存します。どちらも Rime プラグインが元から入れるので、方案側で同梱する必要はありません。
- CI が出すのは本体と Rime プラグインの二種類だけ。他のプラグイン（注音・粤拼・日本語・韓国語など）は包みません。包むものが増えないぶん、上流と同じ大きさに収まります。
- 本体とプラグインは `SIGN_KEY_BASE64` / `SIGN_KEY_PWD` / `SIGN_KEY_ALIAS` の三つの secrets で署名します。一つでも欠けると CI は失敗します。インストールできない包みを出さないためです。

---

<a id="s5"></a>

## 5. 方案リポジトリとの関係

```
MCPDict「西安」データ表（国際音声記号）
        │  tools/ipa2pinyin.mjs
        ▼
xinganhua-fuvufa（方案・字表・説明）
        │  yaml 六つをコピー
        ▼
android-xinganhua（本体＋Rime プラグイン → APK 8 個）
```

| 項目 | 数 |
|---|---|
| 字音項目 | 城区音 3,648 ／ 南郊音 4,350（一字一音一行） |
| 字頭 | 城区 3,345 ／ 南郊 4,065（渭南独占などの追加 720 字を含む） |
| 多音字 | 城区 275 ／ 南郊 223 |
| 声調なし音節 | 城区 392 ／ 南郊 389 |

本リポジトリは方案の中身を変えません。読みや綴りに問題があれば、[xinganhua-fuvufa](https://github.com/SiqYin/xinganhua-fuvufa) の字表を直して生成スクリプトを走らせ、新しい六つのファイルをこちらへ同期してください。

---

<a id="s6"></a>

## 6. 自分でビルドする

ビルド方法は上流と同じです（Android SDK、NDK、CMake、`extra-cmake-modules`、`gettext`、そして `git submodule update --init --recursive`）。詳細は上流の README を見てください。本リポジトリで関係するのは二つのモジュールだけです：

```sh
./gradlew :app:assembleRelease            # 本体
./gradlew :plugin:rime:assembleRelease    # Rime プラグイン
```

リリース版には署名の設定が要ります。鍵がない場合は debug 版を自分用に作れますが、debug と release では署名が違うため、プラグインも同じビルドのものを使う必要があります。

---

<a id="s7"></a>

## 7. 上流と謝辞

- [fcitx5-android](https://github.com/fcitx5-android/fcitx5-android) —— 上流。キーボード、枠組み、プラグインの仕組みはここから
- [fcitx5](https://github.com/fcitx/fcitx5) と [librime](https://github.com/rime/librime) —— 枠組みと Rime エンジン
- [xinganhua-fuvufa](https://github.com/SiqYin/xinganhua-fuvufa) —— 西安方言ピンインの方案、字表、四言語の説明
- [osfans/MCPDict](https://github.com/osfans/MCPDict) —— 字音データの出所
- [fcitx5-wugniu](https://github.com/SiqYin/fcitx5-wugniu) —— 呉語の直装パッケージ。本リポジトリの包み方はこれを参照

---

<a id="s8"></a>

## 8. ライセンス

本リポジトリは上流の **LGPL-2.1**（`LICENSE` を参照）に従い、上流コードへの改変も同じ LGPL-2.1 で公開します。西安方言の方案と字表は [xinganhua-fuvufa](https://github.com/SiqYin/xinganhua-fuvufa)、字音データは MCPDict に由来するため、それぞれのプロジェクトの説明に従ってください。

---

## 注記

簡体中文版が原文で、繁體中文版は OpenCC による変換、English 版と日本語版は対応する翻訳です。四版は内容を同一に保つ想定で、相違があれば簡体版を正とします。本文は AI の補助を受けて作成・翻訳しました。
