# android-archetypes
使用Maven模板，快速生成Android项目。

## 准备工作

### JDK
请安装最新版的JDK 7或更高版本,本人使用版本为7.u55。 [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).

### Android SDK
已安装Android SDK的请跳过。

请在[http://developer.android.com/sdk/index.html](http://developer.android.com/sdk/index.html) 下载最新版本的Android SDK，并按以下内容进行操作
在Android SDK至少安装以下安装包 :

* Tools (all packages)
* Android 4.4 (API 19)
* Android 2.3.3 (API 10)
* Extras (all packages according to your platform)

Or from the command line (headless environment) :

	android update sdk --no-ui --all --filter \
		tools,\
		platform-tools,\
		build-tools-19.0.1

	android update sdk --no-ui --all --filter \
		extra-android-m2repository,\
		extra-android-support,\
		extra-google-admob_ads_sdk,\
		extra-google-analytics_sdk_v2,\
		extra-google-google_play_services_froyo,\
		extra-google-google_play_services,\
		extra-google-m2repository,\
		extra-google-play_apk_expansion,\
		extra-google-play_billing,\
		extra-google-play_licensing,\
		extra-google-webdriver

	android update sdk --no-ui --all --filter \
		android-19,\
		sysimg-19,\
		addon-google_apis-google-19

	android update sdk --no-ui --all --filter \
		android-10,\
		sysimg-10,\
		addon-google_apis-google-10

where options :

* `--no-ui` : Updates from command-line (does not display the GUI)
* `--all` : Includes all packages (such as obsolete and non-dependent ones)
* `--filter`: A filter that limits the update to the specified types of packages

### Maven
请安装至少3.1.1版本以上的Maven。 [Maven](http://maven.apache.org/download.cgi)。
设置好`M2_HOME`。

### Maven Android SDK Deployer
如果要使用本机上的Android SDK
请查看，并按其说明安装，[Maven Android SDK Deployer](https://github.com/mosabua/maven-android-sdk-deployer) :

	git clone https://github.com/mosabua/maven-android-sdk-deployer.git
	cd maven-android-sdk-deployer/
	mvn install -P 2.3.3
	mvn install -P 4.4
	cd extras/compatibility-v4/
	mvn clean install

## 安装
使用Maven安装archetypes至你的Maven本地库:

	git clone https://github.com/destinyd/android-archetypes.git
	cd android-archetypes/
	mvn clean install

## android-library-project archetype
本archetype包含了最常见的apklib项目模板，形式如下
```
parent
+library
+samples
```
生成library，samples自动依赖library。

###快速生成library项目命令行指令:

	mvn archetype:generate \
		-DarchetypeArtifactId=android-library-project \
		-DarchetypeGroupId=com.github.destinyd.android.archetypes \
		-DarchetypeVersion=0.0.3-SNAPSHOT \
		-DarchetypeCatalog=local \
		-DarchetypeRepository=local \
		-DgroupId=your.company \
		-DartifactId=my-android-library-project \
		-Dpackage=your.company.mylib \
		-Dversion=0.1 \
		-DinteractiveMode=false

你必须定义以下属性 :

* `-DgroupId` : 你Maven项目的groupId，用于其他项目引用
* `-DartifactId` : 你Maven项目的名称，用于其他项目引用
* `-Dversion` : 你Maven项目的版本，用于其他项目引用

你还需要定义以下可选属性 :

* `-Dpackage` : 定义library的package (默认为 : 之前设置的`groupId`)
* `-DminSdkVersion` : the minimum API Level required for the library (default : 10, Android 2.3.3)
* `-DtargetSdkVersion` : the targeted Android platform version to use (default : 19, Android 4.4)

Once generated, your application is ready to be built and tested. Start an android emulator or plug an Android dev phone ([USB debugging must be enabled in Developer options settings](http://developer.android.com/tools/device.html#setting-up)) and execute the following commands :

	cd my-android-library-project
	mvn clean install

To deploy and launch the application with Maven :

	cd my-android-library-project
	mvn clean install android:deploy android:run

###快速生成library项目，Intellij Idea操作说明:
File -> New Project -> Maven -> Add Archetype... ->
GroupId: com.github.destinyd.android.archetypes
ArtifactId: android-library-project
Version: 0.0.1
-> 选择com.github.destinyd.android.archetypes:android-library-project -> Next
-> 输入自己项目的GroupId(例如com.github.destinyd.test), ArtifactId(例如test), Version(例如0.0.1) -> Next -> Next
-> 输入自己项目的名称（例如ArtifactId为test,最好设置为test-parent,否则library会显示为`test(1)`不好看）以及路径
-> Finish

-> 这时右上角会显示
	Maven projects need to be imported
	Import Changes Enable Auto-Import
可以直接选择Enable Auto-Import自动加载，也可以只是点击Import Changes
-> 完成后会出现基本的项目框架
-> 展开项目反击pom.xml -> Maven -> Reimport (这几步操作不知道是不是Intellij bug，因为项目创建完后我重新open pom.xml，可以省去这几步操作)
-> 至此项目生成所有步骤结束






# android-archetypes
Provides Maven archetypes for Android to quickly bootstrap a Maven project and start developing an Android application.

All artifacts are based on the android-maven-plugin [http://code.google.com/p/maven-android-plugin/](http://code.google.com/p/maven-android-plugin/). It currently uses the **3.8.1** version.

## Before starting

### JDK
Use at least Java JDK 6 from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).

### Android SDK
Download the latest Android SDK from
[http://developer.android.com/sdk/index.html](http://developer.android.com/sdk/index.html) and follow the instructions there.

From Android SDK, install at least the following packages :

* Tools (all packages)
* Android 4.4 (API 19)
* Android 2.3.3 (API 10)
* Extras (all packages according to your platform)

Or from the command line (headless environment) :

	android update sdk --no-ui --all --filter \
		tools,\
		platform-tools,\
		build-tools-19.0.1

	android update sdk --no-ui --all --filter \
		extra-android-m2repository,\
		extra-android-support,\
		extra-google-admob_ads_sdk,\
		extra-google-analytics_sdk_v2,\
		extra-google-google_play_services_froyo,\
		extra-google-google_play_services,\
		extra-google-m2repository,\
		extra-google-play_apk_expansion,\
		extra-google-play_billing,\
		extra-google-play_licensing,\
		extra-google-webdriver

	android update sdk --no-ui --all --filter \
		android-19,\
		sysimg-19,\
		addon-google_apis-google-19

	android update sdk --no-ui --all --filter \
		android-10,\
		sysimg-10,\
		addon-google_apis-google-10

where options :

* `--no-ui` : Updates from command-line (does not display the GUI)
* `--all` : Includes all packages (such as obsolete and non-dependent ones)
* `--filter`: A filter that limits the update to the specified types of packages

### Maven
Install [Maven](http://maven.apache.org/download.cgi) (**3.1.1 or higher is required**) and set the `M2_HOME` environment variable to the location that should contain Maven.

### Maven Android SDK Deployer
Install [Maven Android SDK Deployer](https://github.com/mosabua/maven-android-sdk-deployer) :

	git clone https://github.com/mosabua/maven-android-sdk-deployer.git
	cd maven-android-sdk-deployer/
	mvn install -P 2.3.3
	mvn install -P 4.4
	cd extras/compatibility-v4/
	mvn clean install

## Installation
Use Maven to install these archetypes in your local Maven repository :

	git clone https://github.com/destinyd/android-archetypes.git
	cd android-archetypes/
	mvn clean install

## android-library-project archetype
This archetype creates a multi-module project containing the Android application, an Android library project and a project for testing this application and its library (instrumentation tests).
This archetype may be use to develop a complete Android application using a custom Android library or to develop an Android library with an example application using this library :

	mvn archetype:generate \
		-DarchetypeArtifactId=android-library-project \
		-DarchetypeGroupId=com.github.destinyd.android.archetypes \
		-DarchetypeVersion=0.0.1 \
		-DarchetypeCatalog=local \
		-DarchetypeRepository=local \
		-DgroupId=your.company \
		-DartifactId=my-android-library-project \
		-Dpackage=your.company.mylib \
		-Dversion=0.1 \
		-DinteractiveMode=false

where properties :

* `-DgroupId` : your Maven project groupId
* `-DartifactId` : the name of your Maven project
* `-Dversion` : the first version number of your Maven project

You can define three optional properties :

* `-Dpackage` : define the package used by the library (default : the given `groupId`)
* `-DminSdkVersion` : the minimum API Level required for the library (default : 10, Android 2.3.3)
* `-DtargetSdkVersion` : the targeted Android platform version to use (default : 19, Android 4.4)

Once generated, your application is ready to be built and tested. Start an android emulator or plug an Android dev phone ([USB debugging must be enabled in Developer options settings](http://developer.android.com/tools/device.html#setting-up)) and execute the following commands :

	cd my-android-library-project
	mvn clean install

To deploy and launch the application with Maven :

	cd my-android-library-project
	mvn clean install android:deploy android:run

## Licensing
Licensed under the Apache Software License, Version 2.0.

## History
Inspired from [android-archetypes Github project](https://github.com/akquinet/android-archetypes) created by [akquinet AG](http://www.akquinet.de/en.html).
