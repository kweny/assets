# assets

## bintray-upload-normal.gradle
```groovy
apply from: 'https://raw.githubusercontent.com/kweny/assets/master/gradle/bintray-upload-normal.gradle'
```

Dependent custom properties:
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
    DEVELIPER_NAME = 'Kweny'
    DEVELIPER_EMAIL = 'iamkweny@gmail.com'

    LICENSE_NAME = 'The Apache Software License, Version 2.0'
    LICENSE_URL = 'http://www.apache.org/licenses/LICENSE-2.0.txt'
    ALL_LICENSES = ["Apache-2.0"]
}
```

Secret properties file:
```groovy
IF file('local.properties').exists()
ELSE IF file('gradle-local.properties').exists()
ELSE file('gradle.properties')
```
