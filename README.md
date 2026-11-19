# 熊熊宝典

温暖轻快的本地生活记录 App，包含日历与农历、手账与心情、美食菜谱、冰箱与周菜单、收支图表、倒计时、天气和提醒。

## Android v2.2.15 · 2026-11-19

- 天气首页、详情和当天分享卡增加风力：优先显示来源发布的等级；只有明确 m/s 风速时按 GB/T 28591—2012 换算并标明“约”。风力、风速分开显示，缺资料不会显示成 0 级。
- 保留现有安卓桌面小部件，常规安装包使用原签名，可覆盖升级。
- 新增小米负一屏提测源码：重要日子 2×2、今日生活 4×4，独立进程、私有 SQLite 显示快照、曝光刷新、系统圆角和日夜配色。适配目标为小米 14 Pro / 澎湃 OS 3.0.309.0；**尚未通过小米审核，也未完成该机真机测试，不能据此声称已可在负一屏添加。**
- 天气 113 项检查、76 个页面自动化回归、组件/计时规则 81 项断言通过；常规版及小米提测版均通过 Android 编译。

## 获取源码

本仓库的完整 Android、iOS 与共享界面源码存放在 [bear-source-final.tar.xz](bear-source-final.tar.xz)，共 384 个文件。解压后即可查看各目录；已包含此前 iOS 构建修复，**无需再应用旧的 ios-build-fixes.patch**。

```sh
echo '2ad7de3e91026e0f9eecc3730a5c796021326586c93e0b25fd108b244d44a3fe  bear-source-final.tar.xz' | shasum -a 256 -c -
tar -xf bear-source-final.tar.xz
```

| 目录 | 内容 |
| --- | --- |
| android/ | Java 原生容器、SQLite、通知、定位、相册与桌面组件 |
| android/xiaomi/ | 小米提测版构建说明与独立 Manifest 生成器 |
| ios/ | Swift / UIKit / WKWebView 工程与原生测试，最低 iOS 16 |
| web/ | 两端共用的界面、业务逻辑、OCR 与主题素材 |
| tools/ | 业务回归检查与构建辅助脚本 |
| licenses/ | 第三方组件许可与素材说明 |

Android 构建见解压后的 android/build.sh，需要 JDK 17、Android SDK 35 / Build Tools 35.0.0，并提供自己的签名环境变量。小米提测版需显式设置 BEAR_XIAOMI_WIDGETS=1，具体限制见 android/xiaomi/README.md；普通构建不会注册未获审核的小米专用组件。

## iOS 构建状态

iOS 2.2.14 已完成 [云端构建](https://github.com/ZxMms/bear-baodian/actions/runs/44535364244)：11 项桥接检查、7 项 XCTest 和 Release 归档通过，产出用于 SideStore 自签的未签名 IPA。未签名文件不能直接安装到 iPhone，需要用户自己的 Apple 签名。

本次源码包含新的风力界面，但**尚未重新构建和交付包含本次更新的 iOS IPA**。仓库 Actions 保留手动触发、只读权限的构建流程，校验源码后在 macOS 上测试并构建，不会回写仓库。

## 数据与素材

生活记录使用本机 SQLite，图片存于应用私有目录。源码不包含用户数据库、签名密钥或个人账号配置。

本项目为非官方主题作品。第三方代码许可及一二布布素材来源见解压后的 licenses/、ASSET-SOURCES.md、AUDIO-SOURCES.md；公开源码不表示取得第三方角色或音频的商业授权。
