### gradlew的使用

gradlew其实就是gradle wrapper，它的作用在于允许客户端在没有安装gradle的环境下通过
简单的命令也能直接进行项目构建，内部的实现原理其实就是先查找用户目录GRADLE_USER_HOME，
默认为用户的目录，如下

    C:\Users\zhenglian\.gradle\wrapper\dists
中是否存在gradle，如果存在就直接使用，否则就从给定的地址下载一个

gradle wrapper命令会自动生成gradle目录，目录结构如下：

    - gradle
        - wrapper
            - gradle-wrapper.jar # gradlew命令依赖
            - gradle-wrapper.properties # gradlew初始化配置
gradle-wrapper.properties中配置了gradlew命令的初始化参数，包括gradlew运行时检查
gradle是否存在的目录，gradle下载的地址

可以在项目build.gradle文件中修改gradle-wrapper.properties中的配置参数

    wrapper {
        gradleVersion = "4.9" # 下载的gradle版本
        distributionType = "bin" # 下载的gradle包类型，有两种：bin, all all包含文档已经源码jar
    }
当配置好build.gradle之后，通过命令生成gradlew

    gradle wrapper # 直接修改build.gradle
    gradle wrapper --gradle-version 4.9 --distribution-type bin # 命令行指定参数
项目发布的时候将生成的以下文件上传即可
    
    gradle
        wrapper
            gradle-wrapper.jar
            gradle-wrapper.properties
    src
    build.gradle
    gradlew
    gradlew.bat
    settings.gradle

生成gradlew命令之后，我们就可以直接使用gradlew来进行项目构建了

    gradlew.bat clean build