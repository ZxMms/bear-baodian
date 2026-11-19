# 熊熊宝典

温暖轻快的本地生活记录 App，包含农历日历、手账与心情、美食菜谱、冰箱与周菜单、收支图表、倒计时、天气和提醒。

## Android 与 iOS 完整源码

两端源码保存在 [bear-source-final.tar.xz](bear-source-final.tar.xz)，共 370 个文件，包含原生代码、共享页面、素材、测试及构建说明。另有 [ios-build-fixes.patch](ios-build-fixes.patch)，修复 Xcode 初始化器编译问题与 Apple Silicon 模拟器架构设置。请下载这两个文件，放在同一目录后执行：

```bash
mkdir bear-source
tar -xJf bear-source-final.tar.xz -C bear-source
cd bear-source
git apply ../ios-build-fixes.patch
```

| 解压后目录 | 内容 |
| --- | --- |
| android/ | Java 原生 Android 工程、SQLite、相册、通知及定位 |
| ios/ | Swift / UIKit / WKWebView 工程，最低 iOS 16 |
| web/ | 共享页面、业务逻辑、OCR 和主题素材 |
| tools/ | 回归检查与开发依赖清单 |
| licenses/ | 第三方许可及素材来源 |

源码不包含个人数据库、账号密码或签名密钥。Android 构建需要 JDK 17、Android SDK 35 / Build Tools 35.0.0，并通过环境变量提供自己的签名。

## iOS 构建与 SideStore

在 Actions → iOS build and tests → Run workflow 手动运行。流程仅有仓库读取权限，不会自动修改仓库；先校验源码 SHA-256、解压并应用修复补丁，再安装锁定的测试依赖，执行桥接检查、XCTest 与 iPhone 架构归档。

只有构建成功才会生成 BearBaodian-unsigned.ipa。下载对应运行的 Artifacts，解压后可把 IPA 导入 SideStore，使用自己的 Apple 账号签名安装。未签名 IPA 不能直接点击安装；本仓库不提供 Apple 账号、证书或 TestFlight 邀请。

2026-11-19 已通过 [第 4 次云端构建](https://github.com/ZxMms/bear-baodian/actions/runs/44535364244)：Xcode 16.4 编译、11 项 JS 桥检查、7 项 XCTest 均通过，iPhone Release 归档成功。IPA 为 arm64 / iPhoneOS，版本 2.2.14 (1)，最低 iOS 16，大小 15,951,067 字节。

构建产物默认保留 14 天；过期后可手动重新构建。尚未完成 iPhone 真机验收，定位、微信分享、后台提醒及 OCR 仍需在设备上测试。SideStore 配置及续签说明：https://docs.sidestore.io/

压缩包内的迁移说明保留了初次制作时的验证记录；最新构建状态以本页和 Actions 结果为准。

完整迁移说明见压缩包内 ios/README-iPhone.md；Android 更新与验收记录也保留在包内。

本项目为非官方主题作品，第三方素材与音频来源见源码中的 ASSET-SOURCES.md、AUDIO-SOURCES.md 和 licenses/。
