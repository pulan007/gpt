# 最新安装测试包

[下载轻停候选7安装测试 APK](https://raw.githubusercontent.com/pulan007/gpt/main/quietguard/downloads/candidate7/quietguard-candidate7-gkd-release-install-test.apk)（约 3.07 MB） · [安装说明、验证结果与限制](downloads/candidate7/README.md)

默认关闭、真实规则为 0，不代表去广告功能有效。使用新的本地测试签名，可能无法覆盖旧版。应用测试 57/57 通过；选择器测试部分受网络阻碍，Release Lint 有未消除问题。完整范围见下载说明。

以下为原源码归档说明，保留其发布时的历史状态；最新 APK 交付信息以上述下载说明为准。

---

# 轻停 QuietGuard · 候选7诊断源码

本目录的源码压缩包公开保存 2026-10-07 的候选7快照修正源码，发布日期 2026-10-08。

**仅供研发检查点保存。不是安装包，不是可用发行版。**

## 已知状态

- 候选7完整自动关闭验证未通过：自有模拟广告仍显示，最终查询阶段捕获 `QUERY_FINAL` 异常，原因尚未确定。
- 真实应用已验证覆盖数量为 **0**。未验证真机兼容性、奖励到账、续航或温度改善。
- 候选7标识为 `0.3.0-owned-fixture-TEST-ONLY-GUARD.7` / versionCode 7，测试包名 `dev.quietguard.gkd.fixturetest.debug`。
- 仅 `ownedFixtureDebug` 通过显式构建属性包含自有模拟页面条目；gkd/play 目录仍为空。不能将此候选版本当作生产第3版源码。
- 所有运行结论均来自原交付记录。本次仅检查、整理和发布源码，没有重新构建、运行测试或修复功能。

## 来源与许可

基于 GKD 1.12.1，原作者及贡献者：GKD / gkd-kit / lisonge。
上游固定提交：https://github.com/gkd-kit/gkd/tree/5a00f844989471458e4cf4601acb3f4710438f9a

保留 GPL-3.0 许可证全文（LICENSE）、原始文件内版权信息和上游 README（UPSTREAM_README.md）。
本项目为独立修改版，不是 GKD 官方发布。修改范围与历史设计限制见 PRIVATE_FORK.md。

## 源码内容

保留 app、hidden_api、selector 三个完整模块（含模块内测试、资源、数据库模式）、Gradle 构建声明、版本目录、脚本及配置。应用与构建输入保持原检查点字节不变。

公开整理仅改写文档和包结构；未修改应用功能。剔除私有运行证据、历史日志/报告、设备资料、研究目标记录、额外验证工具目录和上游 GitHub 工作流/议题模板。应用图标是构建资源，予以保留；没有运行截图。

不含 APK、签名密钥、SDK、缓存、第三方安装包或独立模拟应用源码。模拟页面依赖不在原源码归档内，因此此目录本身不能复现完整设备场景。

## 构建提示（本次未验证）

原构建配置记录 JDK 21、Gradle 9.5.1、AGP 9.2.1、Kotlin 2.3.21、Android SDK / Build Tools 37。

原归档没有 gradle-wrapper.jar；因此不能直接声称 ./gradlew 可用。准备匹配版本的独立 Gradle 和 Android SDK 后，原测试变体命令为：

    gradle :app:assembleOwnedFixtureDebug -PquietguardOwnedFixtureTest=true

模块选择器测试命令：

    gradle :selector:jvmTest

依赖按 Gradle 声明从各公共仓库解析；本归档不是离线依赖包。上述命令本次没有运行，不承诺在新环境成功。调试签名由构建环境生成，不应作为正式发布签名。

## 完整性

SOURCE_SHA256SUMS.txt 列出公开归档内其余文件的 SHA-256。包外 SHA256SUMS.txt 校验压缩包本身。

下载并解压 [quietguard-candidate7-source.tar.gz](quietguard-candidate7-source.tar.gz) 后阅读其中的说明；[SHA256SUMS.txt](SHA256SUMS.txt) 提供压缩包校验值。
