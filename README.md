# flutter android google signin without firebase

A new Flutter project.

## Getting Started

1) edit pubsec.yml
  google_sign_in: ^5.4.2

2) create keytool jks file 
  - cd {JDK_BIN_PATH}
  - ./keytool -genkey -v -keystore ~/flutter_android_signin.jks -keyalg RSA -keysize 2048 -validity 10000 -alias androiddebugkey

  after created flutter_android_signin.jks 
  do it : copy flutter_android_signin.jks -> paste flutter_google_signin/android/app/flutter_android_signin.jks

3) modify android/app/build.gradle
    like this :
    defaultConfig {
        applicationId "com.example.flutter_google_signin"
        minSdkVersion flutter.minSdkVersion
        targetSdkVersion flutter.targetSdkVersion
        versionCode flutterVersionCode.toInteger()
        versionName flutterVersionName
    }
    signingConfigs {
        debug {
            keyAlias 'androiddebugkey'
            keyPassword '123456'
            storeFile file('flutter_android_signin.jks')
            storePassword '123456'
        }
    }
    buildTypes {
        release {
            signingConfig signingConfigs.debug
        }
    }

4) build android package
 - intellij shift+shift
   chose execute gradle task
   >run gradle build with android directory
   
 - intellij shift+shift
   chose execute gradle task
   >gradle signinReport with android directory

   ![alt text]()
   ![alt text]()
   ![alt text]()

5) google console settings 
 - https://console.cloud.google.com/apis/credentials -> create credential
 - copy app/build.gradle applicationId "com.example.flutter_google_signin" and paste credential
 -modify OAuth consent screen add usertype external and add testuser

   ![alt text]()

6) finally : run it

   ![alt text]()
   ![alt text]()
   ![alt text]()