[简体中文](README.md) ｜ [繁體中文](README.zh-Hant.md) ｜ **English** ｜ [日本語](README.ja.md)

# Xi'an Dialect Input Method · Android Build · android-xinganhua

> Ready-to-install [fcitx5-android](https://github.com/fcitx5-android/fcitx5-android) packages with Xi'an dialect schemas pre-installed: install the app and Rime plugin, switch to Rime (中州韵), and choose **西安話城區音** (urban) or **西安話南郊音** (southern suburb) with no manual file import.

- **Target platform**: Android 6.0+ (`minSdk 23`) across `arm64-v8a`, `armeabi-v7a`, `x86`, and `x86_64`
- **Release artifacts**: 8 APKs (app × 4 ABIs + Rime plugin × 4 ABIs), signed with the same key
- **Bundled schemas**: `chengqyu` (urban) and `nanjiao` (southern suburb), placed first in `schema_list`
- **Package ID**: `org.fcitx.fcitx5.android` (matches upstream package name with a different signature — uninstall official builds first)
- **Scheme source**: [xinganhua-fuvufa](https://github.com/SiqYin/xinganhua-fuvufa)

---

## Contents

1. [The Xi'an pinyin scheme](#s1)
2. [Scope of this build](#s2)
3. [Download and installation](#s3)
4. [Internal layout](#s4)
5. [Scheme sync and Iris Keyboard all-in-one](#s5)
6. [Building from source](#s6)
7. [Upstream and credits](#s7)
8. [License](#s8)

---

<a id="s1"></a>

## 1. The Xi'an pinyin scheme

The Android build, desktop Rime config, and web lookup site share one **Xi'an pinyin** system covering urban and southern-suburb Xi'an (`ba1` 巴, `jyuen1` 軍; 中 is `bfeng4` in urban speech and `zung4` in the south):

- **Initials**: 24 shared (including zero initial), plus urban `bf`, `pf` (26 total) and southern `rh` (25 total): `b p m bf pf f v` / `d t n l` / `g k h ng` / `j q x` / `zh ch sh r` / `z c s rh` (`n` shifts to `[ȵ]` before `i`/`y`).
- **Finals**: 39 in urban Xi'an (14 open / 10 `i`-medial / 9 `u`-medial / 6 `ü`-medial, incl. `uu`, `iae`, `uong`), and 37 in the south (13 / 9 / 9 / 6; no `uu`/`iae`, spelling `uong` directly as `ung`).
- **Tones**: Yinping 31, Yangping 24, Shangsheng 53, Qusheng 55 (historical entering tone merged into these four); digits are optional when typing.
- **Apostrophe & shortcuts**: `'` separates ambiguous boundaries (`xi'ngan1` 西安). Both varieties share `in / iu / o / ui / un` (after an initial consonant) and `yo / yun` (incl. zero initial); for `uong → ung`, urban Xi'an pinyin can be simplified this way, whereas `ung` is already the original spelling in the southern suburb.

![Xi'an initials (urban 26; southern 25)](figures/onsets.en.svg)

![Xi'an finals (urban 39; southern 37)](figures/rhymes.en.svg)

![The four Xi'an tones](figures/tones.en.svg)

**Tone sandhi**: Disyllabic sandhi changes the first syllable: `31-31` becomes `24-31`, and `53-53` becomes `31-53`.

![Syllable structure](figures/syllable.en.svg)

![Input-side short forms](figures/abbrev.en.svg)

![Southern-suburb variants](figures/variant.en.svg)

**Southern-suburb variants**: Before `u`-series finals, southern `z`, `c`, `s`, `rh` also allow retroflex `zh`, `ch`, `sh`, `r`, and `sh+u` allows `f`. These appear on characters whose urban reading begins with `bf`, `pf`, `f`, or `v`, plus reviewed Weinan-only characters (e.g. 水 `suei3` with variants `shuei3`, `fei3`).

Full phonology documentation is hosted in [xinganhua-fuvufa](https://github.com/SiqYin/xinganhua-fuvufa) ([简体](https://github.com/SiqYin/xinganhua-fuvufa/blob/main/README.md) / [繁體](https://github.com/SiqYin/xinganhua-fuvufa/blob/main/README.zh-Hant.md) / [English](https://github.com/SiqYin/xinganhua-fuvufa/blob/main/README.en.md) / [日本語](https://github.com/SiqYin/xinganhua-fuvufa/blob/main/README.ja.md)), and character lookup is available at [xinganhua-ziyencaxin](https://siqyin.github.io/xinganhua-ziyencaxin/).

---

<a id="s2"></a>

## 2. Scope of this build

This repository keeps upstream Fcitx5 for Android intact and focuses on three packaging tasks:

1. Shipping the six `chengqyu` and `nanjiao` `.yaml` files inside the Rime plugin's `rime-data` directory and placing them at the top of `default.yaml`.
2. Signing both the main app and Rime plugin with the same release key.
3. Building only `:app` and `:plugin:rime` across four ABIs so downloads remain compact.

---

<a id="s3"></a>

## 3. Download and installation

### 3.1 Artifacts

Download from [Releases](https://github.com/SiqYin/android-xinganhua/releases) (e.g. `v1.1.11`, 8 APKs total) or `Build Custom APK` workflow artifacts:

- App: `org.fcitx.fcitx5.android-…-<abi>-release.apk`
- Plugin: `org.fcitx.fcitx5.android.plugin.rime-…-<abi>-release.apk`

Most modern phones use **`arm64-v8a`** (`armeabi-v7a` for older 32-bit hardware; `x86` / `x86_64` for emulators). **Both APKs must match the same ABI.**

### 3.2 Uninstall upstream first

Because the package name matches upstream (`org.fcitx.fcitx5.android`) under a different signing key, uninstall any official or third-party build first.

### 3.3 Setup steps

1. Install both the main app APK and matching Rime plugin APK.
2. Enable **Fcitx5** under Android's Language & Input settings.
3. Open Fcitx5 → Input Methods → tap `+` to add **中州韵 (Rime)**, then open Rime settings and tap **Deploy**.
4. Open the schema switcher (`〔方案選單〕` or `Ctrl` + `` ` `` / `F4`) and select **西安話城區音** or **西安話南郊音** (`ba1` → 巴, `bfeng4` → 中, `nge3` → 我; tone digits optional).

### 3.4 Troubleshooting

| Symptom | Likely cause |
|---|---|
| Rime (中州韵) missing from list | Rime plugin not installed or mismatched ABI |
| Rime appears, Xi'an schemes missing | Forgot to tap Deploy in Rime settings |
| Only English types | Keyboard not switched to the Rime input method |
| Backtick reverse lookup fails | Reinstall the matching version of the Rime plugin containing `luna_pinyin` |

---

<a id="s4"></a>

## 4. Internal layout

```
plugin/rime/src/main/cpp/rime-xinganhua/   bundled schemas synced from xinganhua-fuvufa
├── chengqyu.schema.yaml                   urban schema (abbreviations + ` reverse lookup)
├── chengqyu.dict.yaml                     urban main dictionary
├── chengqyu.word.dict.yaml                urban readings (3,649)
├── nanjiao.schema.yaml                    southern schema (25 initials, 37 finals)
├── nanjiao.dict.yaml                      southern main dictionary
└── nanjiao.word.dict.yaml                 southern readings (4,594)
plugin/rime/src/main/cpp/default.yaml      schema_list puts chengqyu and nanjiao first
plugin/rime/src/main/cpp/CMakeLists.txt    installs the six files into rime-data
.github/workflows/build-custom.yml         builds :app and :plugin:rime (8 APKs)
```

Reverse lookup uses `luna_pinyin` bundled with the Rime plugin (stroke lookup was removed because `x` is a Xi'an initial). CI reads the release version directly from `nanjiao.word.dict.yaml` and signs both APKs using repository secrets.

---

<a id="s5"></a>

## 5. Scheme sync and Iris Keyboard all-in-one

```
MCPDict Xi'an table (IPA)
        │  tools/ipa2pinyin.mjs
        ▼
xinganhua-fuvufa (schemas, dictionaries, diagrams)
        │  sync 6 yaml files
        ▼
android-xinganhua (app + Rime plugin → 8 APKs)
```

| Metric | Urban (`chengqyu`) | Southern (`nanjiao`) |
|---|---|---|
| Readings | 3,649 | 4,594 |
| Characters | 3,346 | 4,065 (incl. 720 added) |
| Polyphonic characters | 275 | 428 (256 excl. variants) |
| Toneless syllables | 392 | 420 |

Edits to readings always happen first in [xinganhua-fuvufa](https://github.com/SiqYin/xinganhua-fuvufa) and are then copied here.

### All-in-one alternative: Iris Keyboard

If you prefer a single-APK installation with precompiled dictionaries and zero manual deployment, check out [Iris Keyboard (小鸢输入法)](https://github.com/SiqYin/fcitx5-iris), which bundles both Xi'an schemes and both Wu schemes in one installer.

---

<a id="s6"></a>

## 6. Building from source

Follow upstream prerequisites (Android SDK, NDK, CMake, `extra-cmake-modules`, `gettext`, and `git submodule update --init --recursive`), then run:

```sh
./gradlew :app:assembleRelease
./gradlew :plugin:rime:assembleRelease
```

---

<a id="s7"></a>

## 7. Upstream and credits

- [fcitx5-android](https://github.com/fcitx5-android/fcitx5-android), [fcitx5](https://github.com/fcitx/fcitx5), and [librime](https://github.com/rime/librime).
- [xinganhua-fuvufa](https://github.com/SiqYin/xinganhua-fuvufa) for the Xi'an schemes and dictionaries.
- [Xi'an](https://github.com/osfans/MCPDict/blob/master/tools/tables/data/%E8%A5%BF%E5%AE%89.tsv), [Weinan](https://github.com/osfans/MCPDict/blob/master/tools/tables/data/%E6%B8%AD%E5%8D%97.tsv), [Huaxian](https://github.com/osfans/MCPDict/blob/master/tools%2Ftables%2Fdata%2F%E5%8D%8E%E5%8E%BF.tsv), and [Lintong](https://github.com/osfans/MCPDict/blob/master/tools%2Ftables%2Fdata%2F%E4%B8%B4%E6%BD%BC%E6%96%B9%E8%A8%80%E8%AF%AD%E9%9F%B3%E7%A0%94%E7%A9%B6.tsv) tables from [osfans/MCPDict](https://github.com/osfans/MCPDict) (southern-suburb readings compiled for reference only).
- [fcitx5-wugniu](https://github.com/SiqYin/fcitx5-wugniu) for packaging and CI workflow conventions.

---

<a id="s8"></a>

## 8. License

Licensed under **LGPL-2.1** (see `LICENSE`), matching upstream `fcitx5-android`. The bundled Xi'an schemes come from [xinganhua-fuvufa](https://github.com/SiqYin/xinganhua-fuvufa) and underlying data follows MCPDict's terms.
