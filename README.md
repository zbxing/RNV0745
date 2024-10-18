# ThePairs
RN Games

## 0. 常用命令
>1. 运行Android工程: npx react-native run-android
>2. 三方依赖打补丁: yarn patch-package package-name
>3. 安装指定版本库: yarn add xxx@1.0.0 (安装开发依赖: yarn add --dev xxx)
>4. expo依赖库初始化: npx install-expo-modules
>5. expo依赖库安装: npx expo install expo-xxx
>6. git分支更新信息: git remote update origin --prune
>7. git删除指定名称的文件: find ./ -type f -name '.gitempty' -delete
>8. 查看签名文件信息: keytool -list -v -keystore debug.keystore
>9. 重置Metro缓存: yarn start --reset-cache

## Android打包
>1. 生成签名密钥: keytool -genkeypair -v -keystore release.keystore -alias release -keyalg RSA -keysize 2048 -validity 10000
>2. 查看签名信息: keytool -list -v -keystore release.keystore
>3. 生成正式包: ./gradlew assembleRelease bundleRelease
>4. 生成React-Native项目: npx react-native init AwesomeProject --version X.XX.X

## 编译错误
>1. Unable to make progress running work. there are items queued for execution but none of them can be started.
解决方法: 在settings.gradle文件顶部添加gradle.startParameter.excludedTaskNames.addAll([":ModuleName:testClasses"])，ModuleName是clean Project时输出的其中一个；或settings.gradle.kts文件顶部添加gradle.startParameter.excludedTaskNames.addAll(listOf(":ModuleName:testClasses"))

>2. Duplicate class kotlin.collections.jdk8.CollectionsJDK8Kt found in modules jetified-kotlin-stdlib-1.8.10 (org.jetbrains.kotlin:kotlin-stdlib:1.8.10) and jetified-kotlin-stdlib-jdk8-1.7.22 (org.jetbrains.kotlin:kotlin-stdlib-jdk8:1.7.22)
解决办法: 在app/build.gradle的dependencies中添加
constraints {
    implementation("org.jetbrains.kotlin:kotlin-stdlib-jdk8:1.8.0") {
        because 'align all versions of kotlin transitive dependencies'
    }
}
同时，在build.gradle中buildscript的ext配置kotlinVersion = "xxx"

>3. 