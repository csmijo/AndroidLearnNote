# Android monkeyʹ�����

`����` `monkey`

--

## 1. monkey �Ļ���ʹ��

1. `monkey`�ĵ��ٷ���ַ��https://developer.android.com/studio/test/monkey.html
2. ʹ�� `monkey` �����ַ�ʽ��
    * ��һ�ַ�ʽ��shell ������
        1. ���� `adb shell`  
        2. ���� `"/system/bin"` ·���µ� `monkey`�ű�
        
            ```
            $ adb shell
            # cd /system/bin
            # monkey
            ```
    * �ڶ��ַ�ʽ��ֱ�� pc ���� 
        
        ֱ��ͨ�����µ��������У�
        
        ```
        $ adb shell /system/bin/monkey
        ```
    * �����ַ�ʽ������ ͨ�� PC ��������monkey ������־���Ա��浽 PC �ϣ�ͨ�� Shell ��������monkey ������־���Ա��浽�ֻ��
        
3. ����ѡ��`[options]` ���������£�

    ```
    $ adb shell monkey [options] <event-count>
    ```

## 2. monkey �������ʹ��

`monkey` �� `option` �������Ǹ��ݾ���������趨�ģ���Ҫ��Ϊ���࣬�ֱ�Ϊ�� **�����ࡢ�¼��ࡢԼ���ࡢ������͹ٷ����������**��

### 2.1 monkey �ĳ���������

![monkey����������.PNG](http://on9czqsf5.bkt.clouddn.com/monkey����������.PNG?2017-04-10-17-03-49)

1. `-h`: ��ʾ `monkey` ����������Ϣ usage
2. `-v`: ��ӡ����־��Ϣ��ÿ�� `-v` �����ӷ�����Ϣ�ļ��������ʽΪ��
    ```
    $ adb shell monkey -v <event-count>
    ```

  `-v` Խ����־��Ϣ����ϸ������Ŀǰ���֧�� 3 �� `-v`������
    * 0���� ��������ʾ��������ɺ����ս�����ṩ������Ϣ
    * 1���� �ṩ����ϸ������Ϣ����������� Activity ���¼�
    * 2���� �ṩ����ϸ��װ��Ϣ��������б�ѡ�л�Ϊ��ѡ�е� Activity


### 2.2 monkey ���¼�������

![monkey�¼�������.PNG](http://on9czqsf5.bkt.clouddn.com/monkey�¼�������.PNG?2017-04-10-17-04-14)

1. `-f`: ��Ӳ��Խű�������ʾҪʹ�� `monkey` ����ָ���� `monkey` �ű�������ʾ����
    
    ```
    $ adb shell monkey -f <scriptfile>  <event-count>
    $ abd shell monkey -f /mnt/sdcard/test 10
    ```
2. `-s`: ���������������� seed ֵ��**���ʹ����ͬ��seed ֵ�ٴ����� monkey����������ͬ���¼�����**��Ҳ����˵�ظ�ִ�иղŵ����������

    �����ʽΪ��
    ```
    $ adb shell monkey -s <seed> <event-count>
    ```
3. `--throttle`: ���ʱ�䣬��λΪ ms(<milliseconds>)����ʾ�¼�֮��Ĺ̶��ӳ�(��ִ��ÿһ��ָ������ʱ��)��������Ӹ�ѡ�`monkey` �������ӳ١�

    �����ʽ��
    ```
    $ adb shell monkey --throttle <milliseconds>
    ```
    
4. `--ptc-touch`: ���**�����¼��ٷֱ�**�������ʽ��
    ```
    $ adb shell monkey --ptc-touch <percent>
    ```
    
5. `--ptc-motion`: ���**�����¼��ٷֱ�**�������¼�������ָ���Ʋ���������ָ��ĳһ��λ�ð���(��Down�¼�)�󾭹�һϵ��α����¼�����(��Up�¼�)��
6. `--ptc-trackball`: ���**�켣���¼��ٷֱ�**���켣���¼�����һϵ�е�����ƶ����Լ�ż���������ƶ�����ĵ���¼���
7. `--ptc-nav`: ���**���������¼��ٷֱ�**�� ���������¼���Ҫָ���Է��������豸���ϡ��¡������¼���
8. `--ptc-majornav`: ���**��Ҫ�����¼��ٷֱ�**����Ҫ�����¼�ͨ��ָ����ͼ�ν����һЩ�������� 5-way �����м䰴�������ذ������˵������ȡ�
9. `--ptc-syskeys`: ���**ϵͳ�����¼��ٷֱ�**��ϵͳ�����¼�ͨ��ָ����ϵͳʹ�õı������������� home����back�������ż��ȡ�
10. `--ptc-appswitch`: ���**Ӧ�������¼��ٷֱ�**��ҽ�������¼��׳� ��Ӧ�ã�ͨ������`startActivity()` ��������޶ȵؿ����� package �µ�����Ӧ�á�
11. `--ptc-anyevent`: ���**���������¼��ٷֱ�**�����������ᵽ���¼���ȫ�������������¼���

### 2.3 monkey ��Լ��������

![monkeyԼ��������.PNG](http://on9czqsf5.bkt.clouddn.com/monkeyԼ��������.PNG?2017-04-10-17-15-55)

1. `-p`: ���һ����������(<allowed-package-name>)�����Ӧ����Ҫ��������������� Activity������صİ�Ҳ��Ҫ�ڴ�ͬʱָ���������ָ���κΰ���`monkey`������ϵͳ����ȫ������� Activity�� **ÿһ�� -p ��Ӧһ������ָ�������ʱÿ������ǰ����Ҫ���� -p**���磺
    ```
    $ adb shell monkey -p <allowed-package-name> <event-count>
       
    $ adb shell monkey -p com.csmijo.test 1000
    ```
2. `-c`: ���һ�����������(�� <main-category> ����)��`monkey` ��ֻ����ϵͳ������Щ�����ĳ������г��� Activity�������ָ���κ����monkey ��ѡ��`Intent.CATEGORY_LAUNCH` �� `Intent.CATEGORY_monkey`��� Activity��

### 2.4 monkey ����������

![monkey����������.PNG](http://on9czqsf5.bkt.clouddn.com/monkey����������.PNG?2017-04-10-17-38-31)


1. `--dbg-no-events`: �����ô�ѡ���monkey �������ʼ���������뵽ĳ������ Activity �в����һ�������¼��������ʽ��
    ```
    $ adb shell monkey --dbg-no-events <event-count>
    ```
    
2. `--hprof`: �����ô���󣬽���`monkey`�¼�����ǰ���������� `profiling report`�� **��ѡ��� data/misc ������ 5MB ��С���ļ������ã�**
3. `--ignore-crashes`: �����ô���󣬵�Ӧ�ó���������߷���ʧ���쳣ʱ�� `monkey` ����������ֱ��������ɡ���������ô�ѡ�`monkey` �����������������쳣��ֹͣ���С�
4. `--ignore-timeouts`: �����ô�ѡ��󣬵�Ӧ�ó������κγ�ʱ����(��ANR)ʱ��`monkey` ����������ֱ��������������������ô�ѡ�`monkey` �������೬ʱ�Ի���ֹͣ���С�
5. `--ignore-security-exceptions`: �����ô�ѡ��󣬵�Ӧ�ó������κ�Ȩ�޴���(������һ����ҪĳЩȨ�޵� Activity)ʱ��`monkey` ����������ֱ��������ɡ���������ô�ѡ�`monkey` ��������Ȩ�޴���ֹͣ���С�
6. `--kill-process-after-error`: �����ô�ѡ��󣬵�`monkey` ��ΪӦ�ó���������ֹͣʱ������֪ͨϵͳ���ʷ�������Ľ��̡���������ô����`monkey` ֹͣʱ���������Ӧ�ó��򽫼�����������״̬��
7. `--monitor-nativie-crashes`: �����ô�ѡ���`monkey` ����ʱ `native code` �ı����¼��������ӱ����档����������򲻻���ӡ�
8. `--wait-dbg`: �����ô�ѡ��󣬽���ִͣ���е� `monkey`,֪���е������������ӡ�

### 2.5 �ٷ����������

1. `--pkg-blacklist-file`: ���� `monkey` ������ָ���������ĵ��м�¼�İ�(package)�����û��ʹ�����������monkey �����ϵͳ�����еĵİ������ʹ���������������ͨ���ں������ĵ��м�¼���в���Ҫ���Եİ����ƣ�����ֽ monkey ��ִ�з�Χ�� **�������ĵ���ÿһ��ֻ�ܷ�һ������**

2. `--pkg-whitelist-file`: ����`monkey` ֻ����ָ���İ������ĵ��м�¼�İ������û��ʹ�����������monkey �����ϵͳ�����еİ������ʹ���������������ͨ���ڰ������ĵ��ڼ�¼����Ҫ���Եİ���������monkey ��ִ�з�Χ��**�������ĵ���ÿһ��ֻ�ܷ�һ��������**

    **ע�⣺**���Ҫ���Եİ��������İ��й����������һ��ָ����Щ����ִ�����������

## 3. monkey �ű���д

### 3.1 monkey API ���

1. **�켣���¼�**

    ```
    DispatchTrackball(long downTime, long eventTime, int action, float x, float y, float pressure, float size, int metaState, float xPrecision, float yPrecision, int device, int edgeFlags)
    ```
   **ֻ��Ҫ��ע�� action��x��y ����**
   * ACTION_DOWN = 0
   * ACTION_UP = 1
   * ACTION_MULTIPLE = 2
   
2. **�����ַ����¼�**

    ```
    DispatchString(String text)
    ```
    
3. **����¼�**

    ```
    DispatchPointer(long downTime, long eventTime, int action, float x, float y, float pressure, float size, int metaState, float xPrecision, float yPrecision, int device, int edgeFlags)
    ```
    **ֻ��Ҫ��ע�� action��x��y ����**
    
4. **����Ӧ��**

    ```
    LaunchActivity(String pkg_name,String cl_name)
    ```
    
5. **�ȴ��¼�**

    ```
    UserWait(long sleeptime)
    ```
    **ʱ��ĵ�λΪ������(millisecond)**
6. **���¼�ֵ**

    ```
    DispatchPress(int keyCode)
    ```
    
7. **������ֵ**

    ```
    LongPress(int keyCode)
    ```
    
8. **���ͼ�ֵ**

    ```
    DispatchKey(long downTime, long eventTime, int action, int code, int repeat, int metaState, int device, int scancode)
    ```
    
9. **���������**

    ```
    DispatchFlip(boolean keyboardOpen)
    ```
    
### 3.2 monkey �ű���д

```
type= raw events
count= 10
speed= 1.0
start data >>
captureDispatchPointer(5109520,5109520,0,230.75429,458.1814,0.20784314,0.06666667,0,0.0,0.0,65539,0)
captureDispatchKey(5113146,5113146,0,20,0,0,0,0)
captureDispatchFlip(true)
...
```

## 4. monkey ��־����

### 4.1 monkey ��־�ı��淽��

1. ������ pc �У��������£�
    
    ```
    $ adb shell monkey [options] <event-count> > d:\monkeylog.txt
    ```
    
2. �������ֻ��У��������£�

    ```
    $ adb shell
    # monkey [options] <event-count> /mnt/sdcard/monkeylog.txt
    ```
    
3. ��׼����������ֿ����棬�������£�

    ```
    # monkey [options] <event-count> 1>/mnt/sdcard/monkeylog.txt 2>/mnt/sdcard/monkeyErrorlog.txt
    ```
    
### 4.2 monkey ��־���ݽ���

1. �����ؼ���"ANR" ���� ANR �����Ϣ
2. �����ؼ���"CRASH" ���� Crash �����Ϣ