# 对原TVBOX的修正部分为：（源码在main文件里，常规使用者不用下载）
5.1 升级对比
组件	升级前	升级后	变化
compileSdk	33 (Android 13)	35 (Android 15)	+2代
targetSdk	28 (Android 9, 2018年)	34 (Android 14)	+6代
minSdk	19 (Android 4.4)	21 (Android 5.0)	+2代
AGP	8.2.2	8.5.2	兼容Gradle 8.7
Gradle	7.5	8.7	+3个大版本
5.2 依赖升级
依赖	旧版本	新版本	说明
OkHttp	3.12.11	4.12.0	主版本升级，API变更
Room	2.3.0	2.6.1	数据库框架
lifecycle-extensions	2.2.0	移除	已死依赖，拆分为 independent artifacts
lifecycle-runtime/viewmodel/livedata	—	2.8.7	新增替代
Gson	2.10.1	2.11.0	JSON解析
appcompat	1.3.0	1.7.0	AppCompat
constraintlayout	2.0.4	2.2.0	约束布局
recyclerview	1.2.1	1.3.2	列表控件
okio	2.8.0	3.9.0	OkHttp底层IO库
5.3 API 适配修复
OkHttp 3.x → 4.x 迁移（最耗时的部分）：

OkGoHelper.java — okhttp3.internal.Version.userAgent() 是 OkHttp 内部API，4.x 已移除 → 改为硬编码 "okhttp/4.12.0"

DnsOverHttps.java — 三处 OkHttp 内部API调用：

PublicSuffixDatabase.get().getEffectiveTldPlusOne() — 内部类被移除 → 改为简单域名判断
Util.addSuppressedIfPossible() — 内部工具方法移除 → 改为标准 Throwable.addSuppressed()
Platform.get().log(Platform.WARN, ...) — 内部平台日志API变更 → 改为 android.util.Log.w()

另使用者下载后需要配置源，需要先获取存储权限，然后设置源，如果完全不会设置，可以加入qq频道学习一下：TVbox
