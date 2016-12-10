Android NDK
=

####���֪ʶ�㣺####
1. Android���濪��
2. �ײ㿪��
3. jni��������
4. jni�����java��
5. ndk���Դ���

Android Studio �������ʽ
-
1. ������ͨAndroid��Ŀ
2. ��`MainActivity.java`�м���native�������������´���

  ```java
  public static native String getStringFromJNI();
  ```
    
3. ��Android Studio��Terminal�н��뵽`app\src\main`Ŀ¼
4. ʹ��`javah`����C���Ե�ͷ�ļ�
  
  ```java
  javah -d <���Ŀ¼> -classpath <��·��> <����������>
  ```
  
  ʾ����
  
  ```xml
  javah -d jni -classpath D:\Android\sdk\platforms\android-23\android.jar;
  D:\Android\sdk\extras\android\support\v4\android-support-v4.jar;
  D:\Android\sdk\extras\android\support\v7\appcompat\libs\android-support-v7-appcompat.jar;..\..\build\intermediates\classes\debug com.kim.android_study_ndk.MainActivity
  ```

5. ִ�гɹ��󣬽���`app\src\main\jni`Ŀ¼�����ɶ�Ӧ��`*.h`�ļ�<br>
  ʾ����`com_kim_android_study_ndk_MainActivity.h`
  
6. ��`app\src\main\jni`������Ҫ��`*.c`�ļ������������ɵ�`*.h`ͷ�ļ�<br>
  ʾ����
  
  ```c
  #include "com_kim_android_study_ndk_MainActivity.h"

  JNIEXPORT jstring JNICALL Java_com_kim_android_1study_1ndk_MainActivity_getStringFromJNI
  (JNIEnv * env, jclass jclass)
  {
      return (*env)->NewStringUTF(env,"Hello From JNI!");
  }
  ```

7. ��`gradle.properties`�����`android.useDeprecatedNdk=true`
8. ��`local.properties`������NDK·��(`ndk.dir=`)
9. ��`<project>\app\build.gradle`��������´��룺
  ```java
  ndk {
            moduleName "android_study_ndk"
            ldLibs "log", "z", "m"
            abiFilters "armeabi", "armeabi-v7a", "x86", "x86_64"
        }
  ```
  * `moduleName`Ϊģ����
  * `ldLibs`
  * `abiFilters`Ϊ����İ汾

10. �����ɺ�ִ��`Build->Make`��ִ����ɺ�ͻ���<br>
  `app/build/intermediates/ndk/debug/obj/local`�д�����Ӧ��`*.so`�ļ�

11. ֮����native�������ڵ�java�ļ��м������´��룺

  ```java
  static {
      System.loadLibrary("android_study_ndk");
  }
  ```
    * `loadLibrary()`�еĲ���Ϊ��9����ģ����

12. ���벿��App