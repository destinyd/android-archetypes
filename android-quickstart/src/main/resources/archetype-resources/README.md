Android ${rootArtifactId}
============
${rootArtifactId}

如何引用此组件：
-------------
** 安装 **

```
git clone https://github.com/destinyd/${artifactId}
cd ${artifactId}
mvn clean install
```

** maven引用 **

在maven项目，pom.xml添加以下依赖引用：

```
<dependency>
    <groupId>${groupId}</groupId>
    <artifactId>${artifactId}</artifactId>
    <version>${version}</version>
    <type>apklib</type>
</dependency>
```

** android权限设置 **
AndroidManifest.xml 添加如下权限
```
```

使用说明
---------------------
请参考示例


依赖库
---------------------
* [destinyd/android-archetypes][android-archetypes]


[android-archetypes]: https://github.com/destinyd/android-archetypes
