fix file node_module/react-native-camera/android/build.gradle

buildscript {
  repositories {
    jcenter()
     maven { url "https://jitpack.io" }
    maven {
      url 'https://maven.google.com'
    }
  }

  dependencies {
    classpath 'com.android.tools.build:gradle:3.0.0'
  }
}

apply plugin: 'com.android.library'

def DEFAULT_COMPILE_SDK_VERSION             = 26
def DEFAULT_BUILD_TOOLS_VERSION             = "26.0.2"
def DEFAULT_TARGET_SDK_VERSION              = 26
def DEFAULT_GOOGLE_PLAY_SERVICES_VERSION    = "12.0.1"
def DEFAULT_SUPPORT_LIBRARY_VERSION         = "27.1.0"

android {
  compileSdkVersion rootProject.hasProperty('compileSdkVersion') ? rootProject.compileSdkVersion : DEFAULT_COMPILE_SDK_VERSION
  buildToolsVersion rootProject.hasProperty('buildToolsVersion') ? rootProject.buildToolsVersion : DEFAULT_BUILD_TOOLS_VERSION

  defaultConfig {
    minSdkVersion 16
    targetSdkVersion rootProject.hasProperty('targetSdkVersion') ? rootProject.targetSdkVersion : DEFAULT_TARGET_SDK_VERSION

    versionCode 1
    versionName "1.0.0"
  }
  lintOptions {
    abortOnError false
    warning 'InvalidPackage'
  }
}

repositories {
  mavenCentral()
  maven {
   url 'https://maven.google.com'
  }
  maven { url "https://jitpack.io" }
  maven {
    // All of React Native (JS, Obj-C sources, Android binaries) is installed from npm
    url "$rootDir/../node_modules/react-native/android"
  }
}

dependencies {
  def googlePlayServicesVersion = rootProject.hasProperty('googlePlayServicesVersion')  ? rootProject.googlePlayServicesVersion : DEFAULT_GOOGLE_PLAY_SERVICES_VERSION
  def supportLibVersion = rootProject.hasProperty('supportLibVersion')  ? rootProject.supportLibVersion : DEFAULT_SUPPORT_LIBRARY_VERSION

  provided 'com.facebook.react:react-native:+'
  provided 'com.facebook.infer.annotation:infer-annotation:+'
  compile "com.google.zxing:core:3.2.1"
  compile "com.drewnoakes:metadata-extractor:2.9.1"
  compile "com.google.android.gms:play-services-vision:$googlePlayServicesVersion"
  compile "com.android.support:exifinterface:$supportLibVersion"
  compile "com.android.support:support-annotations:$supportLibVersion"
  compile "com.android.support:support-v4:$supportLibVersion"
}