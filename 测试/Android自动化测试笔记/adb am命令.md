# adb am ����

`adb` `am`

---

�� `Android` �����У�������ʹ�� `am` ����������������� `am` ��һЩ��������С�ᡣ
ʹ�õ� Android ϵͳ�� `Android 4.3��API 18`

## 1. am ����

��`adb shell` ������������ `am --help`�� ���Կ������µİ����ĵ���

```
usage: am [subcommand] [options]           # �����ʽ
usage: am start [-D] [-W] [-P <FILE>] [--start-profiler <FILE>]      
               [--R COUNT] [-S] [--opengl-trace]
               [--user <USER_ID> | current] <INTENT>     # ���� Activity
       am startservice [--user <USER_ID> | current] <INTENT>   # ���� Service
       am force-stop [--user <USER_ID> | all | current] <PACKAGE>  # ǿɱ����
       am kill [--user <USER_ID> | all | current] <PACKAGE>     # ɱ��ָ����̨����
       am kill-all   # ɱ�����к�̨����
       am broadcast [--user <USER_ID> | all | current] <INTENT>  # ���͹㲥
       am instrument [-r] [-e <NAME> <VALUE>] [-p <FILE>] [-w]
               [--user <USER_ID> | current]
               [--no-window-animation] <COMPONENT>    # Typically this target <COMPONENT>  is the form <TEST_PACKAGE>/<RUNNER_CLASS>. 
       am profile start [--user <USER_ID> current] <PROCESS> <FILE>
       am profile stop [--user <USER_ID> current] [<PROCESS>]
       am dumpheap [--user <USER_ID> current] [-n] <PROCESS> <FILE>
       am set-debug-app [-w] [--persistent] <PACKAGE>
       am clear-debug-app
       am monitor [--gdb <port>]       # ���
       am hang [--allow-restart]       
       am screen-compat [on|off] <PACKAGE>
       am to-uri [INTENT]
       am to-intent-uri [INTENT]
       am switch-user <USER_ID>
       am stop-user <USER_ID>
```

## 2. options

### 2.1 ���� Activity

���� `Activity` ����ʹ�� `options` ��������������ϸ�Ľ��ܣ�

```
1.    -D: enable debugging ������Թ���
2.    -W: wait for launch to complete  �ȴ� app �������
3.    --start-profiler <FILE>: start profiler and send results to <FILE>  ���� profiler������������͵� <FILE>
4.    -P <FILE>: like above, but profiling stops when app goes idle  ���� --start-profiler����ͬ���ǵ� app ���� idle ״̬����ֹͣ profiling
5.    -R: repeat the activity launch <COUNT> times.  Prior to each repeat,
        the top activity will be finished.   �ظ����� Activity COUNT �Ρ�ÿ������֮ǰ�����ϲ�� activity ���� finish
6.    -S: force stop the target app before starting the activity ���� activity ֮ǰ���ȵ��� forceStopPackage() ����ǿ��ֹͣ app
7.    --opengl-trace: enable tracing of OpenGL functions  ���л�ȡ OpenGL ������trace
8.    --user <USER_ID> | current: Specify which user to run as; if not
        specified then run as the current user.  ָ�����е��û�
```

���� `activity` ��ʵ��ԭ�� ���� `-W` ��������� `startActivityAndWait()` ���������У�������� `startActivityAsUser()` ������


## 3. Intent

`Intent` �Ĳ����� `flags` �Ƚ϶࣬Ϊ�˷����������Ϊ�������Ͳ����� **���ò�����Extra������Flags����**

### 3.1 ���ò���

1. `-a <ACTION>`: ָ��`Intent action`�� ʵ��ԭ��`Intent.setAction()`��
2. `-n <COMPONENT>`: ָ�����������ʽΪ`{����}/.{��Activity��}`��ʵ��ԭ��`Intent.setComponent()`��
3. `-d <DATA_URI>`: ָ��`Intent data URI`��ʵ��ԭ�� `Intent.setData()`����������
4. `-t <MIME_TYPE>`: ָ��`Intent MIME Type`��ʵ��ԭ�� `Intent.setType()`????;
5. `-c <CATEGORY> [-c <CATEGORY>] ...]`:ָ��`Intent category`��ʵ��ԭ��`Intent.addCategory()`;
6. `-p <PACKAGE>`: ָ��������ʵ��ԭ��`Intent.setPackage()`;
7. `-f <FLAGS>`: ���`flags`��ʵ��ԭ��`Intent.setFlags(int )`��**�����ŵĲ���������int�ͣ�**


ʵ����

```
am start -a android.intent.action.VIEW
am start -n com.csmijo.test/.MainActivity
am start -d content://contacts/people/1
am start -t image/png
am start -c android.intent.category.APP_CONTACTS
```

### 3.2 Extra ����

#### 3.2.1 ��������
 
|����|	-e/-es|	-esn|	-ez|	-ei|	-el|	-ef|	-eu|	-ecn|
|:--|:--|:--|:--|:--|:--|:--|:--|:--|
|����|	String|	(String)null|	boolean|	int|	long|	float|	uri|	component|

�������es��Extra String����ĸ��ƣ�ʵ����

```
am start -n com.yuanhh.app/.MainActivity -es website gityuan.com
```

�˴�`-es website gityuan.com`���ȼ���`Intent.putExtra(��website��, ��gityuan.com��)`;

#### 3.2.2 ��������

|����|-eia|	-ela|	-efa|
|:--|:--|:--|:--|
|��������|int[]	|long[]|	float[]|

�������`eia`����`Extra int array`����ĸ��ƣ����`value`ֵ֮���Զ��Ÿ�����ʵ����

```
am start -n com.yuanhh.app/.MainActivity -ela weekday 1,2,3,4,5
```

�˴�`-ela weekday 1,2,3,4,5`���ȼ���`Intent.putExtra(��weekday��, new int[]{1,2,3,4,5})`;

### 3.3 Flags ����

��#3.1 ���ò����У��ᵽ��`-f <FLAGS>`����ͨ��`Intent.setFlags(int )`������������`Intent`��`flags`.��С��Ҳ�ǹ���`flags`����ͨ��`Intent.addFlags(int )`������������ʾ�����е�`flags`������
```
    [--grant-read-uri-permission] [--grant-write-uri-permission]
    [--debug-log-resolution] [--exclude-stopped-packages]
    [--include-stopped-packages]
    [--activity-brought-to-front] [--activity-clear-top]
    [--activity-clear-when-task-reset] [--activity-exclude-from-recents]
    [--activity-launched-from-history] [--activity-multiple-task]
    [--activity-no-animation] [--activity-no-history]
    [--activity-no-user-action] [--activity-previous-is-top]
    [--activity-reorder-to-front] [--activity-reset-task-if-needed]
    [--activity-single-top] [--activity-clear-task]
    [--activity-task-on-home]
    [--receiver-registered-only] [--receiver-replace-pending]
```

���磬����`action=��broadcast.demo��`�Ĺ㲥�����Ҷ���`forceStopPackage()`��Ӧ�ò�������ոù㲥���������£�

```
am broadcast -a broadcast.demo --exclude-stopped-packages
```

---
[�ο�����]

* [Android ������](https://developer.android.com/studio/command-line/adb.html?hl=zh-cn)
* [Am �����÷�](http://gityuan.com/2016/02/27/am-command/)