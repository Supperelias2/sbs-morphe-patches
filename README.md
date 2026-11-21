# Supperelias2 SBS Patches

Unofficial [Morphe](https://morphe.software) patches for SBS On Demand.

[Add this source to Morphe](https://morphe.software/add-source?github=Supperelias2/sbs-morphe-patches)
 · [Releases](https://github.com/Supperelias2/sbs-morphe-patches/releases)
 · [Report a problem](https://github.com/Supperelias2/sbs-morphe-patches/issues)

## What the patches do

An experimental mobile preview adds a purple **Morphe settings** row to the
account menu, above App Settings and Language. It contains persistent toggles
for installed patches and optional QoL experiments. Ad removal and the verified
intro/recap correction start enabled; other experiments start disabled.

Use the source's prerelease channel to test the preview. See the
[experimental settings guide](docs/mobile-settings-experimental.md) for features,
defaults, supported versions and phone test steps. The stable ad-removal release
remains available independently.

**Prefer direct VOD stream** removes the video ads played before and during
on-demand videos (pre-roll and mid-roll) by using SBS's direct Akamai stream.

**Prefer direct live stream** removes the extra video ads inserted before or
during live TV. Ads already present in the TV broadcast itself remain.

Both patches use the direct stream when SBS supplies one. If it is unavailable,
the app keeps its normal playback path. The maintainer has confirmed ad removal
and working VOD/live playback on a phone using **6.3.0 (16435)**. See the testing
section below for 6.4.0 validation. Location requirements are unchanged.

## Install with Morphe Manager

1. Open the source link above, or add `https://github.com/Supperelias2/sbs-morphe-patches`
   under **Sources → + → Remote**.
2. Select an original SBS 6.4.0 (16659) APKM for the QoL preview. The legacy ad/menu
   patches also support 6.3.0 (16435). Both playback patches are selected by
   default; you can disable either one if you only want VOD or live changes.
   The compatibility check is automatic.
3. For development releases, enable **Pre-release patches** for this source.
4. Patch and install using Morphe Manager. A signature conflict with the official
   app may require uninstalling that app, which removes its local data/downloads.
5. Keep Morphe's signing key for future updates. Test start, resume, seeking,
   midstream playback and live playback.

Alternatively import the release's `.mpp` file using **Sources → + → Local**.
Local imports need to be replaced manually for updates. Always patch an original
app file, not an already patched APK.

## Patches

<!-- PATCHES_START EXPANDED -->
> **[v1.2.2](https://github.com/Supperelias2/sbs-morphe-patches/releases/tag/v1.2.2)**&nbsp;&nbsp;•&nbsp;&nbsp;`main`&nbsp;&nbsp;•&nbsp;&nbsp;3 patches total
<details open>
<summary>📦 SBS On Demand&nbsp;&nbsp;•&nbsp;&nbsp;3 patches</summary>
<br>

**🎯 Supported versions:**

| 6.4.0 | 6.3.0 |
| :---: | :---: |

| 💊&nbsp;Patch | 📜&nbsp;Description | ⚙️&nbsp;Options |
|----------|----------------|-----------|
| [Prefer direct VOD stream](#prefer-direct-vod-stream) | Removes pre-roll and mid-roll video ads by selecting SBS's direct VOD stream when available. |  |
| [Prefer direct live stream](#prefer-direct-live-stream) | Removes extra video ads from live TV by selecting the direct stream when available. Ads in the broadcast remain. |  |
| [SBS playback compatibility check](#sbs-playback-compatibility-check) | Verifies the playback methods required by the VOD and live ad-removal patches. |  |

</details>

<!-- PATCHES_END -->

## Development and testing

Build with `./gradlew buildAndroid`. The bundle is written to
`patches/build/libs/patches-*.mpp`. Local builds need GitHub Packages read access;
never commit credentials. Development happens on `dev`; the existing semantic
release workflow builds releases and updates source metadata.

Validation completed: Gradle build, application to the original APKM using
Morphe Desktop 1.16.0, APK rebuild, and inspection of the modified DEX method.
Both patches together were applied to the original APKM and their guards and
fallback paths inspected in the rebuilt DEX. The live patch also passed a
standalone application/rebuild check on the base APK. The maintainer subsequently
reported successful live playback on a phone. Broader channel/device coverage
remains unverified.

SBS **6.4.0 (16659)** also passes the CLI patch-and-rebuild checks with both
playback patches enabled. The 6.3.0 regression check still passes. Playback on
a device with 6.4.0 has not yet been verified.

See [implementation notes](docs/sbs-playback-preparation.md). When reporting a
problem include app/patch versions, phone and Android version, playback action
and a sanitized patching log. Do not include account tokens or private stream URLs.

See [SBS 6.4.0 QoL research](docs/qol-research-6.4.0.md) for the original investigation
and the [experimental settings guide](docs/mobile-settings-experimental.md) for
the implemented mobile subset and its validation limits.

## License and affiliation

Patch code is licensed under [GPLv3](LICENSE); see [NOTICE](NOTICE).
This project is not affiliated with SBS or the Morphe project. No SBS APKs,
decompiled app sources, account data or signing keys are distributed here.
