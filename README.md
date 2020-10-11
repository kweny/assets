# Droaket

积累了一些实用的工具和脚本，目前发布了下面这些——

* **bintray-upload-normal.gradle**：一个通过 Bintray 向 Maven 中央仓库发布项目的 Gradle 脚本。

* **skip-module-task.gradle**：Gradle 构建工程时，跳过指定 module 的指定 task。

---

## bintray-upload-normal.gradle

这是一个通过 Bintray 向 Maven 中央仓库发布项目的 Gradle 脚本。

### Use in build.gradle:

可直接在配置文件 build.gradle 中通过 apply 指令引入使用，如下——

```groovy
apply from: 'https://raw.githubusercontent.com/kweny/assets/master/gradle/bintray-upload-normal.gradle'
```

### Dependent build script:

需要在项目的 Gradle 配置文件中引入 Bintray 官方插件的依赖——

```groovy
buildscript {
    ...
    dependencies {
        ...
        classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.8.0'
    }
}
```

### Dependent custom properties:

同时在项目的 Gradle 配置文件中自定义项目相关信息——

```groovy
ext {
    BINTRAY_REPO = 'maven'
    BINTRAY_NAME = 'carefree-mongodb-spring-boot-starter'

    PUBLISHED_PACKAGING = 'jar'
    PUBLISHED_GROUP_ID = 'org.kweny.carefree'
    PUBLISHED_ARTIFACT_ID = 'carefree-mongodb-spring-boot-starter'
    PUBLISHED_VERSION = '1.0.1'

    PROJECT_NAME = 'Carefree MongoDB'
    PROJECT_DESCRIPTION = 'A MongoDB auto-configuration starter for SpringBoot.'
    PROJECT_WEBSITE_URL = 'https://github.com/kweny/carefree-mongodb-spring-boot-starter'
    PROJECT_VCS_URL = 'https://github.com/kweny/carefree-mongodb-spring-boot-starter.git'
    PROJECT_ISSUE_TRACKER_URL = 'https://github.com/kweny/carefree-mongodb-spring-boot-starter/issues'

    DEVELOPER_ID = 'kweny'
    DEVELOPER_NAME = 'Kweny'
    DEVELOPER_EMAIL = 'iamkweny@gmail.com'

    LICENSE_NAME = 'The Apache Software License, Version 2.0'
    LICENSE_URL = 'http://www.apache.org/licenses/LICENSE-2.0.txt'
    ALL_LICENSES = ["Apache-2.0"]
}
```

### Secret properties file:

Bintray 账号信息需要通过一个额外的 properties 文件来配置，这个文件需要使用特定的名称来命名，按优先级如下——

* local.properties
* gradle-local.properties
* gradle.properties

**如果使用了版本工具来管理代码，请记得将这个文件加入到忽略规则中（如 .gitgnore），以免泄露 Bintray 账号信息。**

这个文件的内容如下——

```groovy
bintray.user=bintray_username
bintray.apiKey=bintray_apikey
bintray.gpg.password=bintray_gpg_password
```

### An example:

一个完整的 build.gradle 结构示例（别忘了还需要一个额外的 properties 文件）——

```groovy
buildscript {
    repositories {
        jcenter()
        mavenCentral()
    }
    dependencies {
        classpath 'org.springframework.boot:spring-boot-gradle-plugin:2.0.4.RELEASE'
        classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.8.0'
    }
}

apply plugin: 'java'
apply plugin: 'idea'
apply plugin: 'maven'
apply plugin: 'maven-publish'

group 'org.kweny.carefree'
version '1.0.1'

sourceCompatibility = 8

repositories {
    jcenter()
    mavenCentral()
}

dependencies {
    compile group: 'org.springframework.boot', name: 'spring-boot-configuration-processor', version: '2.0.4.RELEASE'
    compile group: 'org.springframework.boot', name: 'spring-boot-starter', version: '2.0.4.RELEASE'
    compile group: 'org.springframework.data', name: 'spring-data-mongodb', version: '2.0.10.RELEASE'
    compile group: 'org.mongodb', name: 'mongo-java-driver', version: '3.8.1'

    testCompile group: 'org.springframework.boot', name: 'spring-boot-starter-web', version: '2.0.4.RELEASE'

}

[compileJava, compileTestJava]*.options*.encoding = 'UTF-8'

ext {
    BINTRAY_REPO = 'maven'
    BINTRAY_NAME = 'carefree-mongodb-spring-boot-starter'

    PUBLISHED_PACKAGING = 'jar'
    PUBLISHED_GROUP_ID = 'org.kweny.carefree'
    PUBLISHED_ARTIFACT_ID = 'carefree-mongodb-spring-boot-starter'
    PUBLISHED_VERSION = '1.0.1'

    PROJECT_NAME = 'Carefree MongoDB'
    PROJECT_DESCRIPTION = 'A MongoDB auto-configuration starter for SpringBoot.'
    PROJECT_WEBSITE_URL = 'https://github.com/kweny/carefree-mongodb-spring-boot-starter'
    PROJECT_VCS_URL = 'https://github.com/kweny/carefree-mongodb-spring-boot-starter.git'
    PROJECT_ISSUE_TRACKER_URL = 'https://github.com/kweny/carefree-mongodb-spring-boot-starter/issues'

    DEVELOPER_ID = 'kweny'
    DEVELOPER_NAME = 'Kweny'
    DEVELOPER_EMAIL = 'iamkweny@gmail.com'

    LICENSE_NAME = 'The Apache Software License, Version 2.0'
    LICENSE_URL = 'http://www.apache.org/licenses/LICENSE-2.0.txt'
    ALL_LICENSES = ["Apache-2.0"]
}

apply from: 'https://raw.githubusercontent.com/kweny/assets/master/gradle/bintray-upload-normal.gradle'
```

---

## skip-module-task.gradle

在根工程目录下创建如下命名的配置文件（任选其一，也可三者同存，执行时将合并三者内容）——

* local.properties
* gradle-local.properties
* gradle.properties

其中内容如下——

```properties
# 跳过 droaket-core 模块的 test 任务
gradle.task.test.droaket-core=true

# 跳过 droaket-core 模块的所有任务，即不构建该模块
gradle.task.droaket-core=true

# 效果等同于未配置，即正常构建 droaket-web 模块
gradle.task.droaket-web=false
```

---
