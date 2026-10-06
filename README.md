# OneUI_CSC_Features_Next

三星 One UI 国行功能移植模块，提供 `All` 全量安装包，以及智能收藏、地震预警、字幕助手三个独立安装包。

> 本项目为非官方移植与整理项目，与 Samsung、原项目作者及 Hybrid Mount 项目不存在官方隶属关系。

## 下载

请前往 [Releases](https://github.com/Ann114514/OneUI_CSC_Features_Next/releases/latest) 下载模块。

## 相关项目

- [Mzdyl/OneUI_CSC_Features](https://github.com/Mzdyl/OneUI_CSC_Features)：原始 One UI CSC 功能扩展项目及本项目的重要参考来源。
- [Hybrid-Mount/meta-hybrid_mount](https://github.com/Hybrid-Mount/meta-hybrid_mount)：KernelSU/APatch 混合挂载元模块；临时 Root 用户请自行准备，并确认本模块使用 Magic Mount。

更新日期：2026-10-07

## 发布文件

1. 智能收藏_2.1.00.21_DataKeep_v4.zip
2. 地震预警_1.0.00.17_DataKeep_v4.zip
3. 字幕助手_1.5.00.7_DataKeep_v3.zip
4. OneUI_CSC_Features_Next-all.zip

## All 全量模块说明

- All 模块固定包含智能收藏、地震预警和字幕助手，安装时一次性部署全部三个组件，不再逐项询问或使用音量键选择。
- 已经安装旧版三个单独模块的用户，可以直接安装 All 模块。安装器会自动检测旧单独模块，并将其标记为停用和移除；软重启后由 All 模块统一接管。
- 这种方式属于自动迁移：KernelSU 技术上仍按模块 id 管理模块，并不是一个 id 同时继承三个旧 id。
- 临时 Root 用户先自行准备 Hybrid Mount，并自行确认模块最终处于 Magic Mount 状态。
- 安装器只做提示，不检测、不安装、不修改 Hybrid Mount。
- 安装完成后务必执行一次软重启。

## 功能状态

以下状态依据现有模块记录与用户反馈；本次离线打包未重新实机验证。

### 智能收藏 2.1.00.21

- 支持：智能收藏、智能拖放、朗读文字
- 不支持：摘要
- 智能拖放入口额外依赖系统属性 ro.otch.support.entrance=true。
- 该属性此前由 CSC/系统属性模块提供；智能收藏模块本身不会写入或修改它。
- OneTouch 还需要浮动特征 SEC_FLOATING_FEATURE_COMMON_SUPPORT_BIXBY_TOUCH=TRUE。
- 缺少上述开关时，即使 OneTouch APK、权限和 sysconfig 已正确部署，智能拖放入口仍可能不出现。

### 地震预警 1.0.00.17

- 已包含：设置入口、功能开关、预警服务、定位/通知权限与相关开关自动处理
- 经模拟测试，预警流程可以正常触发。
- 免责声明：模拟触发不等于真实地震事件验证。本模块不保证真实事件一定能够触发，也不保证预警的及时性、准确性或完整性。实际工作状态会受到地区、网络、定位、三星服务、系统版本、后台限制及上游数据源等因素影响。
- 本模块和手机预警功能不能替代政府部门、应急广播及其他官方灾害预警渠道，请勿将其作为涉及人身安全的唯一判断依据。

### 字幕助手 1.5.00.7

- 支持：实时字幕、翻译
- 不支持：摘要

## 主要修复与改动

- 按 all + 单独包的发布方式提供模块：All 固定安装全部功能，同时保留三个独立包。
- All 安装器会自动迁移同系列旧单独模块，避免软重启后重复挂载相同 APK 和权限文件。
- 三个独立模块使用中文名称，完整包使用 OneUI_CSC_Features_Next-all 名称，并全部标明版本。
- 智能收藏状态更新为“朗读文字可用”。
- 修正智能收藏安装脚本中错误的旧 APK 版本提示。
- 补全模块脚本权限设置，并统一增加“务必软重启”提示。
- 保留 DataKeep 逻辑：首次正常生效后建立 /data/app 更新副本，以尽量保留完整重启后的引导、权限与应用数据。

## 更新与切换说明

- 继续使用三个单独模块：可以直接分别安装新版覆盖旧版。三个模块的 id 保持不变，KernelSU 会识别为更新；三个都安装完成后统一软重启一次即可，不必先卸载旧版。
- 从单独模块改用 All：直接安装 All 即可，不需要用户逐个停用或卸载旧单独模块；安装器会自动完成迁移标记。安装完成后软重启一次，旧单独模块会停止加载并由 All 接管。
- 安装 All 后不要再次安装或启用同功能的单独模块，否则可能造成重复挂载。
- 从 All 改回单独模块：先移除或停用 All，再安装需要的单独模块，最后软重启。

## 重要提醒

- 不要在应用信息中点击“卸载更新”，否则 DataKeep 创建的 /data/app 副本会被删除。
- 卸载模块后，/data/app 副本可能仍保留，这是现有 DataKeep 设计行为。
- 离线脚本检查与模拟安装不等于手机实机验证；首次安装建议保留原模块备份。

## 致谢

- 感谢 [Mzdyl](https://github.com/Mzdyl) 及 [OneUI_CSC_Features](https://github.com/Mzdyl/OneUI_CSC_Features) 项目对三星 One UI 国行功能扩展、模块结构和相关资源所做的工作。
- 感谢 [Hybrid Mount](https://github.com/Hybrid-Mount/meta-hybrid_mount) 项目为 KernelSU/APatch 环境提供 OverlayFS、Magic Mount、VFS 等挂载能力。
- 感谢参与功能验证、日志分析和实际测试的用户与贡献者。

## 版权与免责声明

模块中涉及的 Samsung 应用、商标及相关资源，其权利归 Samsung Electronics 及相应权利人所有。本项目仅用于兼容性研究、功能测试与个人学习，不提供任何功能可用性或适用性保证。使用者应自行承担安装、更新、设备兼容性及数据风险。
