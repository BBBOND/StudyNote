Android NDK
=

####相关知识点：####
1. Android常规开发
2. 底层开发
3. jni函数调用
4. jni层调用java层
5. ndk调试代码

Android Studio 环境搭建方式
-
1. 创建普通Android项目
2. 在`MainActivity.java`中加入native方法，比如以下代码

  ```java
  public static native String getStringFromJNI();
  ```
    
3. 在Android Studio的Terminal中进入到`app\src\main`目录
4. 使用`javah`生成C语言的头文件
  
  ```java
  javah -d <输出目录> -classpath <类路径> <带包名的类>
  ```
  
  示例：
  
  ```xml
  javah -d jni -classpath D:\Android\sdk\platforms\android-23\android.jar;
  D:\Android\sdk\extras\android\support\v4\android-support-v4.jar;
  D:\Android\sdk\extras\android\support\v7\appcompat\libs\android-support-v7-appcompat.jar;..\..\build\intermediates\classes\debug com.kim.android_study_ndk.MainActivity
  ```

5. 执行成功后，将在`app\src\main\jni`目录下生成对应的`*.h`文件<br>
  示例：`com_kim_android_study_ndk_MainActivity.h`
  
6. 在`app\src\main\jni`创建需要的`*.c`文件，并引入生成的`*.h`头文件<br>
  示例：
  
  ```c
  #include "com_kim_android_study_ndk_MainActivity.h"

  JNIEXPORT jstring JNICALL Java_com_kim_android_1study_1ndk_MainActivity_getStringFromJNI
  (JNIEnv * env, jclass jclass)
  {
      return (*env)->NewStringUTF(env,"Hello From JNI!");
  }
  ```

7. 在`gradle.properties`中添加`android.useDeprecatedNdk=true`
8. 在`local.properties`中配置NDK路径(`ndk.dir=`)
9. 在`<project>\app\build.gradle`中添加如下代码：
  ```java
  ndk {
            moduleName "android_study_ndk"
            ldLibs "log", "z", "m"
            abiFilters "armeabi", "armeabi-v7a", "x86", "x86_64"
        }
  ```
  * `moduleName`为模块名
  * `ldLibs`
  * `abiFilters`为编译的版本

10. 添加完成后，执行`Build->Make`，执行完成后就会在<br>
  `app/build/intermediates/ndk/debug/obj/local`中创建对应的`*.so`文件

11. 之后在native方法所在的java文件中加入如下代码：

  ```java
  static {
      System.loadLibrary("android_study_ndk");
  }
  ```
    * `loadLibrary()`中的参数为第9步的模块名

12. 编译部署App