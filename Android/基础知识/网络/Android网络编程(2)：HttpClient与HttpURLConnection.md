#Android������(2):HttpClient��HttpURLConnection

`Android` `HttpClient` `HttpURLConnection`

--

##1. HttpClient

����Android SDK�а�����HttpClient����**Android6.0�汾ֱ��ɾ����HttpClient���**���������ʹ�����������ǣ�

* ���ʹ�õ���eclipse����libs�м���**org.apache.http.legacy.jar**,
���jar���ڣ�**sdk\platforms\android-23\optionalĿ¼�У���Ҫ����android
6.0��SDK��
* ���ʹ�õ���android studio�� ����Ӧ��module�µ�build.gradle�м��룺

    ```java
    android {
           useLibrary 'org.apache.http.legacy'
            }
    ```
    
##2. HttpURLConnection

����**Android 2.2�汾֮ǰ��HttpURLConnectionһֱ������һЩ�����ᷳ��bug**������˵��һ���ɶ���InputStream����close()����ʱ�����п��ܻᵼ�����ӳ�ʧЧ�ˡ���ô����ͨ���Ľ���취����ֱ�ӽ��õ����ӳصĹ��ܣ�
```java
private void disableConnectionReuseIfNecessary() {
      // ����һ��2.2�汾֮ǰ��bug
      if (Integer.parseInt(Build.VERSION.SDK) < Build.VERSION_CODES.FROYO) {
            System.setProperty("http.keepAlive", "false");
      }
}
```

��������**��Android 2.2�汾�Լ�֮ǰ�İ汾ʹ��HttpClient�ǽϺõ�ѡ�񣬶���Android 2.3�汾���Ժ�HttpURLConnection������ѵ�ѡ��**������API�򵥣������С������ǳ�������Android��Ŀ��ѹ���ͻ�����ƿ�����Ч�ؼ���������ʵ��������������ٶȺ�ʡ�緽��Ҳ���˽ϴ�����á�����**��Android 6.0�汾�У�HttpClient�ⱻ�Ƴ��ˣ�HttpURLConnection�����Ժ�����Ψһ��ѡ��**��