# Jmeter���Ա�������

`Jmeter` `report`

---

����ʹ�õ� `Jmeter` �汾Ϊ `apache-jmeter-3.2`��

## 1. ������ģʽ�� jtl �ļ�ת�ɲ���ͼ�� 

**ע�⣺** ���ַ�ʽֻ������ `jmeter3.0` �Ժ�İ汾

### 1.1 �ڲ��ԵĹ����н� jtl ת���ɲ��Ա���

����ִ���������
```
jmeter -n -t test_request.jmx -l test_result.jtl -e -o /home/csmijo/resultReport
```

����˵����
  * `-n` : ��GUI ģʽִ��JMeter
  * `-t` : ִ�в����ļ����ڵ�λ�ü��ļ���
  * `-r` : Զ�̽�����agent�������ڷֲ�ʽ���Գ����£����Ƿֲ�ʽ����ֻ�ǵ���Ͳ���Ҫ-r
  * `-l` : ָ�����ɲ��Խ���ı����ļ��� jtl �ļ���ʽ
  * `-e` : ���Խ��������ɲ��Ա���
  * `-o` : ָ�����Ա���Ĵ��λ��
      * **-o ָ�����ļ����ļ��У����벻����**������ִ�л�ʧ�ܣ���Ӧ������������ `resultReport` �ļ��б��벻���ڷ��򱨴�**������ڣ����ļ��б���Ϊ��**

�����ļ���������ͼ��ʾ��

![2017-06-26_165038.PNG](http://on9czqsf5.bkt.clouddn.com/2017-06-26_165038.PNG?2017-06-26-16-51-13)


### 1.2 ʹ��֮ǰ�Ĳ��Խ�������ɲ��Ա���

�����ִ��ѹ��ű���ʱ��û��ָ�����ɲ��Ա��棬�ڲ��Խ���֮��Ҳ����ͨ�����µ��������ɣ�
```
jmeter -g log.jtl -e -o resultReport
```

����˵��:

* `-g` : ָ���Ѵ��ڵĲ��Խ���ļ�
* `-e` �����Խ�������ɲ��Ա���
* `-o` : ָ�����Ա���Ĵ��λ��
    * **-o ָ�����ļ����ļ��У����벻����** ������ִ�л�ʧ��

Ч������ͼ

## 2. ���ģʽ�� jtl ת�ɲ���ͼ��

## 2.1 ͼ�� plugin ������

1. `AggregateReport` = JMeter's native Aggregate Report, can be **saved only as CSV**
2. `SynthesisReport` = mix between JMeter's native Summary Report and Aggregate Report, can be **saved only as CSV**
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


## 2.2 ��ͬ plugin ���͵����ɷ�ʽ

### 2.2.1 ��Ҫ plugin ����

����ʹ�� `JMeterPluginCMD` �����ɶ�Ӧ��ͼƬ���� csv ͳ���ļ���

1. �ӹ������أ� `jpgc-cmd-2.1.zip`: https://jmeter-plugins.org/wiki/JMeterPluginsCMD/ 
2. ��ѹ�ļ�����Ӧ���ļ��ֱ���� `jmeter` ��װĿ¼�Ķ�Ӧ�ļ����£�����ѹ�� `bin` Ŀ¼�µ��ļ������뵽 `jmeter` ��װĿ¼�� `bin` Ŀ¼�£��Դ����ơ�
3. Ϊ��ʹ�� `JMeterPluginCMD` ���ɽ��ͼƬ�� csv �ļ�������Ҫ����һ�µ������
    1. `jpgc-filterresults-2.1.zip`  https://jmeter-plugins.org/wiki/FilterResultsTool/
    2. `jpgc-synthesis-2.1.zip`  https://jmeter-plugins.org/?search=jpgc-synthesis  
    3. `GUI` �����е� [plugins manager](https://jmeter-plugins.org/install/Install/) �е� `jpgc-Standard set`�����й��������µ��ļ���
        * jpgc-dummy
        * jpgc-fifo
        * jpgc-graphs-basic
        * jpgc-perfmon
        * jpgc-tst
        * jpgc-sense
        * jpgc-functions
        * jpgc-casutg
        * jpgc-ffw        
![jpgc-Standard-Set.PNG](http://on9czqsf5.bkt.clouddn.com/jpgc-Standard-Set.PNG?2017-06-26-18-46-44)

        
   
4. Ȼ��Ϳ���ʹ�� `JMeterPluginsCMD.bat/sh` ����ͼƬ�� CSV �ļ��ˡ����磬�������ܲ��Խ��ͼƬ�� CSV �ļ�������Ϊ��

    ```
    # ����ͼƬ
    JMeterPluginsCMD.bat --generate-png cpu.png --input-jtl cpu.jtl --plugin-type PerfMon
    
    # ���� CSV �ļ�
     JMeterPluginsCMD.bat --generate-csv cpu.csv --input-jtl cpu.jtl --plugin-type PerfMon
    ```
    
5. ������������ļ��Ϳ����������� `plugin` ���͵�ͼ��
    1. AggregateReport
    2. SynthesisReport
    3. ThreadsStateOverTime
    4. PerfMon
    5. ResponseTimesOverTime
    6. TransactionsPerSecond

### 2.2.2 �������͵� plugin

���Ҫ�������� `plugin` ���͵�ͼ��

1. BytesThroughputOverTime
2. HitsPerSecond
3. LatenciesOverTime
4. ResponseCodesPerSecond
5. ResponseTimesDistribution
6. ResponseTimesPercentiles
7. ThroughputVsThreads
8. TimesVsThreads

�ͻ���Ҫ������µ� `jar` ���� `jmeter` ��װĿ¼�� `lib\ext`�£�

* `JMeterPlugins-Standard.jar`  https://jmeter-plugins.org/downloads/old/
* `JMeterPlugins-Extras.jar`  https://jmeter-plugins.org/downloads/old/

### 2.2.3 �������� plugin ���͵�����

��Ӻ�����������ļ��󣬾Ϳ���ʹ�����µĽű���������ͼ���ˡ�
```
source /etc/profile
file="./csv/test"
jtlfile="test.jtl"
JMeterPluginsCMD.sh --generate-csv $file"_AggregateReport.csv" --input-jtl  $jtlfile  --plugin-type AggregateReport
JMeterPluginsCMD.sh --generate-csv $file"_SynthesisReport.csv" --input-jtl  $jtlfile  --plugin-type SynthesisReport
JMeterPluginsCMD.sh --generate-csv $file"_ThreadsStateOverTime.csv" --input-jtl  $jtlfile  --plugin-type ThreadsStateOverTime
JMeterPluginsCMD.sh --generate-csv $file"_BytesThroughputOverTime.csv" --input-jtl  $jtlfile  --plugin-type BytesThroughputOverTime
JMeterPluginsCMD.sh --generate-csv $file"_HitsPerSecond.csv" --input-jtl  $jtlfile --plugin-type HitsPerSecond
JMeterPluginsCMD.sh --generate-csv $file"_LatenciesOverTime.csv" --input-jtl  $jtlfile  --plugin-type LatenciesOverTime
JMeterPluginsCMD.sh --generate-csv $file"_ResponseCodesPerSecond.csv" --input-jtl  $jtlfile  --plugin-type ResponseCodesPerSecond
JMeterPluginsCMD.sh --generate-csv $file"_ResponseTimesDistribution.csv" --input-jtl  $jtlfile  --plugin-type ResponseTimesDistribution
JMeterPluginsCMD.sh --generate-csv $file"_ResponseTimesOverTime.csv" --input-jtl  $jtlfile  --plugin-type ResponseTimesOverTime
JMeterPluginsCMD.sh --generate-csv $file"_ResponseTimesPercentiles.csv" --input-jtl  $jtlfile  --plugin-type ResponseTimesPercentiles
JMeterPluginsCMD.sh --generate-csv $file"_ThroughputVsThreads.csv" --input-jtl  $jtlfile  --plugin-type ThroughputVsThreads
JMeterPluginsCMD.sh --generate-csv $file"_TimesVsThreads.csv" --input-jtl  $jtlfile  --plugin-type TimesVsThreads
JMeterPluginsCMD.sh --generate-csv $file"_TransactionsPerSecond.csv" --input-jtl  $jtlfile  --plugin-type TransactionsPerSecond
```


---

[�ο�����]

* [JMeterPluginsCMD Command Line Tool](https://jmeter-plugins.org/wiki/JMeterPluginsCMD/)
* [JMeterִ��ѹ�����HTMLͼ�λ���������](http://www.cnblogs.com/qmfsun/p/6382540.html)
* [jmeter֮jtl�ļ�����](http://www.cnblogs.com/miaomiaokaixin/p/6118081.html)
* [JMeter Plugins Manager](https://jmeter-plugins.org/wiki/PluginsManager/)