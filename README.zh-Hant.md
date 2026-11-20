[簡體中文](README.md) ｜ **繁體中文** ｜ [English](README.en.md) ｜ [日本語](README.ja.md)

# 西安話輸入法 · 安卓直裝版 · android-xinganhua

> 把西安話輸入法做成安卓直裝包：裝上**小企鵝輸入法**（Fcitx5 for Android）的**本體**與 **Rime 插件**，切到「中州韻」再選「西安話城區音」或「西安話南郊音」，就能用西安話拼音打字——不必自己往手機裏導入方案。

- **平臺**：Android 6.0 及以上（minSdk 23）；`arm64-v8a` / `armeabi-v7a` / `x86` / `x86_64` 四個 ABI
- **發佈物**：8 個 APK = 本體 × 4 ABI ＋ Rime 插件 × 4 ABI，都是同一把密鑰簽名
- **內置方案**：`chengqyu`（西安話城區音）、`nanjiao`（西安話南郊音），隨插件裝進 `rime-data`，在方案選單裏排前兩位
- **包名**：`org.fcitx.fcitx5.android`（與官方版相同、簽名不同；裝前先卸掉官方版）
- **方案源庫**：[xinganhua-fuvufa](https://github.com/SiqYin/xinganhua-fuvufa)（只讀引用，本倉庫不改方案內容）
- **四種語言**：簡體 / 繁體 / English / 日本語，頂部的鏈接可直接切換；四版內容一致，以簡體版爲準

---

## 目錄

1. [西安話拼音方案](#s1)
2. [這是什麼](#s2)
3. [下載與安裝](#s3)
4. [內置方式：本倉庫改了什麼](#s4)
5. [與方案倉庫的關係](#s5)
6. [自行構建](#s6)
7. [上游與致謝](#s7)
8. [授權](#s8)

---

<a id="s1"></a>

## 一、西安話拼音方案

無論是手機上的小企鵝，還是電腦上的 Rime、另外兩個倉庫，用的都是同一套**西安話拼音**，城區音、南郊音各一套。一個音節寫成「聲母 + 韻母 + 調號」，例如 `ba1` 巴、`jyuen1` 軍；`bfeng4` 中是城區音，南郊音作 `zuong4`：

- **聲母**：兩套共用 24 個（含零聲母），城區音另有 `bf`、`pf`（共 26），南郊音另有 `rh`（共 25）：`b p m f v bf pf d t n l z c s rh j q x zh ch sh r g k h ng`
- **韻母**：兩套共用 38 個（開 15 ／ 齊 8 ／ 合 9 ／ 撮 6），城區音另有 `uu`、`iai`，共 40 個（開 16 ／ 齊 9 ／ 合 9 ／ 撮 6）
- **四聲**：陰平 21、陽平 24、上聲 53、去聲 44；入聲已併入四調
- **調號緊貼音節**，不空格：`bfeng4` 中、`jyuen1` 軍
- **音節邊界用撇號**：`xi'ngan1` 西安（否則會被切成 xin 心 + gan 幹）
輸入端可用簡拼：`in / ing / iu / ui / un / ung / yun / yung`（分別對應 `ien / ieng / iou / uei / uen / uong / yuen / yuong`；零聲母只放行 `yuen`、`yuong`）；調號不輸入。

下面五張圖把方案講全（與其他兩個倉庫用的是同一套圖，各語言版本內容一致）：

![西安話聲母（城區音 26；南郊音 25——多 rh，無 bf、pf）](figures/onsets.hant.svg)

![西安話韻母（城區音 40；南郊音 38，無 uu、iai）](figures/rhymes.hant.svg)

![西安話四聲](figures/tones.hant.svg)

![音節結構：聲母 + 韻母 + 調號](figures/syllable.hant.svg)

![西安話簡拼對照圖（輸入端 8 條縮寫規則）](figures/abbrev.hant.svg)

方案的完整說明——聲母韻母的分佈規則、正字法細則、與普通話拼音的逐條對照、可用的簡拼——見輸入法倉庫的 [README](https://github.com/SiqYin/xinganhua-fuvufa)（[簡體](https://github.com/SiqYin/xinganhua-fuvufa/blob/main/README.md) ／ [繁體](https://github.com/SiqYin/xinganhua-fuvufa/blob/main/README.zh-Hant.md) ／ [English](https://github.com/SiqYin/xinganhua-fuvufa/blob/main/README.en.md) ／ [日本語](https://github.com/SiqYin/xinganhua-fuvufa/blob/main/README.ja.md)）。查字音可以用[字音查詢站](https://siqyin.github.io/xinganhua-ziyencaxin/)。

---

<a id="s2"></a>

## 二、這是什麼

本倉庫是 [fcitx5-android](https://github.com/fcitx5-android/fcitx5-android)（小企鵝輸入法）的定製分支，專門爲西安話做安卓直裝包。

小企鵝輸入法本身是個輸入法**框架**——Fcitx5 的安卓移植，自帶鍵盤、候選欄、主題，中文輸入則交給插件：拼音、雙拼、五筆、倉頡，以及能加載任意 Rime 方案的 **Rime 插件（中州韻）**。

所以這裏不重寫輸入法，只做三件事：

1. **把方案放進插件**：`chengqyu`、`nanjiao` 兩套方案的六個文件隨 Rime 插件裝進 `rime-data`，並在 `default.yaml` 的 `schema_list` 裏排前兩位；
2. **統一簽名**：本體與插件用同一把發佈密鑰，插件纔會被本體認下來；
3. **把包發出來**：只構建本體與 Rime 插件，四個 ABI 各一套，附這份安裝說明。

換句話說，我們發佈的內容就是：**改過、內置了西安話城區音與南郊音兩套方案的小企鵝輸入法本體** ＋ **同一個 Rime 插件** ＋ **下載安裝使用的引導**。裝的還是小企鵝，只是開箱就能打西安話。

---

<a id="s3"></a>

## 三、下載與安裝

### 3.1 取包

- **Releases**（推薦）：<https://github.com/SiqYin/android-xinganhua/releases> ，最新版（寫作時爲 `v1.1.1`）共 8 個 APK：
  - 本體：`org.fcitx.fcitx5.android-…-<abi>-release.apk`
  - 插件：`org.fcitx.fcitx5.android.plugin.rime-…-<abi>-release.apk`
- **Actions**：`Build Custom APK` 工作流的產物裏，`fcitx5-android-custom` 是本體，`fcitx5-plugins` 裏是 Rime 插件。

ABI 怎麼選：現在的手機基本都選 **`arm64-v8a`**；很老的 32 位機選 `armeabi-v7a`；模擬器按自己的架構選 `x86` / `x86_64`。**本體和插件必須是同一個 ABI**，否則插件不會被加載。

### 3.2 先卸掉官方版

本包與官方小企鵝**同包名**（`org.fcitx.fcitx5.android`）但**簽名不同**，兩者不能共存，也不能互相覆蓋升級。裝之前請先卸載機器上的官方版（以及其它改版），再裝本包。

### 3.3 安裝順序

1. 裝**本體**（`org.fcitx.fcitx5.android-…`）；
2. 裝 **Rime 插件**（`org.fcitx.fcitx5.android.plugin.rime-…`）；
3. 兩個都裝完再打開輸入法，先裝插件後裝本體也可以，但**都要裝**。

### 3.4 啓用輸入法

系統設置 →「語言和輸入法」→「屏幕鍵盤 / 管理鍵盤」→ 打開 **Fcitx5**（小企鵝輸入法）→ 在輸入法選擇器裏切到它。不同廠商的設置路徑略有出入，找不到就搜「輸入法」。

### 3.5 加上「中州韻」，選「西安話」

1. 打開小企鵝輸入法的 App，進「輸入法」頁，點「＋」添加 **中州韻（Rime）**；
2. 在 Rime 的設置裏點一次 **部署**（Deploy），讓插件把 `rime-data` 裏的方案編譯出來；
3. 回到鍵盤，用方案選單（〔方案選單〕，或 `Ctrl` + `` ` ``、`F4`）切到 **西安話城區音** 或 **西安話南郊音**；
4. 直接打：`ba1` → 巴，`bfeng4` → 中，`nge3` → 我。調號可省，打 `ba` 出四個調。

### 3.6 打不出西安話？

| 現象 | 先查 |
|---|---|
| 輸入法列表裏沒有「中州韻」 | 插件沒裝，或裝成了另一個 ABI；補裝同 ABI 的 Rime 插件 |
| 有「中州韻」但沒有「西安話」 | 沒點「部署」，或部署失敗；進 Rime 設置重新部署一次 |
| 能打英文，中文出不來 | 鍵盤上的輸入法沒切到 Rime（看空格鍵旁的方案名） |
| 反查（`q` + 普通話拼音、`x` + 筆畫）不可用 | `luna_pinyin` / `stroke` 沒隨插件裝上；重裝同版本的 Rime 插件 |

---

<a id="s4"></a>

## 四、內置方式：本倉庫改了什麼

```
plugin/rime/src/main/cpp/rime-xinganhua/   兩套方案（拷貝自 xinganhua-fuvufa）
├── chengqyu.schema.yaml                   西安話城區音：字母表、簡拼演算、反查 Q/X
├── chengqyu.dict.yaml                     城區音主詞典，import_tables 指向字音表
├── chengqyu.word.dict.yaml                城區音字音表 3,648 條
├── nanjiao.schema.yaml                    西安話南郊音（聲母 25 含 rh、韻母 38）
├── nanjiao.dict.yaml                      南郊音主詞典
└── nanjiao.word.dict.yaml                 南郊音字音表 4,350 條
plugin/rime/src/main/cpp/default.yaml      schema_list 前兩項 = chengqyu、nanjiao
plugin/rime/src/main/cpp/CMakeLists.txt    三個文件安裝到 rime-data
.github/workflows/build-custom.yml         只構建 :app 與 :plugin:rime，出 8 個 APK
```

- 方案是**拷貝**進來的，不是 submodule。方案倉庫更新後，要重新同步這六個文件再出包，兩邊不會自動跟。
- 反查依賴 `luna_pinyin`（普通話）與 `stroke`（筆畫），這兩個上游方案本來就隨 Rime 插件裝好，所以方案裏不用再帶。
- CI 只出兩類包：本體和 Rime 插件。其它插件（注音、粵拼、日文、韓文……）不打包，包體和上游一致，不會因爲多帶插件而變大。
- 本體與插件都用 `SIGN_KEY_BASE64` / `SIGN_KEY_PWD` / `SIGN_KEY_ALIAS` 這三項 secrets 簽名；缺一項，CI 直接失敗，避免發出裝不上的包。

---

<a id="s5"></a>

## 五、與方案倉庫的關係

```
MCPDict《西安》數據表（國際音標）
        │  tools/ipa2pinyin.mjs
        ▼
xinganhua-fuvufa（方案、字表、說明）
        │  拷貝三個 yaml
        ▼
android-xinganhua（本體 + Rime 插件 → 8 個 APK）
```

| 項 | 城區音 | 南郊音 |
|---|---|---|
| 字音條目 | 3,648 | 4,350（一字一音一行） |
| 字頭 | 3,345 | 4,065（含渭南獨有等新增 720 字） |
| 多音字 | 275 | 223 |
| 不計調音節 | 392 | 389 |

本倉庫不改方案內容：發現讀音或拼寫有問題，請改 [xinganhua-fuvufa](https://github.com/SiqYin/xinganhua-fuvufa) 的字表（城區音 `data/source.tsv`、南郊音字表）後重跑生成腳本，再把新的六個文件同步過來。

---

<a id="s6"></a>

## 六、自行構建

構建方式與上游一致（Android SDK、NDK、CMake、`extra-cmake-modules`、`gettext`，以及 `git submodule update --init --recursive`），細節見上游 README。本倉庫只關心兩個模塊：

```sh
./gradlew :app:assembleRelease            # 本體
./gradlew :plugin:rime:assembleRelease    # Rime 插件
```

本地出正式包同樣需要簽名配置；沒有密鑰時可以先出 debug 包自用（debug 與 release 簽名不同，插件要裝同一次構建的 debug 版本纔會被識別）。

---

<a id="s7"></a>

## 七、上游與致謝

- [fcitx5-android](https://github.com/fcitx5-android/fcitx5-android)（小企鵝輸入法）——本倉庫的上游，鍵盤、框架與插件體系都來自這裏
- [fcitx5](https://github.com/fcitx/fcitx5) 與 [librime](https://github.com/rime/librime) ——框架與 Rime 引擎
- [xinganhua-fuvufa](https://github.com/SiqYin/xinganhua-fuvufa) ——西安話拼音方案、字表與四語說明
- [osfans/MCPDict](https://github.com/osfans/MCPDict) ——字音數據源
- [fcitx5-wugniu](https://github.com/SiqYin/fcitx5-wugniu) ——吳語直裝包，本倉庫的打包做法參照

---

<a id="s8"></a>

## 八、授權

本倉庫沿用上游的 **LGPL-2.1**（見 `LICENSE`）；對上游代碼的修改同樣按 LGPL-2.1 發佈。西安話方案與字表來自 [xinganhua-fuvufa](https://github.com/SiqYin/xinganhua-fuvufa)，字音數據來自 MCPDict，版權與授權請遵循各自項目說明。

---

## 聲明

簡體版爲源文；繁體版由 OpenCC 從簡體轉出，英文與日文版爲對應譯本。四版內容一致，如有出入以簡體版爲準。本文由 AI 輔助撰寫與翻譯。
