# 燃点聚变 Spark Fusion

## 📚 文档目录

- [Git 规范流程](./../document/git-workflow.md) - 团队 Git 工作流程与规范

## 隐私政策基本使用

### 使用SparkFusionSDK

Step.1 添加依赖
```
	dependencyResolutionManagement {
		repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
		repositories {
			mavenCentral()
			maven { url 'https://jitpack.io' }
		}
	}

	dependencies {
	        implementation 'com.github.Spark-Fusion:SparkFusionSDK:TAG'
	}
```

Step.2 初始化
```
//必须在Application中初始化(包含mmkv)
 SparkFusionSDK.initialize(this)

```
Step.3 在SplashActivity中使用
```
SparkFusionSDK.showPrivacyPolicyDialog(
    context = this,
    appname = "我的应用",
    onClickWeb = {
        // 点击《隐私政策》文本时的回调
        // 可以在这里打开隐私政策网页
    },
    onAgree = {
        // 用户点击"同意"按钮的回调
        // 可以在这里保存用户同意状态，进入应用主界面等
        //初始化广告等SDK
    },
    onRefuse = {
        // 用户点击"拒绝"按钮的回调
        // 可以在这里处理拒绝逻辑，如退出应用
        finish()
    }
)
```

# 权限说明
隐私政策已经更新了权限相关说明，只保留了必要权限。
```
 <uses-permission android:name="android.permission.VIBRATE" />
    <!--联⽹权限-->
    <uses-permission android:name="android.permission.INTERNET" />
    <!--检测当前⽹络状态是2G、3G、4G还是WiFi-->
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <!--获取设备标识IMEI。⽤于标识⽤户-->
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <!--读写存储权限-->
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" tools:node="replace" />
    <!--获取MAC地址，⽤于标识⽤户-->
    <uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <!--安装应⽤权限-->
    <uses-permission android:name="android.permission.REQUEST_INSTALL_PACKAGES" />
    <!-- 华硕获取OAID权限 -->
    <uses-permission android:name="com.asus.msa.SupplementaryDID.ACCESS" />
    <!--穿山甲sdk需要的权限，不接入穿山甲sdk不用添加-->
    <!--必要权限，解决安全风险漏洞，发送和注册广播事件需要调用带有传递权限的接口-->
    <permission android:name="${applicationId}.openadsdk.permission.TT_PANGOLIN" android:protectionLevel="signature" />
    <!--必要权限，解决安全风险漏洞，发送和注册广播事件需要调用带有传递权限的接口-->
    <uses-permission android:name="${applicationId}.openadsdk.permission.TT_PANGOLIN" />
    <!-- 如果视频广告使用textureView播放，请务必添加，否则黑屏 -->
    <uses-permission android:name="android.permission.WAKE_LOCK" />
    <uses-permission android:name="android.permission.EXPAND_STATUS_BAR" />
    <!-- 穿山甲3400版本新增：建议添加“query_all_package”权限，穿山甲将通过此权限在Android R系统上判定广告对应的应用是否在用户的app上安装，避免投放错误的广告，以此提高用户的广告体验。若添加此权限，需要在您的用户隐私文档中声明！ -->
    <uses-permission android:name="android.permission.QUERY_ALL_PACKAGES" />
    <!--ks-->
    <permission android:name="${applicationId}.permission.KW_SDK_BROADCAST" android:protectionLevel="signature" />
    <uses-permission android:name="${applicationId}.permission.KW_SDK_BROADCAST" />
```
# 相关属性冲突
需要在AndroidManifest.xml中声明Application中添加
```
tools:replace="android:allowBackup"
```
#其他补充
...

*燃点聚变 Spark Fusion © 2026*

