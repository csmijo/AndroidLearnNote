# ��װ apk �� /system/app Ŀ¼��

`adb` `system`

---

�� Android �У����Ҫʹ��ϵͳ���Ƶ�Ȩ�ޣ����� `android.permission.WRITE_SECURE_SETTINGS`����������Ҫ�ѳ���װ�� `/system/app/` �¡�

������ `test.apk` Ϊ������ʾ���������**��Ҫ׼��һ̨�Ѿ���� `Root` Ȩ�޵��ֻ���**

1. ͨ�� USB �����ֻ��͵��ԡ�
2. ʹ�� adb �����ֻ���
3. ִ�����²�����

    ```
    $ adb push test.apk /sdcard/  // �ϴ�Ҫ��װ���ļ���Ϊ��װ��׼����
    $ adb shell
    $ su // �л��� root �û������û�л�� Root Ȩ�ޣ���һ������ɹ���
    # mount -o remount,rw -t yaffs2 /dev/block/mtdblock3 /system // �÷�����д��
    # cat /sdcard/test.apk > /system/app/test.apk // ��һ�������� cp ʵ�֣���һ���豸��û�а�����������ʹ�� mv ����ִ���failed on '/sdcard/NetWork.apk' - Cross-device link�� 
    # mount -o remount,ro -t yaffs2 /dev/block/mtdblock3 /system // ��ԭ�������ԣ�ֻ����
    # cd /system/app
    # chmod 777 test.apk  // ��test.apk���Ȩ��
    # exit
    $ exit
    ```
4. �� `/system/app` Ŀ¼���ҵ� `test.apk` ���ִ�а�װ

---
[�ο�����]

* [��װ apk �� /system/app Ŀ¼��](https://my.oschina.net/zengsai/blog/11195)