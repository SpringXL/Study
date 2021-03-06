> 配置全局仓库
```
//配置全局仓库
allprojects {
    repositories {
        mavenLocal()
        maven { url "https://repo.huaweicloud.com/repository/maven/" }
        maven { url "http://maven.aliyun.com/nexus/content/groups/public" }
        maven { url "https://repo.grails.org/grails/core" }
        maven { url "http://jasperreports.sourceforge.net/maven2/" }
    }
}


//启动时加载
bootRun {
    systemProperties = System.properties
}

//编译java文件时用utf-8编码
tasks.withType(JavaCompile) {
    options.encoding = "UTF-8"
}

//解决编译java时警告：请使用 -Xlint:unchecked 重新编译
compileJava {
    options.compilerArgs << "-Xlint:unchecked"
}
```
> 如需将项目的gradle-wapper.properties中的distributionUrl配置为本地zip，配置如下

```
#Fri Nov 27 23:09:32 CET 2015
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
#distributionUrl=https\://services.gradle.org/distributions/gradle-3.5-bin.zip
distributionUrl=file:///D:/gradle-3.5-bin.zip
```
> 解决运行时jdk path文件名过长问题
```
//解决运行时提示path文件名过长的问题
ext {
    //overcome error executing java for gson views compilation
    grails {
        pathingJar = true
    }
}
```
> 打包为指定名称
```
war {
    archiveName 'test.war'
}
```

* 加载application.properties文件，但只能加载application.properties，其他名字的properties不能加载
```
bootRun {
    systemProperties = System.properties
}
```

* 加载properties文件的另一种写法，没测试
```
bootRun {
  doFirst {
    bootRun.systemProperties = localBootRunProperties()
  }
}
```
