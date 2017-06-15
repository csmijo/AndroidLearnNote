# JMeter���ܲ�������ƪ�ʼ�

`JMeter`

---


## 1. JMeter �������

1. ʹ�� `Jmeter` ���� `B/S` �ܹ��Ĳ���
2. ������ `Https://jemter.apache.org`
3. `Jmeter` �������Ҫ�����������֣�
    * **ȡ����** �� ���нű��߼��Ŀ���
    * **�߳���** �� ��������
    * **������** �� ��ؽű������У�ȡ������ָ��

 
### 1.1 Jmeter �������

1. �߳����� �൱��Ҫģ����û���
2. Ramp-Up Period(in seconds): ��ѹ�Ĳ���
3. ѭ�������� �ű����еĴ���

**С��**����ʹ�� `Jmeter` ���̲߳����������ܲ���ʱ��������Ҫʹ�ö��ԣ���Ϊʵ��ʹ���з��ֶ��̹߳�������ʱ����ֶ��Բ�׼ȷ�����⡣

## 2. JMeter �ű�¼�Ʒ�ʽ�� badboby ���

### 2.1 JMeter �ű�������¼�Ʒ�ʽ

1.  ʹ�� `badbody` ����¼��
    
    `badboby` ��һ��ߣ������Խ��������������¼�ƣ�Ȼ�󵼳�Ϊ `JMeter`�ű�
    
2. ʹ�ô���ʽ����¼��

### 2.2 �ű�¼�Ƶ�������˼·

1. ҵ������
2. ¼�ƹ���
3. �ű�����
4. ���ܲ���

### 2.3 Badbody ����Ҳ��ʾ

������Ҫ�����ĸ����֣�

1. ������
2. ��ַ��
3. �ű���
4. ��ͼ��


## 3. JMeter ����¼�Ƽ�����

### 3.1 ����¼�ƵĲ���

1. HTTP ����Ĭ��ֵ
2. HTTP ���������
3. ���������

**һ��Ҫʹ�ú� `����ģʽ` �� `�ų�ģʽ`**


## 4. JMeter��ͼ�ν�������

### 4.1 �����нű�

* `../jmeter -n -t default_online.jmx -l result_1557.jtl`

* ָ��Զ��ѹ��������ѹ�����ԣ�
`../jmeter -n -t default_online.jmx -R 10.173.210.141 -l result_1557.jtl`

* һ������һ�߷�����־
`../jmeter -n -t baidu_requests_results.jmx -r -l baidu_requests_results.jtl -e -o /home/tester/apache-jmeter-3.0/resultReport`

* �����в�����
 
    * -n : ��GUI ģʽִ��JMeter
    * -t : ִ�в����ļ����ڵ�λ�ü��ļ���
    * -r : Զ�̽�����agent�������ڷֲ�ʽ���Գ����£����Ƿֲ�ʽ����ֻ�ǵ���Ͳ���Ҫ-r
    * -l : ָ�����ɲ��Խ���ı����ļ��� jtl �ļ���ʽ
    * -e : ���Խ��������ɲ��Ա���
    * -o : ָ�����Ա���Ĵ��λ��
    
        -o ָ�����ļ����ļ��У����벻���� ������ִ�л�ʧ�ܣ���Ӧ������������resultReport�ļ��б��벻���ڷ��򱨴�
 
### 4.2 jmeterѹ������������

1. `nohup ./jmeter-server &`  ��̨���� jmeter server ����
2. `ps -ef | grep jmeter` �鿴 jmeter ����


`jmeter -n -t weather.jmx -l test.jtl -JforcePerfmonFile=true`

`java -jar D:\program\apache-jmeter-3.1\lib\ext\CMDRunner.jar --tool Reporter --input-jtl test.jtl --plugin-type PerfMon --generate-png report-cpu.png`

### 4.3 ����ֵ��������

�޸� `jmeter\bin\jmeter.properties` �� `sampleresult.default.encoding` ���ԣ�Ĭ��ֵΪ `ISO-8859-1`���޸�Ϊ `utf-8` ���� 