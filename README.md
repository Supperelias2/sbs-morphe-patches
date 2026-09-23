# Supperelias2 SBS Patches

Unofficial [Morphe](https://morphe.software) patches for SBS On Demand.

[Add this source to Morphe](https://morphe.software/add-source?github=Supperelias2/sbs-morphe-patches)
 · [Releases](https://github.com/Supperelias2/sbs-morphe-patches/releases)
 · [Report a problem](https://github.com/Supperelias2/sbs-morphe-patches/issues)

## What the patch does

**Prefer direct VOD stream (experimental)** selects an Akamai HLS alternative
already present in the app's playback response instead of Google DAI. It only
changes on-demand playback when a non-empty alternative URL is available.
Live playback and cases without an alternative retain the original selection.

The maintainer reports successful playback with the patch on a phone using
SBS **6.3.0 (16435)**. This is an initial user test, not comprehensive device
coverage. Ad-free playback is not guaranteed for every title or session.
Location requirements are unchanged.

## Install with Morphe Manager

1. Open the source link above, or add `https://github.com/Supperelias2/sbs-morphe-patches`
   under **Sources → + → Remote**.
2. Enable **Experimental app versions** for this source. For dev releases,
   enable **Pre-release patches** as well.
3. Enable **Expert mode**, select an original SBS 6.3.0 APKM, and select
   **Prefer direct VOD stream (experimental)**. Its compatibility check is automatic.
4. Patch and install using Morphe Manager. A signature conflict with the official
   app may require uninstalling that app, which removes its local data/downloads.
5. Keep Morphe's signing key for future updates. Test start, resume, seeking,
   midstream playback and live playback.

Alternatively import the release's `.mpp` file using **Sources → + → Local**.
Local imports need to be replaced manually for updates. Always patch an original
app file, not an already patched APK.

## Patches

<!-- PATCHES_START EXPANDED -->
The release workflow generates the patch list here.
<!-- PATCHES_END -->

## Development and testing

Build with `./gradlew buildAndroid`. The bundle is written to
`patches/build/libs/patches-*.mpp`. Local builds need GitHub Packages read access;
never commit credentials. Development happens on `dev`; the existing semantic
release workflow builds releases and updates source metadata.

Validation completed: Gradle build, application to the original APKM using
Morphe Desktop 1.16.0, APK rebuild, and inspection of the modified DEX method.
The maintainer subsequently reported a successful phone test.

See [implementation notes](docs/sbs-playback-preparation.md). When reporting a
problem include app/patch versions, phone and Android version, playback action
and a sanitized patching log. Do not include account tokens or private stream URLs.

## License and affiliation

Patch code is licensed under [GPLv3](LICENSE); see [NOTICE](NOTICE).
This project is not affiliated with SBS or the Morphe project. No SBS APKs,
decompiled app sources, account data or signing keys are distributed here.
