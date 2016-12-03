
[gradle](http://gradle.org/)



```
wget https://downloads.gradle.org/distributions/gradle-2.11-bin.zip
sudo mkdir /usr/local/grale/
sudo unzip gradle-2.11-bin.zip -d /usr/local/grale/


sudo vi /etc/profile.d/zll.sh
export GRADLE_HOME=/usr/local/grale/gradle-2.11
export PATH=$GRADLE_HOME/bin:$PATH

# 启用 Gradle Daemon
vi ~/.gradle/gradle.properties
org.gradle.daemon=true


# 列出所有task
gradle tasks --all
```

## run main

build.gradle

```
# gradle -PmainClass=Boo execute
task execute(type:JavaExec) {
   main = mainClass
   classpath = sourceSets.main.runtimeClasspath
}

// gradle -DmainClass=me.test.Example bootRun
springBoot {
    mainClass = System.properties['mainClass']
}

// gradle -DmainClass=me.test.Example execute
task execute(type:JavaExec) {
    main = System.getProperty('mainClass')
    classpath = sourceSets.main.runtimeClasspath
}
```

## init plugin

```
gradle init --type groovy-library
gradle wrapper --gradle-version 3.1
```

## init script
maven可以通过 settings.xml 进行全局配置，比如本地仓库的位置，mirror等。
那Gradle如何进行类似设置？——可以使用 [init script](https://docs.gradle.org/current/userguide/init_scripts.html)

创建文件 `~/.gradle/init.gradle`

```
allprojects {
    repositories {
        mavenLocal()
        maven {
            url "http://mvn.kingsilk.xyz/content/groups/public/"
        }
    }
}

```

# io.spring.gradle:dependency-management-plugin


https://spring.io/blog/2015/02/23/better-dependency-management-for-gradle

```
buildscript {
  repositories {
    jcenter()
  }
  dependencies {
    classpath "io.spring.gradle:dependency-management-plugin:0.5.1.RELEASE"
  }
}

apply plugin: "io.spring.dependency-management"

dependencyManagement {
  imports {
    mavenBom 'io.spring.platform:platform-bom:1.1.1.RELEASE'
  }
}
dependencies {
    compile 'org.springframework:spring-core'
}
```