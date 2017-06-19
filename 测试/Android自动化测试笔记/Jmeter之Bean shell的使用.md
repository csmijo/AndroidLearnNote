# Jmeter֮Bean shell��ʹ��

`Jmeter` `Bean shell`

--

�����ѧϰʹ�� Jmeter �����нӿڲ��ԣ�ʹ�� Jmeter �ṩ�Ļ��������޷���ɲ�������������Ҫ��дһЩ Bean shell �ű������潫�� Bean shell��һЩʹ�÷������м򵥵Ľ��ܡ�

## 1. ʲô�� Bean shell

`Bean shell`������http://www.BeanShell.org/

* `BeanShell` ��һ����ȫ����Java�﷨�淶�Ľű�����,������ӵ���Լ���һЩ�﷨�ͷ���;
* `BeanShell` ��һ����ɢ���͵Ľű�����(����JS����);
* `BeanShell` **����Javaд�ɵ�**,һ��С�͵ġ���ѵġ��������صġ�Ƕ��ʽ��JavaԴ���������,���ж���ű���������,�ǳ�����Ľ�����jar�ļ���СΪ175k��
* `BeanShell` **ִ�б�׼Java���ͱ��ʽ**,�������һЩ�ű�������﷨��

## 2. Jmeter ����Щ Bean shell

* ��ʱ����`BeanShell Timer`
* ǰ�ô�������`BeanShell PreProcessor`
* ��������`BeanShell Sampler`
* ���ô�������`BeanShell PostProcessor`
* ���ԣ�`BeanShell����`
* ��������`BeanShell Listener`

## 3. Bean shell���Ã��ñ���

JMeter������BeanShell�������˱������û�����ͨ����Щ������JMeter���н�����������Ҫ�ı�������ʹ�÷�������:

* `log`��д����Ϣ��jmeber.log�ļ���ʹ�÷�����`log.info(��This is log info!��);`
* `ctx`���ñ��������˵�ǰ�̵߳�������
* `vars - (JMeterVariables)`������ `jmeter` �������������ʵ��������JMeter�߳��еľֲ�������������������Map�������ǲ���������BeanShell���������������÷�����
    * a) vars.get(String key)����jmeter�л�ñ���ֵ
    * b) vars.put(String key��String value)�����ݴ浽jmeter������
* `props - (JMeterProperties - class java.util.Properties)`������jmeter���ԣ��ñ���������JMeter��������Ϣ�����Ի�ȡJmeter�����ԣ�����ʹ�÷�����vars���ƣ�����**ֻ��put��ȥString���͵�ֵ����������һ������**����Ӧ��java.util.Properties�� 
��������
    * a) props.get("START.HMS");����ע��START.HMSΪ�����������ļ�jmeter.properties�ж��� 
    * b) props.put("PROP1","1234"); 
* `prev - (SampleResult)`����ȡǰ���sample���ص���Ϣ�����÷�����
    * a) getResponseDataAsString()����ȡ��Ӧ��Ϣ
    * b) getResponseCode() ����ȡ��Ӧcode
             
## 3. Bean shell ���÷�

### 3.1 ��������

���������������Ĳ�������

�� http �ӿ�xx ����ѹ�����ԣ���Ҫ����ʱ������ uid ģ���û����ʣ�Ȼ������ӿڷ��ص� Json �����еõ� vid ֵ����Ϊ��һ��ʹ�ã��жϸô����󷵻ص��б��鳤�ȼ���Ӧ���Ƿ����Ҫ��

### 3.2 ��������

1. �����߳���
2. ���� http sampler
3. ���� BeanShell PreProcessor ������� uid
    ���Դ��� BeanShell PreProcessor��Ȼ���д������ɷ���������������ɵ�ָ���Լ���Ҫ�Ĺ��򡣱�����ͼ��ʹ��"test_ + ��ǰʱ�� + �����" �Ĺ�������αuid��
    
    ����ʹ�� `log.info()` ������е��ԣ��������·��� log �н��в鿴��
    
    ����ʹ�� `vars.put()` ������������ŵ� jmeter �ı����У�Ȼ��Ϳ����� http ������ͨ�� `${uid}` �ķ�ʽ����ʹ���ˡ�
    

    ![2017-06-19_202106.PNG](http://on9czqsf5.bkt.clouddn.com/2017-06-19_202106.PNG?2017-06-19-20-29-08)

4. ���� BeanShell PostProcessor 
    �������ص� json��������ʹ�õ������� fastjson.jar �����н�����ֻ��Ҫ�� `fastjson.jar` �ŵ� jmter ��װĿ¼�� `lib\ext` �ļ����¼���ʹ�á�
    
    ![2017-06-19_202520.PNG](http://on9czqsf5.bkt.clouddn.com/2017-06-19_202520.PNG?2017-06-19-20-29-17)

5. ���� Beanshell����
    ![2017-06-19_202722.PNG](http://on9czqsf5.bkt.clouddn.com/2017-06-19_202722.PNG?2017-06-19-20-29-30)




--

[�ο�����]
* [Jmeter֮Bean shellʹ��(һ)](http://www.cnblogs.com/puresoul/p/4915350.html)
* [Jmeter֮Bean shellʹ��(��)](http://www.cnblogs.com/puresoul/p/4949889.html)
* [[����]Jmeter-BeanShell��ʹ�ý���](http://www.jianshu.com/p/bc537d6acb3a)
* [ Jmeter BeanShell PostProcessor��ȡjson����](http://blog.csdn.net/silencemylove/article/details/51373873)