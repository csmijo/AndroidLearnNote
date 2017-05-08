# TraceView ѧϰ�ʼ�

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


---
[�ο�����]

* [��ȷʹ��Android���ܷ������ߡ���TraceView](http://blog.jobbole.com/78995/)
* [Android ����µ� TraceView ��鼰�䰸��ʵս](http://www.cnblogs.com/sunzn/p/3192231.html)
* [Android application (performance and more) analysis tools - Tutorial](http://www.vogella.com/tutorials/AndroidTools/article.html)