# 第三方代码、素材与数据说明

## 着色器

`app/src/main/assets/shaders` 来自本项目对三星天气壁纸资源的研究流程。以下文件保留了原文件中的 “Copyright (C) 2023 The Android Open Source Project” 和 Apache License 2.0 声明：

- `constants.agsl`
- `fog_effect.agsl`
- `glass_rain.agsl`
- `rain.agsl`
- `rain_effect.agsl`
- `snow.agsl`
- `snow_effect.agsl`
- `utils.agsl`

相应许可证全文见 `LICENSES/Apache-2.0.txt`。`sunny_effect.agsl` 未发现同样的许可证头，不能据此推定其许可；再分发权限仍需单独核实。不要把前述部分文件的 Apache 声明扩大为所有三星资源或整个项目的许可。

`app/src/main/assets/adaptations` 是本项目的效果适配与冰晶图集。原有版权头、来源注释均保留。仓库发布不表示获得第三方官方认可或商用授权。

## 视频与头像

- `app/src/main/assets/wallpaper.mp4` 为用户提供的气泡视频，保留完整原文件，不转码、不裁短。
- `app/src/main/res/drawable-nodpi/avatar_lihua.jpg` 为梨花怎黛玉指定的头像，按其要求用于本应用和本次公开分享。
- 未对这些素材授予额外的第三方再分发许可，相关权利归各自权利人。

## 天气数据

天气与日出日落可由 [Open-Meteo](https://open-meteo.com/) 或用户自行配置的[和风天气 QWeather](https://www.qweather.com/)提供，使用前应遵守各服务当时的许可、额度、认证及归因要求。和风账号的专属Host与API Key由用户填写，源码和发布APK不包含可用的共用凭据。应用当前没有接入三星天气或 The Weather Channel 的授权接口，也不含这些服务的 API 密钥。

## Gradle Wrapper

构建启动脚本与 `gradle-wrapper.jar` 由 Gradle 9.6.0 的 Wrapper 任务生成，保留其原有 Apache License 2.0 声明。其他构建依赖不打包在本仓库中，由 Gradle 按配置下载。
