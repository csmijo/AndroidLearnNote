# adb��������

`adb`

---

ԭ�ģ�http://gityuan.com/2015/06/28/adb-notes/



## 1. ����ָ��

1. `adb -s serialNumber shell`  // ����ָ���豸
2. `adb version` // �鿴�汾
3. `adb logcat` // �鿴��־
4. `adb devices`  // �鿴�豸
5. `adb get-state`  // ����״̬
6. `adb start-server`  // ���� adb ����
7. `adb kill-server`  // ֹͣ adb ����
8. `adb push local remote` // �������͵��ֻ�
9. `adb pull remote local`  // �ֻ���ȡ������
10. `adb shell getprop ro.boot.serialno`  // ��ȡ�豸 ID ��
11. `adb shell getprop ro.build.version.release` // ��ȡ Android �汾��
12. `adb shell getprop ro.build.version.sdk`  // ��ȡ SDK �汾��
13. `adb shell dumpsys display | grep PhysicalDisplayInfo`  // ��ȡ�ֱ�������
14. `adb shell dumpsys battery`  // ��ȡ��������Ϣ
15. `adb shell dumpsys input | grep FocusedApplication`  // ��ȡ��ǰ����� package �� application
16. `adb shell am start -W component | grep TotalTime`  // ��ȡ component ������ʱ��
17. `adb shell settings get secure default_input_method`  // ��ȡĬ�����뷨  http://www.cnblogs.com/yajing-zh/p/5125317.html
18. `adb shell settings put secure default_input_method com.sohu.inputmethod.sogou/.SogouIME`  // ����Ĭ�ϵ����뷨
 

## 2. am �� pm

1. `am start -n {packageName}/.{activityName}`  // ���� app
2. `am kill <packageName>`   // ɱ��ָ�����Ľ���
3. `am force-stop <packageName>`  // ǿ��ֹͣ
4. `am startservice`   // ��������
5. `am stopservice`    // ֹͣ����
6. `am start -a android.intent.action.VIEW -d http://www.12306.com`  // ��12306 ��վ
7. `am start -a android.intent.action.CALL -d tel:10086`  // ���� 10086
8. `pm list packages`  // �г��ֻ������еİ���
9. `pm install/uninstall <packagename> `  // ��װ/ж��

## 3. ģ���û��¼�

1. **�ı�����**�� `adb shell input text <String>`  ���ֻ������`demo`�ַ�������Ӧָ�`adb shell input "demo"`.
2. **�����¼�**�� `input keyevent <KEYCODE>`  ��������ؼ�����Ӧָ� `input keyevent 4`.
3. **����¼�**�� `input tap <x> <y>` ��������꣨500��500������Ӧָ� `input tap 500 500`
4. **�����¼�**�� `input swipe <x1> <y1> <x2> <y2> <time>` ��������(300��500)������(100��500)����Ӧָ� `input swipe 300 500 100 500`.


## 4. logcat

1. `logcat | grep <str>`  // ��ʾ���� str ��logcat
2. `logcat | grep -i <str>`  // ��ʾ���� str ��logcat�������Դ�Сд
3. `logcat -s "ActivityManager"`  // ��ʾ�ñ�ǩ��log
4. `logcat -d`  // ��������log�󷵻أ�������һֱ�ȴ�
5. `logcat -c`  // ���log���˳�
6. `logcat -t <count>`    // ��ӡ��� count �е�log
7. `logcat -v <format>` ����ʽ����� log������ `format` �����¿�ѡֵ��
    * `brief` �� ��ʾ���ȼ�/��Ǻ�ԭʼ���̵�PID (Ĭ�ϸ�ʽ)
    * `process` �� ����ʾ����PID
    * `tag` �� ����ʾ���ȼ�/���
    * `thread` �� ����ʾ���̣��̺߳����ȼ�/���
    * `raw` �� ��ʾԭʼ����־��Ϣ��û��������Ԫ�����ֶ�
    * `time` �� ��ʾ���ڣ�����ʱ�䣬���ȼ�/��ǣ�PID
    * `long` ����ʾ���е�Ԫ�����ֶβ����ÿ��зָ���Ϣ����

