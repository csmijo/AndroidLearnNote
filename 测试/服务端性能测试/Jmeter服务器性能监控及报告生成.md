Jmeter ���������ܼ�ؼ���������

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
2. ��ѹ�ļ�����Ӧ���ļ��ֱ���� jmeter ��װĿ¼�Ķ�Ӧ�ļ����£���
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

### 3.2.3 ������ Plugin Type

#### 1. plugin-type ����

Most of class names are self-explanatory:

* `AggregateReport` = JMeter's native Aggregate Report, can be **saved only as CSV**
* `SynthesisReport` = mix between JMeter's native Summary Report and Aggregate Report, can be **saved only as CSV**
* `ThreadsStateOverTime` = Active Threads Over Time
* `BytesThroughputOverTime`
* `HitsPerSecond`
* `LatenciesOverTime`
* `PerfMon` = PerfMon Metrics Collector
* `DbMon` = DbMon Metrics Collector, DataBase, get performance counters via sql
* `JMXMon` = JMXMon Metrics Collector, Java Management Extensions counters
* `ResponseCodesPerSecond`
* `ResponseTimesDistribution`
* `ResponseTimesOverTime`
* `ResponseTimesPercentiles`
* `ThroughputVsThreads`
* `TimesVsThreads` = Response Times VS Threads
* `TransactionsPerSecond`
* `PageDataExtractorOverTime`
* `MergeResults` = MergeResults Command Line Merge Tool to simplify the comparison of two or more load tests, need properties file (like merge-results.properties)

## tmp

standard set
* AggregateReport
* SynthesisReport
* ThreadsStateOverTime
* PerfMon
* ResponseTimesOverTime
* TransactionsPerSecond

----

JMeterPlugins-Standard.jar��JMeterPlugins-Extras.jar

* BytesThroughputOverTime
* HitsPerSecond
* LatenciesOverTime
* ResponseCodesPerSecond
* ResponseTimesDistribution
* ResponseTimesPercentiles
* ThroughputVsThreads
* TimesVsThreads
 


#### 2. �������������

Ϊ��ʹ�� JMeterPluginCMD ���ɽ��ͼƬ�� csv �ļ�������Ҫ����һ�µ������

1. `jpgc-filterresults-2.1.zip`  https://jmeter-plugins.org/wiki/FilterResultsTool/
2. `jpgc-synthesis-2.1.zip`  https://jmeter-plugins.org/?search=jpgc-synthesis  
3. `GUI�����е� plugins manager �е� jpgc-Standard set`�����й��������µ��ļ���
    * jpgc-dummy
    * jpgc-fifo
    * jpgc-graphs-basic
    * jpgc-perfmon
    * jpgc-tst
    * jpgc-sense
    * jpgc-functions
    * jpgc-casutg
    * jpgc-ffw

## 4. ���ܼ���������С��

### 4.1 ServerAgent-2.2.1.zip

`ServerAgent-2.2.1`(������ʹ��): https://jmeter-plugins.org/wiki/PerfMonAgent/

### 4.2 jpgc-perfmon-2.1.zip

`jpgc-perfmon-2.1.zip`(����ʹ��): https://jmeter-plugins.org/wiki/PerfMon/#Concept

### 4.3 jpgc-cmd-2.1.zip

`jpgc-cmd-2.1.zip`: https://jmeter-plugins.org/wiki/JMeterPluginsCMD/ 

### 4.4 ����

1. `jpgc-filterresults-2.1.zip`  https://jmeter-plugins.org/wiki/FilterResultsTool/
2. `jpgc-synthesis-2.1.zip`  https://jmeter-plugins.org/?search=jpgc-synthesis  
3. `GUI�����е� plugins manager �е� jpgc-Standard set`�����й��������µ��ļ���
    * jpgc-dummy
    * jpgc-fifo
    * jpgc-graphs-basic
    * jpgc-perfmon
    * jpgc-tst
    * jpgc-sense
    * jpgc-functions
    * jpgc-casutg
    * jpgc-ffw


### 4.5 jar���б�

#### 4.5.1 lib

* `jmeter-plugins-cmn-jmeter-0.3.jar`
* `perfmon-2.2.2.jar` ------ jpgc-perfmon-2.1.zip
* `cmdrunner-2.0.jar` ------ jpgc-cmd-2.1.zip


#### 4.5.2 lib\ext

* `jmeter-plugins-manager-0.13.jar`
* `jmeter-plugins-perfmon-2.1.jar` ------ jpgc-perfmon-2.1.zip
* `jmeter-plugins-cmd-2.1.jar` ------ jpgc-cmd-2.1.zip
* `jmeter-plugins-filterresults-2.1.jar` ------ jpgc-filterresults-2.1.zip
* `jmeter-plugins-synthesis-2.1.jar` ------ jpgc-synthesis-2.1
* `jmeter-plugins-dummy-0.2.jar`
* `jmeter-plugins-fifo-0.2.jar`
* `jmeter-plugins-graphs-basic-2.0.jar`
* `jmeter-plugins-tst-2.0.jar`
* `jmeter-plugins-senseuploader-2.4.jar`
* `jmeter-plugins-functions-2.0.jar`
* `jmeter-plugins-casutg-2.1.jar`
* `jmeter-plugins-ffw-2.0.jar`

#### 4.5.3 bin

* `JMeterPluginsCMD.bat` ------ jpgc-cmd-2.1.zip
* `JMeterPluginsCMD.sh` ------ jpgc-cmd-2.1.zip
* `FilterResults.bat` ------ jpgc-filterresults-2.1.zip
* `FilterResults.sh` ------ jpgc-filterresults-2.1.zip

---

�ο����ף�
* [JMeterִ��ѹ�����HTMLͼ�λ���������](http://www.cnblogs.com/qmfsun/p/6382540.html)
* [PerfMon Server Agent](https://jmeter-plugins.org/wiki/PerfMonAgent/#PerfMon-Server-Agent)
* [Servers Performance Monitoring](https://jmeter-plugins.org/wiki/PerfMon/#Concept)
* [JMeterPluginsCMD Command Line Tool](https://jmeter-plugins.org/wiki/JMeterPluginsCMD/)
