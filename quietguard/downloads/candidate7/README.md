# 轻停候选7 · 安装测试 APK

**仅用于安装和界面检查，不是有效去广告版本。默认关闭，真实应用规则为 0。**

[直接下载 APK](https://raw.githubusercontent.com/pulan007/gpt/main/quietguard/downloads/candidate7/quietguard-candidate7-gkd-release-install-test.apk) · [校验值](SHA256SUMS.txt) · [详细验证结果](VERIFICATION.json)

2026-10-08，从候选7源码提交 `b18f28eac70861e755b30a82f598c8dd2bab28e2` 构建。采用正常 `gkdRelease` 变体，未设置 `quietguardOwnedFixtureTest`，不编入自有模拟规则；诊断记录实现为空操作。此处的 release 仅表示构建类型，不代表正式产品质量。

## 安装信息

| 项目 | 实际 APK 结果 |
|---|---|
| 大小 | 3,067,881 字节（约 3.07 MB / 2.93 MiB） |
| 包名 | `dev.quietguard.gkd.fixturetest` |
| versionName / versionCode | `0.3.0-owned-fixture-TEST-ONLY.1` / `1` |
| 应用名称 | `轻停 TEST ONLY·自有模拟测试`（沿用源码名称，未启用模拟规则） |
| Android | minSdk 26（Android 8.0）；targetSdk 37 |
| ABI | `arm64-v8a`、`x86_64`、`x86` |
| 构建 | `gkdRelease`；不可调试；关闭备份 |
| 签名 | 新的本地测试 RSA-3072 签名，APK v2 校验通过 |

源码中的候选7专用 `ownedFixtureDebug` 才使用 versionCode 7 和 `.debug` 包名；本包采用该源码中的正常 gkd 变体，保留其原始版本标识，不能据此称作正式第7版。

APK SHA-256：`7996415407f05eb857c2c52d346056ab9fe64e50cfa41cb81cbf450bc6208bfd`

签名证书 SHA-256：`997c5d00401185154af6a66fc6d9924b6df71b2f08025607927a0479509e7056`。

旧签名不可用。本包使用新测试密钥，可能无法覆盖同包名旧版本；没有搜索或上传旧密钥，也没有上传新私钥。手机若拒绝覆盖，请先确认旧版数据保留需求；卸载会删除其本地数据。本次未在真实手机安装，Android 版本兼容性仅以 Manifest 声明为准。

## 验证范围

| 检查 | 结果 |
|---|---|
| 原源码包及包内 SHA-256 | 全部通过；应用、构建声明和测试源码未修改 |
| `:app:assembleGkdRelease` | 通过，已生成签名 APK |
| `:app:testGkdDebugUnitTest` | 57 / 57 通过，含生产目录无规则检查 |
| `:selector:jvmTest` | 18 项已运行：9 通过、9 失败；失败项无法下载外部快照（UnknownHostException，代理连接该站也返回 403） |
| `:app:lintGkdRelease` | 失败：1 错误、32 警告；未屏蔽、未加入 baseline |
| APK 签名、ZIP CRC、16 KB zipalign | 通过 |
| 实际 APK 包名、版本、ABI、权限、不可调试及备份关闭 | 已核验 |
| 真机安装、启动、HyperOS、仪器测试、自动关闭、奖励、续航和温度 | 未运行 / 未验证 |

完整 Gradle 组合命令退出码为 1，原因是 Lint；不能把该命令整体称为全部通过。应用单元测试使用实际存在的 `gkdDebug` 任务，此配置没有 `testGkdReleaseUnitTest` 任务。单元测试不等于 APK 运行测试。

Lint 的唯一错误是源 Manifest 的 `tools:node="remove"` 删除标记引用 `androidx.compose.ui.tooling.PreviewActivity`，而 Release 不含该调试类。已在合并清单和最终 APK 中确认该组件不存在。警告包括 QueryPermissionsNeeded 1、GradleDependency 1、NewerVersionAvailable 23、UnusedResources 6、UseKtx 1；没有新增包查询权限或升级依赖来消除警告。

实际请求权限仅为 `POST_NOTIFICATIONS`、`FOREGROUND_SERVICE`、`FOREGROUND_SERVICE_SPECIAL_USE` 和自身的 `dev.quietguard.gkd.fixturetest.DYNAMIC_RECEIVER_NOT_EXPORTED_PERMISSION`（签名级）。无障碍服务另受系统 `BIND_ACCESSIBILITY_SERVICE` 保护，需要用户手动授权；默认关闭。APK 没有 INTERNET、悬浮窗、存储写入、安装包、全应用查询、Shizuku 或安全设置写入权限。

## 已知功能限制

- 候选7此前完整自动关闭验证失败，最终查询阶段曾出现 `QUERY_FINAL` 异常；本次未修复或重新验证。
- 真实应用可执行规则和已验证覆盖均为 0，不能声称真实广告处理有效。
- 主开关默认关闭；没有放宽防误点条件、加入真实规则或新增权限。
- 仅完成构建和静态/单元验证；不能保证具体手机上的安装、启动或后台运行表现。

## 对应源码、许可与构建差异

[对应候选7应用源码](../../quietguard-candidate7-source.tar.gz)（SHA-256 `a20c141d6eddd3f82544f26a76275b5ef671cac98a1e461232dd352773906bc3`）及 [GPL-3.0 全文](../../LICENSE) 保留。基于 GKD 1.12.1，保留 GKD / gkd-kit / lisonge 及贡献者署名。此为独立修改版，非官方 GKD 发布。

应用归档无任何修改，也未补写 wrapper；使用官方独立 Gradle 9.5.1。工具链为 Eclipse Temurin JDK 21.0.8+9、AGP 9.2.1、Kotlin 2.3.21、SDK Platform 37.0 revision 2、Build Tools 37.0.0。Gradle 下载 SHA-256 与源码固定值一致，JDK 下载与官方校验值一致，SDK 从 Google 官方仓库安装。

环境无法访问 JitPack，因此从官方固定标签本地重建 Toaster 15.0、XXPermissions 28.2、DeviceCompat 2.6、ActivityResultLauncher 1.1.2 和其传递依赖 Callbacks 1.0.0。未升级版本、未修改它们的实现代码；构建适配仅迁移旧 Gradle DSL、Manifest namespace 及标准 Maven 发布。这些产物不声称与 JitPack 二进制逐字节相同。

[依赖源码及构建适配](build-dependencies-source.tar.gz) 包含完整提交来源 `PROVENANCE.json`、源代码、原有许可和构建说明。`Callbacks` 原标签没有单独 LICENSE 文件，此事实已原样记录，没有杜撰许可文本。

复现时先解压依赖源码并运行 `gradle publishToMavenLocal`，再解压原应用源码，配置相同 Maven 本地目录、官方工具链和自己的本地测试签名。在应用目录执行：

```sh
gradle :app:assembleGkdRelease :app:testGkdDebugUnitTest :app:lintGkdRelease --continue --no-daemon --max-workers=4
gradle :selector:jvmTest --no-daemon --max-workers=4
```

签名通过外部私有 Gradle 属性 `GKD_STORE_FILE`、`GKD_STORE_PASSWORD`、`GKD_KEY_ALIAS`、`GKD_KEY_PASSWORD` 配置；不应提交到源码目录。网络代理和本地工具路径只存在于构建环境。不同签名密钥或工具版本会改变 APK 哈希。

发布清单仅包含本 APK、此说明、校验清单、脱敏验证摘要、依赖源码；不含用户资料、私钥、环境配置、完整运行日志或内部诊断证据。原仓库其余内容保留。
