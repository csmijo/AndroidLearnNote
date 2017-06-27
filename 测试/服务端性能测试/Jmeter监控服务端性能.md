# Jmeter��ط��������

`Jmeter`

---

����ʹ�õ� `Jmeter` �汾Ϊ `apache-jmeter-3.2`��

## 1. ǰ������--����Ĳ��

`jmeter` Ҳ������ `loadrunner` һ����ط�����CPU���ڴ�����ܲ�����������Ҫ��װһЩ�����

1. `jpgc-perfmon-2.1.zip`(����ʹ��): https://jmeter-plugins.org/wiki/PerfMon/#Concept
2. `ServerAgent-2.2.1.zip`(������ʹ��): https://jmeter-plugins.org/wiki/PerfMonAgent/

## 2. GUI ��ط���������

### 2.1 ʹ�ò���

1. ������Ҫ�� **������** ��ѹ `ServerAgent-2.2.1.zip`, Ȼ��ͨ�� `startAgent.sh` ���� `startAgent.bat` ���� `PerfMon Server Agent`
2. ��ѹ `jpgc-perfmon-2.1.zip` �ļ���Ȼ�󽫶�Ӧ�ļ����µ� `jar`���ŵ� `jemter`��װĿ¼��Ӧ���ļ����¡����罫 `jpgc-perfmon-2.1\lib` �µ����� `jar` �ŵ�`jemter`��װĿ¼�� `lib`Ŀ¼�¡�


���������Ļ��������ú��ˣ����� `jmeter`�����Է���`jmeter GUI` ����� `ѡ��` �˵��������� `Plugins Manager` �˵��������߳���ļ������������� `jp@gc - PerfMon Metrics Collector` ��ѡ������Ϳ���Ϊ�߳���������ܼ����ķ���

ʹ�� `GUI` ����������ܼ�أ�����ͨ�����������Ҫ��صķ������� `Ip`��`�˿�`��`Metric` �ȡ�

### 3. NO GUI ��ط���������

ʹ�� `GUI` ��������Ķ�������ܣ�������û���ʹ�� `NO GUI` �������������ܼ�ء�

### 3.1 ʹ�ò���

1. ʹ�� `GUI` �����д�� `xxx.jmx` ���ܲ��Խű�����Ȼ�ڽű���Ҫָ����Ҫ��صķ������� `IP`��`�˿�`��`Metric`�ȡ�
    
    **ע��**��������Ҫ�ڽű���ָ�����ܲ��Խ���ı����ļ����� `cpu`��`memory`�Ȳ��Խ���ı����ļ��������ȫ����������ָ���� `log.jtl` �ļ��С� ����ͼ��ʾ��
    ![](http://img.blog.csdn.net/20140730151453344?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY2xvdWRfbGw=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

2. ʹ����������ִ�в��Խű���

    ```
    jmeter -n -t xxx.jmx -l log.jtl -JforcePerfmonFile=true
    ```
3. ִ�н���֮�󣬽���ᱣ���� `log.jtl` �ļ��У����ܲ��Խ�������� `result.jtl` �У� �� `GUI` �����е��� `result.jtl` �м��ɲ鿴�����ԵĽ��������ͼ��ʾ��
![2017-06-26_115857.PNG](http://on9czqsf5.bkt.clouddn.com/2017-06-26_115857.PNG?2017-06-26-11-59-47)

---
[�ο�����]
* [PerfMon Server Agent](https://jmeter-plugins.org/wiki/PerfMonAgent/#PerfMon-Server-Agent)
* [Servers Performance Monitoring](https://jmeter-plugins.org/wiki/PerfMon/#Concept)