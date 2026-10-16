# 天气映景 · WeatherGlass

<img src="icon.png" width="96" alt="天气映景图标" />

本地视频与雨、雪、雾、晴、昼夜光线组合的 Android 动态壁纸。

**由梨花怎黛玉与 OpenAI Codex（AI 编程助手）共同开发。** 梨花怎黛玉负责产品构思、效果设计和实机测试反馈；OpenAI Codex提供编程实现与调试协助。

> 完整源码以Release专用附件 **WeatherGlass-0.29-source.zip** 提供；本仓库目录当前展示说明与图片。GitHub自动生成的 Source code 归档仅包含仓库当前文件。

## 下载

- [v0.29 beta 发布页：APK、完整源码包和校验值](https://github.com/Narcissus521/WeatherGlass/releases/tag/v0.29-beta)
- [直接下载 APK](https://github.com/Narcissus521/WeatherGlass/releases/download/v0.29-beta/WeatherGlass-0.29.apk)
- [下载完整源码工程](https://github.com/Narcissus521/WeatherGlass/releases/download/v0.29-beta/WeatherGlass-0.29-source.zip)
- Android 13及以上；重点验证设备为 Galaxy S25 Ultra / Android 17 / One UI 9。其他设备的锁屏应用范围与显示效果以系统为准。

这是开发签名测试版。自己编译会使用自己的调试证书，通常不能直接覆盖发布的APK；源码不含签名私钥。覆盖更新后如果系统没有重新运行壁纸，请在应用内重新应用一次。

## 0.29 新增功能

- **天气来源切换**：在“天气与位置 → 天气来源”选择 Open-Meteo 或和风天气。未配置前沿用 Open-Meteo。
- **和风配置**：在和风控制台设置复制专属 API Host，在项目管理创建 API KEY 凭据，然后仅在手机内填写。凭据使用 Android Keystore / AES-GCM 本机加密保存，不包含共用密钥。当前使用 weather/v1 接口和 API Key 标头认证；未实现JWT配置。官方计划自2027年起限制API Key认证的每日请求量，届时以官方控制台规则为准。
- **本地天气页面**：查看天气、温度、湿度、风速、降水、能见度、日出日落及查询更新时间；支持手动壁纸模式下按需查询，不切换自动/手动模式。缺失数据明确显示，日出日落按手机时区展示。
- **每5分钟自动刷新**：应用或锁屏可见时到期更新，后台接续安排任务；系统省电、休眠、网络与配额可能导致延后，不保证全天严格每300秒唤醒。切换来源取消旧请求并隔离缓存，失败保留并标注上次数据来源。

和风接入与页面的合成测试通过；**尚无真实和风凭据，未完成真实账号端到端联网验证**。使用者需自行配置并确认接口权限。

## 其他已有功能

- 选择自己的视频，内置完整20秒、1440×3200、60fps气泡视频，保持原时长和源帧率。
- 小、中、大三档雨珠、冰窗花与哈气、雾、晴天效果。
- 按手机当前时间及所在地日出日落，连续调整光线；无有效日出日落时暂以手机当地06:00/18:00估算。
- 预览页的天气、强度和时段仅作画面预览，不覆盖实际锁屏设置。
- 不可见时暂停，15秒后释放解码资源，重新可见时从保存位置恢复。
- 莫奈配色、菜单过渡动画、浅色线稿图标、作者头像、共同开发署名与免责声明。

**AOD由系统管理。** 本应用没有三星原生AOD权限，第三方动态壁纸的息屏显示不能跨设备保证。此前三星原生引擎测试不等于普通APK在所有设备上的能力。

## 构建完整源码

解压 `WeatherGlass-0.29-source.zip`，用 Android Studio 打开 `WeatherGlass` 文件夹。工程为独立Java/Android单模块，与CampusFinance无关。

1. 安装 Android SDK Platform 37，让IDE配置本机SDK路径，不要公开 `local.properties`。
2. 使用JDK 25（本项目实测Android Studio JBR 25.0.3）、AGP 9.4.1、Gradle Wrapper 9.6.0，Java源码兼容级别11。
3. Windows执行 `./gradlew.bat :app:assembleDebug :app:lintDebug`；macOS/Linux执行 `./gradlew :app:assembleDebug :app:lintDebug`。首次构建需要下载构建工具和依赖。
4. APK位于 `app/build/outputs/apk/debug/app-debug.apk`。主机检查可在设置JAVA_HOME后执行 `pwsh ./tools/check-host.ps1`。

`app/src/androidTest` 的 `WallpaperChecks` 会改写测试设备设置，**仅允许在可丢弃的模拟器运行**，不要用于日常手机。`sourceOnly=true`运行和风与数据页检查，`cadenceOnly=true`运行刷新检查；测试包含明确标注的假密钥和合成天气，不含真实凭据。

## 验证与限制

0.29离线构建、lint（0错误、原有1条提示）、升级签名通过。隔离Android17模拟器通过63项和风与页面检查、25项定时检查、93项GL/缓存/天气查询/预览隔离回归，包括10组GLES程序和固定测试城市坐标的真实Open-Meteo查询。打包的独立工程已另行验证构建、lint和122项JVM检查。

历史S25小雨样本GL提交约60fps、视频纹理更新约59–60fps，曾有约25ms间隔；不等于面板逐帧呈现或全程零掉帧。息屏释放后曾测得进程PSS约142MiB，亮屏与预览会增加。本版未重测手机帧率、整机电量或全天后台准点性，不将历史结果计作本版重测。

## 隐私与权利

视频和头像不通过应用上传。查询向所选的 `api.open-meteo.com` 或用户专属 `*.qweatherapi.com` 发送保留两位小数的大致坐标。背景随位置更新需要相应定位授权；关闭自动天气停止自动查询，本地天气页仍可由用户主动查询。不要将个人API凭据提交到公开仓库。

天气数据仅用于壁纸展示，不作为出行、安全或灾害预警依据。本项目为独立开发，与三星或天气服务商无官方隶属关系。第三方代码、视频、头像等权利见[第三方说明](THIRD_PARTY_NOTICES.md)。没有选择覆盖整个工程的统一开源许可证；公开可见不表示所有素材都已获任意再分发或商用授权。

## 署名界面

<img src="credits.png" width="320" alt="共同开发署名与作者头像" />
