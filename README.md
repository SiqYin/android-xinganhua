**简体中文** ｜ [繁體中文](README.zh-Hant.md) ｜ [English](README.en.md) ｜ [日本語](README.ja.md)

# 西安话输入法 · 安卓直装版 · android-xinganhua

> 为 [fcitx5-android](https://github.com/fcitx5-android/fcitx5-android)（小企鹅输入法）预置西安话方案的安卓直装包：安装本体与 Rime 插件后切至「中州韵」，即可选用**西安話城區音**或**西安話南郊音**直接打字，不必自行导入方案文件。

- **系统支持**：Android 6.0 及以上（`minSdk 23`），提供 `arm64-v8a` / `armeabi-v7a` / `x86` / `x86_64` 四个 ABI
- **发布产物**：8 个 APK（输入法本体 × 4 ABI ＋ Rime 插件 × 4 ABI），共用同一把签名密钥
- **内置方案**：`chengqyu`（西安话城区音）、`nanjiao`（西安话南郊音），编入插件 `rime-data` 并列于方案选单前两位
- **包名约定**：`org.fcitx.fcitx5.android`（与上游同包名而签名不同，装前需先卸载官方版）
- **方案源库**：[xinganhua-fuvufa](https://github.com/SiqYin/xinganhua-fuvufa)（本仓只打包同步，不单独改字音）

---

## 目录

1. [西安话拼音方案](#s1)
2. [项目定位](#s2)
3. [下载与安装](#s3)
4. [内置结构说明](#s4)
5. [与方案库及小鸢一体包的关系](#s5)
6. [本地自行构建](#s6)
7. [上游与致谢](#s7)
8. [授权许可](#s8)

---

<a id="s1"></a>

## 一、西安话拼音方案

本直装包、桌面端 Rime 与在线字音站共用同一套**西安话拼音**（含城区音、南郊音两套字表）。音节由「声母 + 韵母 + 调号」组成，例如 `ba1` 巴、`jyuen1` 軍；「中」在城区音作 `bfeng4`，在南郊音作 `zung4`：

- **声母**：两支共用 24 个（含零声母），城区音另有 `bf`、`pf`（共 26），南郊音另有 `rh`（共 25）。依次排作：`b p m bf pf f v` / `d t n l` / `g k h ng` / `j q x` / `zh ch sh r` / `z c s rh`（`n` 逢 `i`、`y` 细音读 `[ȵ]`）。
- **韵母**：城区音 39 个（开 14 ／ 齐 10 ／ 合 9 ／ 撮 6，含 `uu`、`iae`、`uong`），南郊音 37 个（开 13 ／ 齐 9 ／ 合 9 ／ 撮 6，无 `uu`、`iae`，合口鼻尾韵直接拼作 `ung`）。
- **四声**：阴平 31、阳平 24、上声 53、去声 55，古入声已并入四调；调号紧贴音节末尾，打字时可省略。
- **隔音撇号**：音节连写易误切处用 `'` 隔开（如 `xi'ngan1` 西安）。
- **输入简拼**：两支共用的规则为 `in / iu / o / ui / un`（限前有辅音声母，对应 `ien / iou / uo / uei / uen`）、`o`（`j q x` 后的 `yuo`：`jo / qo / xo`）、`yo`（零声母与 `n` 后的 `yuo`）与 `yun`（对应 `yuen`）；至于 `uong → ung`，**城区音中拼音可以这样简化，南郊音本来的拼写就是后者（`ung`）**。

下面六张图展示完整音系与拼写规则：

![西安话声母（城区音 26；南郊音 25——多 rh，无 bf、pf）](figures/onsets.hans.svg)

![西安话韵母（城区音 39；南郊音 37，无 uu、iae）](figures/rhymes.hans.svg)

![西安话四声](figures/tones.hans.svg)

**连读变调**：两字连读主要由前字变调——连续两个阴平（`31-31`）前字改读阳平（`24-31`）；连续两个上声（`53-53`）前字改读阴平（`31-53`）。

![音节结构：声母 + 韵母 + 调号](figures/syllable.hans.svg)

![西安话简拼对照图（城区 9 条 · 南郊 8 条）](figures/abbrev.hans.svg)

![南郊音的变体](figures/variant.hans.svg)

**南郊音变体**：南郊音 `z`、`c`、`s`、`rh` 接 `u` 韵母时另有 `zh`、`ch`、`sh`、`r` 翘舌变体，其中 `sh` 拼 `u` 时另有 `f` 变体；变体只加注在城区音读 `bf`、`pf`、`f`、`v` 的字及审定的渭南独有字上（如「水」南郊作 `suei3`，另有变体 `shuei3`、`fei3`），与本读音同调并一并编入词库。

完整的分布细则与普通话对照详见 [xinganhua-fuvufa](https://github.com/SiqYin/xinganhua-fuvufa)（[简体](https://github.com/SiqYin/xinganhua-fuvufa/blob/main/README.md) ／ [繁體](https://github.com/SiqYin/xinganhua-fuvufa/blob/main/README.zh-Hant.md) ／ [English](https://github.com/SiqYin/xinganhua-fuvufa/blob/main/README.en.md) ／ [日本語](https://github.com/SiqYin/xinganhua-fuvufa/blob/main/README.ja.md)）；单字查音可访问[字音查询站](https://siqyin.github.io/xinganhua-ziyencaxin/)。

---

<a id="s2"></a>

## 二、项目定位

本仓库是 [fcitx5-android](https://github.com/fcitx5-android/fcitx5-android) 的定制打包分支，不动用输入法上层交互与核心引擎，只负责三项打包工作：

1. **预置方案**：将 `chengqyu` 与 `nanjiao` 的六个 `.yaml` 文件随 Rime 插件写入 `rime-data`，并在 `default.yaml` 的 `schema_list` 中置顶；
2. **统一签名**：用同一把签名证书签署本体与 Rime 插件，使插件能被本体正常加载；
3. **精简产物**：CI 仅构建 `:app` 与 `:plugin:rime` 两个模块（各 4 个 ABI），不夹带其余语言插件。

---

<a id="s3"></a>

## 三、下载与安装

### 3.1 获取安装包

- **Releases**（推荐）：<https://github.com/SiqYin/android-xinganhua/releases> ，新版（如 `v1.1.13`）附带 8 个 APK：
  - 本体：`org.fcitx.fcitx5.android-…-<abi>-release.apk`
  - 插件：`org.fcitx.fcitx5.android.plugin.rime-…-<abi>-release.apk`
- **Actions**：`Build Custom APK` 产物中的 `fcitx5-android-custom` 为本体、`fcitx5-plugins` 内为 Rime 插件。

**ABI 选择**：现代手机大多选 **`arm64-v8a`**；老旧 32 位设备选 `armeabi-v7a`；模拟器按宿主架构选 `x86` 或 `x86_64`。**本体与插件必须同 ABI**。

### 3.2 卸载冲突版本

本包与官方版小企鹅同用 `org.fcitx.fcitx5.android` 包名但签名不同，安装前请先卸载手机上的官方版及其他第三方签名改版，否则系统会拒装。

### 3.3 安装与启用

1. 安装同 ABI 的**本体** APK 与 **Rime 插件** APK（安装顺序任意，两者须齐全）。
2. 在系统「语言和输入法」设置中启用 **Fcitx5** 并设为当前键盘。
3. 打开小企鹅 App →「输入法」→ 点击「＋」添加 **中州韵（Rime）**，进 Rime 设置点一次 **部署**（Deploy）。
4. 回到键盘通过方案选单切至 **西安話城區音** 或 **西安話南郊音** 即可输入（如 `ba1` → 巴、`bfeng4` → 中、`nge3` → 我；省去调号也可）。

### 3.4 常见排查

| 现象 | 排查方向 |
|---|---|
| 列表里找不到「中州韵」 | 未安装 Rime 插件，或本体与插件 ABI 不一致 |
| 有「中州韵」却看不到「西安話」 | 初次未点「部署」，或部署失败；进 Rime 设置重新部署 |
| 只能出英文不出汉字 | 当前键盘停留在英文方案，点击空格旁方案名切到 Rime |
| 普通话反查（`` ` `` + 拼音）无效 | `luna_pinyin` 未随插件到位，重装同版本 Rime 插件 |

---

<a id="s4"></a>

## 四、内置结构说明

```
plugin/rime/src/main/cpp/rime-xinganhua/   两套西安话方案（同步自 xinganhua-fuvufa）
├── chengqyu.schema.yaml                   城区音方案（简拼演算与 ` 反查）
├── chengqyu.dict.yaml                     城区音主词典
├── chengqyu.word.dict.yaml                城区音字音表（3,649 条）
├── nanjiao.schema.yaml                    南郊音方案（25 声母、37 韵母）
├── nanjiao.dict.yaml                      南郊音主词典
└── nanjiao.word.dict.yaml                 南郊音字音表（4,596 条）
plugin/rime/src/main/cpp/default.yaml      schema_list 置顶 chengqyu、nanjiao
plugin/rime/src/main/cpp/CMakeLists.txt    将方案与词典安装进 rime-data
.github/workflows/build-custom.yml         构建 :app 与 :plugin:rime，生成 8 APK
```

普通话反查依赖内置的 `luna_pinyin`；`x` 已作为西安话正式声母，旧笔画反查已随方案撤除。构建机以 `nanjiao.word.dict.yaml` 中的 `version` 字段作为 APK 版本名基准，并由 `SIGN_KEY_BASE64` / `SIGN_KEY_PWD` / `SIGN_KEY_ALIAS` 统一签名。

---

<a id="s5"></a>

## 五、与方案库及小鸢一体包的关系

```
MCPDict《西安》数据表（国际音标）
        │  tools/ipa2pinyin.mjs
        ▼
xinganhua-fuvufa（方案、字表、配图）
        │  同步六个 yaml
        ▼
android-xinganhua（本体 + Rime 插件 → 8 个 APK）
```

| 项 | 城区音 | 南郊音 |
|---|---|---|
| 字音条目 | 3,649 | 4,596（一字一音一行） |
| 字头 | 3,346 | 4,065（含增补 720 字） |
| 多音字 | 275 | 428（不含变体 256） |
| 不计调音节 | 392 | 421 |

字音修订均在 [xinganhua-fuvufa](https://github.com/SiqYin/xinganhua-fuvufa) 完成，之后再把六个 `.yaml` 同步到本仓重新打包。

### 一体包：小鸢输入法（Iris Keyboard）

若希望免去「先装本体再装插件并手动部署」的步骤，可直接选用 [小鸢输入法 Iris Keyboard](https://github.com/SiqYin/fcitx5-iris)（`SiqYin/fcitx5-iris`）。该仓库将本体与 Rime 插件合入单个 APK，预编译好西安话（城区音／南郊音）与吴语方案共四套词库，安装后即可直接使用。

---

<a id="s6"></a>

## 六、本地自行构建

构建环境与上游一致（Android SDK、NDK、CMake、`extra-cmake-modules`、`gettext` 及 `git submodule update --init --recursive`），编译核心模块：

```sh
./gradlew :app:assembleRelease
./gradlew :plugin:rime:assembleRelease
```

---

<a id="s7"></a>

## 七、上游与致谢

- [fcitx5-android](https://github.com/fcitx5-android/fcitx5-android)、[fcitx5](https://github.com/fcitx/fcitx5) 与 [librime](https://github.com/rime/librime) —— 输入法框架与 Rime 引擎。
- [xinganhua-fuvufa](https://github.com/SiqYin/xinganhua-fuvufa) —— 西安话拼音方案、词库与配图。
- [西安话音档](https://github.com/osfans/MCPDict/blob/master/tools/tables/data/%E8%A5%BF%E5%AE%89.tsv)、[渭南话音档](https://github.com/osfans/MCPDict/blob/master/tools/tables/data/%E6%B8%AD%E5%8D%97.tsv)、[华县话音档](https://github.com/osfans/MCPDict/blob/master/tools%2Ftables%2Fdata%2F%E5%8D%8E%E5%8E%BF.tsv)、[临潼话音档](https://github.com/osfans/MCPDict/blob/master/tools%2Ftables%2Fdata%2F%E4%B8%B4%E6%BD%BC%E6%96%B9%E8%A8%80%E8%AF%AD%E9%9F%B3%E7%A0%94%E7%A9%B6.tsv)（[osfans/MCPDict](https://github.com/osfans/MCPDict)）。**南郊话音档**在四档底本上参考知乎关于南郊、东郊平翘舌合流讨论并与家人日常读音核对整理而成，**仅供参考**。
- [fcitx5-wugniu](https://github.com/SiqYin/fcitx5-wugniu) —— 打包脚本与发布流程参照。

---

<a id="s8"></a>

## 八、授权许可

本仓库代码遵循上游 **LGPL-2.1**（见 `LICENSE`）。内置西安话方案与词库源于 [xinganhua-fuvufa](https://github.com/SiqYin/xinganhua-fuvufa)，字音原始数据版权遵循 MCPDict 原项目说明。
