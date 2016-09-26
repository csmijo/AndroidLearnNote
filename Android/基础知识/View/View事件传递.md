#View�¼�����

`Android` `View` `�ʼ�`

--

##1. ����֪ʶ

(1) ���� `Touch`�¼�������װ�� `MotionEvent` ���󣬰��� Touch��λ�á�ʱ�䡢��ʷ��¼�Լ��ڼ�����ָ(��ָ����)�ȡ�

(2) �¼����ͷ�Ϊ: `ACTION_DOWN`,`ACTION_UP`,`ACTION_MOVE`,`ACTION_POINTER_DOWN`,`ACTION_POINTER_UP`,`ACTION_CANCEL`��ÿ���¼�������`ACTION_DOWN`��ʼ��`ACTION_UP`�����ġ�
(3) ���¼��Ĵ���������ࣺ
* ���ݡ���`dispatchTouchEvent()`
* ���ء���`onInterceptTouchEvent()`
* ���ѡ���`onTouchEvent()`��`onTouchListener()`

##2. ��������
(1) �¼���`Activity.dispatchTouchEvent()`��ʼ���ݣ�ֻҪû�б�ֹͣ�������أ������ϲ��View/ViewGroup��ʼһֱ����(��View)���ݡ���View����ͨ��`onTouchEvent()`���¼����д���

(2) �¼��Ӹ�View/ViewGroup ���ݸ���View�� ViewGroupͨ�� `onInterceptTouchEvent()`���¼������أ�ֹͣ�����´��ݡ�**`onInterceptTouchEvent()`ֻ������ViewGroup��**����ͨ��View��û�����������

(3) ����¼��������´��ݹ�����һֱû��ֹͣ������ײ���Viewû�����Ѹ��¼������¼��ͻᷴ�����ϴ��ݣ���ʱ��View/ViewGroup���Խ������ѣ�������Ǹ��¼�����û�б����ѵĻ������ᵽActivity��`onTouchEvent()`����

(4) ���Viewû�ж� `ACTION_DOWN`�������ѣ�**֮��������¼����ᴫ�ݹ���**��

(5) `onTouchListener()`������ `onTouchEvent()`���¼��������ѡ�

##3. �����¼�
![view-dispatchTouch.png](pic/view-dispatchTouch.png "")

**˵����**

����ViewGroup A���� ���View��ViewGroup�����оͰ�����ViewGroup B��ViewGroup BҲ�������View ��ViewGroup�����оͰ�����View C��View C��һ����ͨ��View��

�������ڼ����û����ȴ���������Ļ�ϵĵ���C�ϵ�ĳ���㣬�õ㱻���Ϊ�����㣨`touch point`����DOWN�¼����ڸõ������Ȼ���û��ƶ���ָ������뿪��Ļ���˹�������ָ�Ƿ��뿪C�������޹ؽ�Ҫ���ؼ������ƣ�gesture���Ǵ����￪ʼ�ġ�

�������ڼ���ViewGroup Bû������ `DOWN`�¼��������������� `MOVE`�¼���ԭ�������ViewGroup B��һ��scrolling view�����û����������������ڵ����tap��ʱ�����������Ԫ��Ӧ���ܴ���õ���¼������ǵ��û���ָ�ƶ���һ���ľ���󣬾Ͳ������Ӹ����ƣ�gesture��Ϊ����ˡ��������ԣ��û�����scroll�������ΪʲôBҪ�ӹܸ����ƣ�gesture����

**�������¼��������˳��**

1. `DOWN` �¼������δ��� A �� B�� `onInterceptTouchEvent()`���������Ƕ����� false�� ��Ϊ����Ŀǰ���������ء�
2. `DOWN`�¼����ݵ�C��onTouchEvent������������true��
3. �ں�������`MOVE`�¼�ʱ��A ��`onInterceptTouchEvent()`������Ȼ����false��
4. B ��`onInterceptTouchEvent()`�����յ��˸� `MOVE` �¼�����ʱB ע�⵽�û���ָ�ƶ������Ѿ�������һ����threshold�����߳�Ϊslop������ˣ�B��`onInterceptTouchEventz()` ������������true���Ӷ�**�ӹܸ����ƣ�gesture�������Ĵ���**��
5. Ȼ����� `MOVE` �¼����ᱻϵͳ���һ�� `CANCEL`�¼������`CANCEL`�¼����ᴫ�ݸ�C ��`onTouchEvent()`������
6. ���ڣ�������һ��`MOVE �¼����������ݸ�A�� `onInterceptTouchEvent()`������A���ǲ����ĸ��¼������`onInterceptTouchEvent()`������������false��
7. ��ʱ���� `MOVE`�¼��������ٴ��ݸ�B ��`onInterceptTouchEvent()`�������÷���**һ������һ��`true`������Ҳ���ᱻ������**����ʵ�ϣ���MOVE�Լ�������ʣ�ಿ�֡��������ݸ�**B�� `onTouchEvent()` ����**������A�������ء�����ʣ�ಿ�֡�����
8. C **��Ҳ����**�յ������ƣ�gesture���������κ��¼��ˡ�

**�ܽ᣺**
* ���һ��`ViewGroup` ������**�����`DOWN`**�¼������¼�**��Ȼ��**���ݵ���ViewGroup��`onTouchEvent()`�����С�
* ��һ���棬���ViewGroup������һ��**��·���¼�**�����磬MOVE��������¼����ᱻϵͳ���һ�� `CANCEL` �¼��������ݸ�֮ǰ��������ƣ�gesture������View������**�����ٴ���**�������Ǳ����ص�MOVE����ϵͳ���ɵ�CANCEL���� ViewGroup��`onTouchEvent()`������ֻ���ٵ������¼��Żᴫ�ݵ�ViewGroup��`onTouchEvent()`�����С�
* ���������ӷ��һ�㣬����������Լ���ViewGroup��ֱ�Ӹ�д `dispatchTouchEvent()`���������Դ��ݽ������¼����κ��������Ĵ����������Ļ���**���ܻ��ƻ�һЩԼ��������Ӧ��С�ġ�**

--
���ο���
* [����������֮ View �¼�����](http://b.codekk.com/blogs/detail/54cfab086c4761e5001b253e)
* [�����ǽ���Android�¼��ַ���õ�����](http://www.jianshu.com/p/2be492c1df96)