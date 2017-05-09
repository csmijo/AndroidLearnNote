# TraceView ѧϰ�ʼ�

`TraceView` `����`

---

## 1. TraceView ���

`TraceView` �� `Android` ƽ̨�䱸һ���ܺõ����ܷ����Ĺ��ߡ�����Ҫ���ڷ��� `Android` ��Ӧ�ó���� `hotspot`��������ͨ��ͼ�λ��ķ�ʽ�������˽�����Ҫ���ٵĳ�������ܣ������ܾ��嵽 `method`����ϸ���ݲο���[Profiling with Traceview and dmtracedump](https://developer.android.com/studio/profile/traceview.html)

## 2. TraceView ��ʹ��

ʹ�� `TraceView` ��Ҫ�����ַ�ʽ��

1. **û��Ŀ��Ӧ��Դ��������**������ʹ�� `DDMS`���������ݵĲɼ�������Ĳ��裺
    * ѡ����Ҫ�����Ľ���
    * ��� `DDMS`�����е� `Start Method Profiling` ��ť���Ⱥ�ɫ��С���ɺ�ɫ֮��ͱ�ʾ `TraceView` �Ѿ���ʼ�����ˡ�Ȼ��Ϳ��Խ���Ӧ�õĲ����ˣ�**������ò�Ҫ���� 5 �룬��Ϊ����ǽ���С��Χ�����ܲ���**��Ȼ���ٵ��һ�� `Stop Method Profiling` ��ť������������һ�����档

2. **����Դ��������**�� ��Դ����ʹ�� `android.os.Debug.startMethodTracing()` �͡�`android.os.Debug.stopMethodTracing()` ����������������������֮��Ĵ���ʱ�ͻ���һ�� `trace` �ļ��� `/sdcard` Ŀ¼�����ɡ�Ҳ����ͨ��`startMethodTracing(String traceName)` ���� `trace` �ļ����ļ�����������ͨ�� `adb pull /sdcard/xxx.trace  /tmp` ��� `trace` �ļ���ȡ�������У�Ȼ��ʹ�� `DDMS` ���߽��з�����

3. ʹ�� `DDMS` �ķ������÷�Χ���㣬����ʹ��`startMethodProfiling()` �ķ������Ӿ�ȷһЩ��

## 3. TraceView ����

![traceview����.PNG](http://on9czqsf5.bkt.clouddn.com/traceview����.PNG?2017-05-09-10-48-24)


���� `TraceView` ����ͼ��ʾ��������Ҫע��ĵط���ͼ��ʶ:

1. �����Ӧ�õĽ�����
2. `Start Method Profiling`,`Stop Method Profiling` ��ť
3. ���Խ�����ÿ���̵߳�ִ�������ÿ���߳�ռһ��
4. ʱ����
5. ��ʾ��ǰѡ�еķ���
6. ��ѡ��ĳ������֮��(���磺Handler.dispatchMessage())����ʾ���������ݣ�
    * `Parents` : ��ʾ���� `Handler.dispatchMessage()` �����ĸ����������Կ����������Ϊ 0
    * `Children` : ��ʾ `Handler.dispatchMessage()` �����ڲ����õ��������������Կ�������������������

7. `traceView` ��ָ������У���ϸ�г���ÿ�������� CPU ʹ��ʱ�䣬���ô����ȣ���Щ��Ϣ�ǲ��� `hotspot` �Ĺؼ���

    |����|����|
    |:--|:--|
    |Name|���߳����й����������õķ�����|
    |Incl Cpu Time|ĳ����ռ�õ� CPU ʱ�䣬**�����ڲ��������������� CPU ʱ��**|
    |Excl CPU Time|ĳ����ռ�õ� CPU ʱ�䣬**���ǲ�����**�ڲ��������������� CPU ʱ��|
    |Incl Real Time|ĳ�������е���ʵʱ��(�Ժ���Ϊ��λ)��**������������������ռ�õ���ʵʱ��**|
    |Excl Real Time|ĳ�������е���ʵʱ��(�Ժ���Ϊ��λ)��**���ǲ�����**��������������ռ�õ���ʵʱ��|
    |Call+RecurCalls/Total|ĳ���������ô����Լ��ݹ���õĴ���|
    |Cpu Time/Call|ĳ�������� CPU ʱ������ô����ıȣ�Ҳ���Ǹ÷���ƽ��ִ��ʱ��|
    |Real Time/Call|ĳ������ʵ��ƽ��ִ��ʱ��|

## 4. TraceView ʵս

�˽��� `TraceView` �Ľ�������ڽ���������� `TraceView` ������ `hotspot`��һ����ԣ�`hotspot` �����������͵ĺ�����

* һ���ǵ��ô������࣬��ÿ�ε���ȴ��Ҫ���Ѻܳ�ʱ��ĺ�����
* һ������Щ����ռ��ʱ�䲻����������ȴ�ǳ�Ƶ���ĺ�����

������Ҫʹ�� [Android application (performance and more) analysis tools - Tutorial](http://www.vogella.com/tutorials/AndroidTools/article.html) �ṩ��ʾ����������ϰ��

�ҵĽ�������������£�

1. ���� `Incl Cpu Time`���н�������
2. �� Top1 �ķ�����ʼ�����Ľ������� `Children` �������жϵı�׼�� ����÷�����`Incl Cpu Time`ռ���÷����İٷֱȡ�

   ������ͼ�� `Handler.dispatchMessage()` �� `Children` �У����� `Handler.handleCallback()` ����ռ���� 99.8% �ı�����������һ���ͽ��뵽 `Handler.handleCallback()` �������н�һ���ķ���
    
3. ����һ���ķ�����ֱ���ҵ����Ǽ�ص�Ӧ�õķ�����Ȼ������ϸ�鿴�÷����������ǿ�����������⡣

    ![traceviewʵս.PNG](http://on9czqsf5.bkt.clouddn.com/traceviewʵս.PNG?2017-05-09-11-27-58)
    
    ������ `demo` Ϊ����Ӧ�õİ���Ϊ `csmijo.com.traceviewdemo`�� һ������������ `csmijo/com/traceviewdemo/MyArrayAdapter.getView()`�����г������⣬���÷�����Ҫ�� `CPU` �������ڱ�ʶ�����������ĵ����У����Ծ���Ҫ����Ӧ�Ĵ��봦�鿴�������Ż���
    


�������Ҹ���ѧϰʹ�� `TraceView` �ľ��飬����ʵս���֣������ο���������κδ���ĵط������æָ����лл��



---
[�ο�����]

* [��ȷʹ��Android���ܷ������ߡ���TraceView](http://blog.jobbole.com/78995/)
* [Android ����µ� TraceView ��鼰�䰸��ʵս](http://www.cnblogs.com/sunzn/p/3192231.html)
* [Android application (performance and more) analysis tools - Tutorial](http://www.vogella.com/tutorials/AndroidTools/article.html)