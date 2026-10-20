# 天气映景 · WeatherGlass

<img src="icon.png" width="96" alt="天气映景图标" />

本地视频与雨、雪、雾、晴、昼夜光线组合的 Android 动态壁纸。

**由梨花怎黛玉与 OpenAI Codex（AI 编程助手）共同开发。**

## 下载

- [v0.31 beta 发布页](https://github.com/Narcissus521/WeatherGlass/releases/tag/v0.31-beta)
- [直接下载 APK](https://github.com/Narcissus521/WeatherGlass/releases/download/v0.31-beta/WeatherGlass-0.31.apk)
- [下载完整源码工程](https://github.com/Narcissus521/WeatherGlass/releases/download/v0.31-beta/WeatherGlass-0.31-source.zip)
- [SHA-256 校验文件](https://github.com/Narcissus521/WeatherGlass/releases/download/v0.31-beta/SHA256SUMS.txt)

> 完整源码以专用附件 **WeatherGlass-0.31-source.zip** 提供；本仓库目录当前展示说明与图片。GitHub自动生成的 Source code 归档仅包含仓库当前文件。

Android 13及以上，重点验证设备为 Galaxy S25 Ultra。开发签名测试版，可保留数据覆盖此前同签名版本；自行编译通常使用不同证书。

## 0.31 实际壁纸雾效修复

- 修复预览正常、实际壁纸出现半透明多边形与直线接缝的问题：替换实际雾效OpenGL路径中的不稳定噪声哈希。
- 预览AGSL、雾的层次/速度/浓度公式和全部素材保持原样；实际雾块随机分布会变化。
- 雨、雪、晴及无天气的GLSL与0.30逐字节相同，保留2K/60fps视频、亮屏续播、天气源、5分钟刷新及原设置。
- 已在S25 Ultra/Adreno830完成三档强度、三个时间点的18组离屏对比及噪声边界检查；锁屏观感由使用者验收，不将离屏结果当作满屏帧率或功耗测量。

## 0.30 亮屏续播修复

- 正常息屏时保留暂停的视频解码器，亮屏直接续播，减少重新准备视频和定位暂停帧造成的等待。
- 相同尺寸和格式的重复显示区域回调复用渲染资源；真正的尺寸变化和Surface销毁重建仍正常处理。
- 息屏停止播放和绘制；内存回收或销毁时释放资源，隐藏的系统壁纸预览仍在15秒后回收。
- 原2K/60fps完整视频、天气特效、昼夜变化、5分钟天气刷新和已有设置保持。

保留解码缓冲会增加息屏驻留内存。S25 Ultra小雾/内置视频样本PSS约288–292MiB，随手机、素材、天气效果和系统策略变化；不是整机功耗测量。系统回收后仍可能需要冷恢复，不承诺所有条件下瞬时亮屏。

## 已有功能

- 自选视频，内置完整20秒、1440×3200、60fps气泡视频。
- 小、中、大三档雨珠、冰窗花与哈气、雾、晴天效果。
- 根据手机当前时间及所在地日出日落连续调整光线；没有有效日出日落时以手机当地06:00/18:00估算。
- Open-Meteo与和风天气手动切换，本地天气页面可查看温度、湿度、风速、降水、能见度及日出日落。
- 自动天气目标每5分钟更新，后台受省电、休眠、网络及系统调度影响可能延后。
- 天气预览独立于实际锁屏设置，莫奈配色、菜单动画、作者头像及免责声明。

和风需自行配置专属API Host与API Key，凭据由Android Keystore/AES-GCM本机加密保存。本包没有共用密钥；已完成合成测试，尚未完成真实和风账号端到端联网验证。

**AOD由系统管理。** 第三方动态壁纸的息屏显示和锁屏应用范围不能跨设备保证，无需root。

## 构建与验证

解压专用源码包，用Android Studio打开WeatherGlass文件夹。工程为独立Java/Android单模块。使用SDK37、JDK25、AGP9.4.1及Gradle9.6.0，Java源码兼容级别11。

Windows执行 `./gradlew.bat :app:assembleDebug :app:lintDebug`；其他平台执行 `./gradlew :app:assembleDebug :app:lintDebug`。APK位于 `app/build/outputs/apk/debug/app-debug.apk`。

0.31通过构建、lint（0错误、1条原有提示）及升级签名检查；122项主机检查、实际手机GPU的18组雾效离屏输出及9组CPU参考比较通过。噪声边界专项测试140400对相邻点，修复后没有超过2个8bit码值的跳变。独立源码工程另做构建、lint与主机检查。0.30的27项恢复和107项Android回归为历史记录，本次未重跑该完整套件，也未重测满屏帧率或功耗。

测试程序会改写测试设备状态，仅应在可丢弃的模拟器运行，不能用于日常手机。画面验收由使用者完成，不保证全程零掉帧或固定耗电。

## 隐私与权利

视频和头像不通过应用上传。天气查询向所选Open-Meteo或用户专属和风服务发送保留两位小数的大致坐标。源码包不含个人凭据、开发签名私钥、手机日志或本机路径。

天气数据仅用于壁纸展示，不作为安全或灾害预警依据。本项目与三星或天气服务商无官方隶属关系。第三方代码及素材说明见[THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)；公开可见不表示所有素材均可任意再分发或商用，项目没有统一覆盖全部内容的开源许可证。

## 署名界面

<img src="credits.png" width="320" alt="共同开发署名与作者头像" />

