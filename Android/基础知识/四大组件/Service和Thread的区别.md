#Service��Thread�Ĺ�ϵ

`Android` `Service` `Thread`

--

##1. Service��Thread�Ĺ�ϵ

### PartA

��������Android��ѧ�߶����ܻ����������ɻ�Service��Thread������ʲô��ϵ�أ�ʲôʱ��Ӧ����Service��ʲôʱ����Ӧ����Thread��

�����𰸿��ܻ��е�����Ծ�����Ϊ**Service��Thread֮��û���κι�ϵ**��

����֮�����в����˻��������ϵ��������Ҫ������Ϊ**Service�ĺ�̨����**��Thread���Ǵ�Ҷ�֪���������ڿ���һ�����̣߳�������ȥִ��һЩ��ʱ�����Ͳ����������̵߳����С���Service�����������ʱ���ܻ����������������һЩ��̨����ģ�һЩ�ȽϺ�ʱ�Ĳ���Ҳ���Է����������У���ͻ����˲��������ˡ����ǣ�����Ҹ�����**Service��ʵ�����������߳����**���㻹���������Thread��ʲô��ϵ��

��������ܻᾪ�����ⲻ�ǿӵ�ô��������ҪService���к����أ���ʵ��Ҳ�Ҫ�Ѻ�̨�����߳���ϵ��һ������ˣ�����������ȫ��ͬ�ĸ��

����**Android�ĺ�̨����ָ��������������ȫ������UI��**����ʹActivity�����٣����߳��򱻹رգ�**ֻҪ���̻��ڣ�Service�Ϳ��Լ�������**������˵һЩӦ�ó���ʼ����Ҫ�������֮��ʼ�ձ������������ӣ��Ϳ���ʹ��Service��ʵ�֡�������ֻ��ʣ�ǰ�治�Ǹո���֤��Service�����������߳����ô��������һֱִ�����������ӣ��ѵ��Ͳ����������̵߳������𣿵�Ȼ�ᣬ�������ǿ�����Service���ٴ���һ�����̣߳�Ȼ��������ȥ�����ʱ�߼���û�����ˡ�

�������Ȼ��Service��ҲҪ����һ�����̣߳���Ϊʲô��ֱ����Activity�ﴴ���أ�������Ϊ**Activity���Ѷ�Thread���п��ƣ���Activity������֮�󣬾�û���κ������İ취���������»�ȡ��֮ǰ���������̵߳�ʵ����������һ��Activity�д��������̣߳���һ��Activity�޷�������в���**������Service�Ͳ�ͬ�ˣ����е�Activity��������Service���й�����Ȼ����Ժܷ���ز������еķ�������ʹActivity�������ˣ�֮��ֻҪ������Service���������������ܹ���ȡ��ԭ�е�Service��Binder��ʵ������ˣ�ʹ��Service�������̨����Activity�Ϳ��Է��ĵ�finish����ȫ����Ҫ�����޷��Ժ�̨������п��Ƶ������

### PartB

���ߣ�rlei

���ӣ�https://www.zhihu.com/question/19591125/answer/15998566

��Դ��֪��

����Ȩ���������У�ת������ϵ���߻����Ȩ��


������Service��ͬ��thread��process��һ���ǳ���������⡣��Ҫ**ǿ����ǿ��**�ĵ�һ���ǣ�**Android��Service��һ��Context��������Ȼ����һ�������thread**�����������ϸ���ĵ�(Service | Android Developers)������ר��ǿ��
* **A Service is not a separate process**. The Service object itself does not imply it is running in its own process; unless otherwise specified, it runs in the same process as the application it is part of.
* **A Service is not a thread**. It is not a means itself to do work off of the main thread (to avoid Application Not Responding errors).

������Service��ʲô��**"A Service is an application component representing either an application's desire to perform a longer-running operation while not interacting with the user or to supply functionality for other applications to use."** 

����Serviceֻ�Ǵ��߼��ϱ�ʾһ������ִ��**"longer-running"**��"��̨"������ܵ�**"application component"**��

����Ϊʲôǿ��˵**"longer running"**��**"component"**? �ǳ����ԣ������Ǻ�Activity���ֻ�Ծ������Զ��ݵ�component�Աȶ��ԡ�һ���û��л�������Ӧ�ã���ǰActivity�ͱ���pause, stop������destroy�������ں�̨��������������Ҫǿ�����£��ϸ���˵����Ȼ������activity�ﴴ���Լ���worker thread��async task֮������̨�����飬��������û���κα��ϡ���**��Ϊһ�������е�activity�����л����˺�̨��ϵͳ��ʱ����kill�����process����ĺ�̨������ʱ����������Ϣ��������**

����ActivityΪʲô������ƣ�Windows����Ĵ�������С����ʱ����һ�����Դ�����Ϣ���߼�����������������һ�����⣬�����ش�Ҳ�ܼ򵥣������ƶ��豸���ڴ�/��ض����ޡ�

���������Ӧ�ö��ԣ�ͨ����manifest������Service������Ҫ��̨��Գ������е��߼�����Service�������������ı��ϣ�ֻҪϵͳ�ڴ治�Ǽ��˲����ã����Serviceһ�����ᱻkill������ϵͳ���ԣ�������һ����������Service�����У�������̾;��нϸߵ����ȼ��������ڴ治�㱻ɱ���������ŵñȽϿ���

��������ǰ�治��ǿ����Service��������process��thread��Ϊʲô��������˵ɱ����ʲô�ģ������ٴ�ǿ��������԰�Service����һ�ȴ��룬�����ں�̨��Щ���飬���˶��ѡ��������ȴ������������У���ȫ��ȡ�������Լ���ϲ�á����local service�����������worker thread����Ȼ�������Ӧ�ý��̵����̼߳�UI�߳������С�����㲻������UI�̣߳���ͽ�һ��worker thread������Щϸ�ڣ�Android framework������ôcare����ֻ֪����������һ��service��Ȼ�������manifest�����ҵ����service���������ĸ�process�����У���ô���process�Ͳ����ױ�kill��

����ʲôʱ��ѡ��local service������ָ������Ľ��̣���ʲôʱ��ѡ��remote service������Ľ��̣���**ͨ�����ǻ�������Ҫ�������е�service������IM֮�ࣩ���ڵ����Ľ�����**������UI���ڵĽ����ڱ�Ҫ��ʱ����Ȼ���Ա�ϵͳkill�����ڳ��ڴ档**��local serviceͨ����������һЩ��Ҫ�������е���Ȼ����activity����ڵ�����**������ȷ������Ͷ��Ż���š�����������ִ�����Ժ�service�Ϳ���stop�Լ�����Ȼ����������UI���̱����յ���

--
**[�ο�]**
* [ Android Service��ȫ���������ڷ���������֪����һ��(��)](http://blog.csdn.net/guolin_blog/article/details/11952435)
* [Android��Local Service��ʵ�������ʲô��](https://www.zhihu.com/question/19591125)