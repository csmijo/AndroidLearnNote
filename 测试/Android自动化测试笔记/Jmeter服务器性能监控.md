Jmeter ���������ܼ��

`Jmeter`

---


`Jmeter�汾`��**apache-jmeter-3.2**

## 1. ǰ������--����Ĳ��

jmeterҲ������loadrunnerһ����ط�����CPU���ڴ�����ܲ�����������Ҫ��װһЩ�����

1. `jpgc-perfmon-2.1.zip`(����ʹ��): https://jmeter-plugins.org/wiki/PerfMon/#Concept
2. `ServerAgent-2.2.1`(������ʹ��): https://jmeter-plugins.org/wiki/PerfMonAgent/


## 2. GUI ��ط���������

### 2.1 ʹ�ò���

1. ������Ҫ�� **������** ͨ�� `startAgent.sh` ���� `startAgent.bat` ���� `PerfMon Server Agent`
2. ��ѹ `jpgc-perfmon-2.1.zip` �ļ���Ȼ�� `lib` �ļ��еģ�
    * `jmeter-plugins-cmn-jmeter-0.3.jar` ---> ���� `jmeter` ��װĿ¼�� `lib` Ŀ¼
    * `perfmon-2.2.2.jar` ---> ���� `jmeter` ��װĿ¼�� `lib` Ŀ¼
    * `ext\jmeter-plugins-manager-0.11.jar` ---> ���� `jmeter` ��װĿ¼�� `lib\ext` Ŀ¼
    * `ext\jmeter-plugins-perfmon-2.1.jar` ---> ���� `jmeter` ��װĿ¼�� `lib\ext` Ŀ¼
 

���������Ļ��������ú��ˣ����� `jmeter`�����Է���`jmeter GUI` ����� `ѡ��` �˵��������� `Plugins Manager` �˵��������߳���ļ������������� `jp@gc - PerfMon Metrics Collector` ��ѡ������Ϳ���Ϊ�߳���������ܼ����ķ���

ʹ��GUI����������ܼ�أ�����ͨ�����������Ҫ��صķ������� `Ip`��`�˿�`��`Metric` �ȡ�

### 3. NO GUI ��ط���������

ʹ�� GUI ��������Ķ�������ܣ�������û���ʹ�� NO GUI �������������ܼ�ء�

### 3.1 ʹ�ò���

1. ʹ�� GUI �����д�� xxx.jmx ���ܲ��Խű�����Ȼ�ڽű���Ҫָ����Ҫ��صķ������� IP���˿ڣ�Metric��
    
    **ע��**��������Ҫ�ڽű���ָ�����ܲ��Խ���ı����ļ����� cpu��memory�Ȳ��Խ���ı����ļ��������ȫ����������� log.jtl �ļ��С� ����ͼ��ʾ��
    ![](http://img.blog.csdn.net/20140730151453344?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY2xvdWRfbGw=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

2. ʹ����������ִ�в��Խű���

    ```
    jmeter -n -t xxx.jmx -l log.jtl -JforcePerfmonFile=true
    ```
3. ִ�н���֮�󣬽���ᱣ���� `log.jtl` �ļ��У�����ͨ�������������ɲ��Ա��棺

    ```
    jmeter -g log.jtl -e -o resultReport
    ```
    ע�⣺ �������ȷ�� resultReport �ļ��д��ڣ���Ȼ��ִ�д���
    
### 3.2 ���ģʽ��jtlת�ɲ���ͼ��

#### 3.2.1 GUI ��ʽ

�� GUI ���ڣ����� log.jtl �����������ܽ���������ٶȱȽ�����

### 3.2.2 �����ʽ

����ʹ�� JMeterPluginCMD �����ɶ�Ӧ��ͼƬ���� csv ͳ���ļ���

1. �ӹ������أ� `jpgc-cmd-2.1.zip`: https://jmeter-plugins.org/wiki/JMeterPluginsCMD/ 
2. ��ѹ�ļ�����Ӧ���ļ��ֱ���� jmeter ��װĿ¼�Ķ�Ӧ�ļ����£�����
    * `bin\JMeterPluginsCMD.bat` --> `jmeter\bin\JMeterPluginsCMD.bat`
    * `bin\JMeterPluginsCMD.sh`--> `jmeter\bin\JMeterPluginsCMD.bat`
    * `lib\cmdrunner-2.0.jar` --> `jmeter\lib\cmdrunner-2.0.jar`
    * `lib\jmeter-plugins-cmn-jmeter-0.3.jar` --> `jmeter\lib\jmeter-plugins-cmn-jmeter-0.3.jar`
    * `lib\ext\jmeter-plugins-cmd-2.1.jar` --> `jmeter\lib\ext\jmeter-plugins-cmd-2.1.jar`
    * `lib\ext\jmeter-plugins-manager-0.11.jar` --> `jmeter\lib\ext\jmeter-plugins-manager-0.11.jar`

* Ȼ��Ϳ���ʹ�� JMeterPluginsCMD.bat/sh ����ͼƬ�� CSV �ļ��ˡ����磬��������ͼƬ���ļ�������Ϊ��

    ```
    # ����ͼƬ
    JMeterPluginsCMD.bat --generate-png cpu.png --input-jtl cpu.jtl --plugin-type PerfMon
    
    # ���� CSV �ļ�
     JMeterPluginsCMD.bat --generate-csv cpu.csv --input-jtl cpu.jtl --plugin-type PerfMon
    ```

---

�ο����ף�
* [JMeterִ��ѹ�����HTMLͼ�λ���������](http://www.cnblogs.com/qmfsun/p/6382540.html)
* [PerfMon Server Agent](https://jmeter-plugins.org/wiki/PerfMonAgent/#PerfMon-Server-Agent)
* [Servers Performance Monitoring](https://jmeter-plugins.org/wiki/PerfMon/#Concept)
* [JMeterPluginsCMD Command Line Tool](https://jmeter-plugins.org/wiki/JMeterPluginsCMD/)
