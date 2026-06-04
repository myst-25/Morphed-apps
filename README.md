# Morphed-apps Builder

[![Telegram Channel](https://img.shields.io/badge/Telegram_Channel-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/morphedapps)
[![Myst25 Chat](https://img.shields.io/badge/Myst25_Chat-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/+OQA0X-ECCHI4ZmU1)

A fully automated, heavily customized build pipeline for generating patched, optimized **Morphed** Android apps (YouTube, YouTube Music, X/Twitter, Instagram) directly from experimental APKs.

This repository is a completely overhauled fork of the original `revanced-magisk-module`, specifically engineered to pull custom experimental app versions and dynamically post them to Telegram.

## 🚀 How it Works

The entire build process is automated via GitHub Actions and is strictly tethered to the [**myst-25/ampy**](https://github.com/myst-25/ampy) repository.

1. **Base Uploads:** Unmodified, experimental APKs are uploaded to the `ampy` repository releases.
2. **Dynamic Versioning:** The `apps.json` file in `ampy` tracks the exact version number of the target APKs.
3. **Fuzzy Fetching:** When triggered, the GitHub Actions in this repo download the `apps.json` file, extract the version, and use fuzzy matching to precisely identify and download the massive base APKs from `ampy`.
4. **Patching & Stripping:** The pipeline patches the apps using specific patchers (like `MorpheApp/morphe-patches` and `crimera/piko`) and dynamically strips native libraries to export both `arm64-v8a` and `arm-v7a` optimized variants.
5. **Telegram Integration:** It natively pushes the final, dual-architecture APKs directly to the official Telegram channel with formatted changelogs and download links.

## 🛠 Configurations

The build settings are strictly modularized into isolated TOML files:
- [`youtube.toml`](./youtube.toml): Manages YouTube and YouTube Music patches (uses Morphe).
- [`social.toml`](./social.toml): Manages X/Twitter and Instagram patches (uses Piko/ReVanced).

Instead of hardcoded versions, these configs utilize `json-key` and `dl-keyword` properties to seamlessly locate resources.

## ⚙️ Triggering a Build

Builds **do not run automatically** on push. To trigger a build:
1. Navigate to the **Actions** tab of this repository.
2. Select either **Build YouTube and Music** or **Build Social (Twitter/Instagram)**.
3. Click **Run workflow**. 

Wait for the build to finish, and the fully formatted post and files will appear directly in your Telegram channel.

## 🖇 Useful Links
* **Base APK Repository:** [myst-25/ampy](https://github.com/myst-25/ampy)
* **MicroG for Non-Root:** [MorpheApp/MicroG-RE](https://github.com/MorpheApp/MicroG-RE/releases/tag/6.1.4)
* **Detach Play Store:** [zygisk-detach](https://github.com/j-hc/zygisk-detach)
