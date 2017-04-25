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


##4. ͼ�� Android �¼��ַ�����

###1. Android �¼��ַ���

 ![Android �¼��ַ���](pic/Android �¼��ַ���.png "")
 
ע�⣺

1. ��ϸ���Ļ���ͼ��Ϊ3�㣬��������������Activity��ViewGroup��View
2. �¼������Ͻ��Ǹ���ɫ��ͷ��ʼ����Activity��dispatchTouchEvent���ַ�
3. ��ͷ�������ִ���������ֵ����return true��return false��return super.xxxxx(),super ����˼�ǵ��ø���ʵ�֡�
4. dispatchTouchEvent�� onTouchEvent�Ŀ����и���true��->���ѡ����֣���ʾ����˼�������������true����ô�����¼��ʹ����ѣ������������ĵط����ˣ��¼���ֹ��
5. Activity ��dispatchTouchEvent ���۷���ʲô���������ViewGroup ��dispatchTouchEvent�����п�Դ�룩


###2. ��ϸ����

1. **����¼������жϣ������¼�������һ����U��ͼ**

    �����������û�жԿؼ�����ķ���������д����ķ���ֵ����ֱ����super���ø����Ĭ��ʵ�֣���ô�����¼�����Ӧ���Ǵ�Activity��->ViewGroup��>View �������µ���dispatchTouchEvent������һֱ��Ҷ�ӽڵ㣨View����ʱ������View��>ViewGroup��>Activity�������ϵ���onTouchEvent������
    
2. **dispatchTouchEvent �� onTouchEvent һ��return true,�¼���ֹͣ�����ˣ������յ㣩��û��˭�����յ�����¼�����**

    ��Android�¼��ַ����е�ͼƬ��ʾ��ֻҪ return true���ͱ�ʾ�¼���û�����¼��������ˡ�
    
    �����ʡ���dispatchTouchEvent return true ��ʱ���øò�ؼ��� onTouchEvent() ����������¼�������
    
    ���ش𡿣�dispatchTouchEvent return true ֻ����ֹ���ݣ�����鿴�������6 ������
    
3. **dispatchTouchEvent �� onTouchEvent return false��ʱ���¼����ش������ؼ���onTouchEvent����**
    * **����dispatchTouchEvent ���� false �ĺ���Ӧ����**���¼�ֹͣ����View���ݺͷַ�ͬʱ��ʼ�����ؼ����ݣ����ؼ���onTouchEvent��ʼ�������ϻش�ֱ��ĳ��onTouchEvent return true�����¼��ַ����ƾ���ݹ飬return false ��������ǵݹ�ֹͣȻ��ʼ���ݡ�
    * **����onTouchEvent return false �ͱȽϼ���**������������������¼��������¼����������ؼ��ķ����������������
    

4. **dispatchTouchEvent��onTouchEvent��onInterceptTouchEvent**

    ViewGroup ��View����Щ������Ĭ��ʵ�־��ǻ��������¼���װU���������꣬���� return super.xxxxxx() �ͻ����¼�����U�͵ķ�����������������¼�����·�������м䲻���κθĶ��������ݡ�����ֹ��ÿ�����ڶ��ߵ���
    
5. **onInterceptTouchEvent ������**

    Intercept ����˼�����أ�ÿ��ViewGroupÿ�������ַ���ʱ����һ��������Ҫ��Ҫ���أ�Ҳ���������Լ�����¼�Ҫ��Ҫ�Լ����������Ҫ�Լ������Ǿ���onInterceptTouchEvent������ return true�ͻύ���Լ���onTouchEvent�Ĵ�����������ؾ��Ǽ������ӿؼ����´���Ĭ���ǲ���ȥ���صģ���Ϊ��ViewҲ��Ҫ����¼�������onInterceptTouchEvent������return super.onInterceptTouchEvent()��return false��һ���ģ��ǲ������صģ��¼����������View��dispatchTouchEvent���ݡ�
    
6. **ViewGroup ��View ��dispatchTouchEvent��������super.dispatchTouchEvent()��ʱ���¼�������**

    ���ȿ���**ViewGroup ��dispatchTouchEvent**��֮ǰ˵��return true���սᴫ�ݡ�return false �ǻ��ݵ���View��onTouchEvent��Ȼ��ViewGroup����ͨ��dispatchTouchEvent�����ܰ��¼��ַ����Լ���onTouchEvent�����أ�return true��false �����У���ôֻ��ͨ��Interceptor���¼������������Լ���onTouchEvent������ViewGroup dispatchTouchEvent������superĬ��ʵ�־���ȥ����onInterceptTouchEvent����ס��һ�㡣
    
    ��ô����**View��dispatchTouchEvent** return super.dispatchTouchEvent()��ʱ�����¼��ᴫ�������أ����ź�Viewû��������������ͬ���ĵ���return true���սᡣreturn false �ǻ��ݻḸ���onTouchEvent���������¼��ַ����Լ���onTouchEvent �����أ���ֻ��return super.dispatchTouchEvent,View���dispatchTouchEvent��������Ĭ��ʵ�־����ܰ������View�Լ���onTouchEvent�����ġ�
    
7. **С�᣺**
    * ���� dispatchTouchEvent��onTouchEvent��return true���ս��¼����ݡ�return false �ǻ��ݵ���View��onTouchEvent������
    * ViewGroup ����Լ��ַ����Լ���onTouchEvent����Ҫ������onInterceptTouchEvent����return true ���¼�����������
    * ViewGroup ��������onInterceptTouchEvent Ĭ���ǲ����صģ�����return super.onInterceptTouchEvent()=return false��
    * View û����������Ϊ����View���԰��¼��ַ����Լ���onTouchEvent��View��dispatchTouchEventĬ��ʵ�֣�super�����ǰ��¼��ַ����Լ���onTouchEvent��

###3. ACTION_DOWN �¼������ܽ�


1. **ViewGroup��View ��dispatchTouchEvent �����¼��ַ�����ô����¼����ַܷ���ȥ���ĸ�Ŀ��**

    ע������> ��������¼�Ŀ����Ҫ��ô����
    1. �Լ����ѣ��սᴫ�ݡ�����->return true ��
    2. ���Լ���onTouchEvent������-> ����super.dispatchTouchEvent()ϵͳĬ�ϻ�ȥ���� onInterceptTouchEvent����onInterceptTouchEvent return true�ͻ�ȥ���¼��ָ��Լ���onTouchEvent����
    3. ������View����>����super.dispatchTouchEvent()Ĭ��ʵ�ֻ�ȥ���� onInterceptTouchEvent ��onInterceptTouchEvent return false���ͻ���¼��������ࡣ
    4. ��������View���¼���ֹ���´��ݣ��¼���ʼ���ݣ��Ӹ�View��onTouchEvent��ʼ�¼����µ��ϻع�ִ��ÿ���ؼ���onTouchEvent����->return false��
    
    **ע��** ����Viewû����View���Բ���ҪonInterceptTouchEvent ���ؼ��Ƿ���¼����ݸ���View�������أ�����View���¼��ַ�����super.dispatchTouchEvent()��ʱ��Ĭ�ϰ��¼������Լ���onTouchEvent�����൱�����أ����Ա�ViewGroup��dispatchTouchEvent �¼��ַ���View���¼��ַ�û�������ᵽ��4��Ŀ��ĵ�3�㡣

2. **ViewGroup��View��onTouchEvent���������¼�����ģ���ô����¼�ֻ������������ʽ��**

    1. �Լ����ѵ����¼��սᣬ���ٴ���˭���C>return true;
    2. �����������ϴ����������¼����ø�ViewҲ���յ�������¼����C>return false;**View��Ĭ��ʵ���ǲ����ѵġ�����super==false��**

3. **ViewGroup��onInterceptTouchEvent���������¼������������**

    1. �������������Լ���onTouchEvent����>return true;
    2. �����أ����¼����´�����View��->return false,**ViewGroupĬ���ǲ����صģ�����super==false��**

###4. ���� ACTION_MOVE �� ACTION_UP

1. �򵥵�˵�����ǵ�dispatchTouchEvent�ڽ����¼��ַ���ʱ��ֻ��ǰһ���¼�����ACTION_DOWN������true���Ż��յ�ACTION_MOVE��ACTION_UP���¼���
2.  **�����ĳ���ؼ���dispatchTouchEvent ����true�����ս��¼�**����ô�յ�ACTION_DOWN �ĺ���Ҳ���յ� ACTION_MOVE��ACTION_UP��
3. **������onTouchEvent�����¼������**�����ĸ�View��onTouchEvent ����true����ôACTION_MOVE��ACTION_UP���¼��������´������View��Ͳ������´����ˣ���ֱ�Ӵ����Լ���onTouchEvent �����������¼����ݹ��̡�



--
���ο���
* [����������֮ View �¼�����](http://b.codekk.com/blogs/detail/54cfab086c4761e5001b253e)
* [�����ǽ���Android�¼��ַ���õ�����](http://www.jianshu.com/p/2be492c1df96)
* [ͼ�� Android �¼��ַ�����](http://mp.weixin.qq.com/s/BJT0qAN_i0lXsJFnTrCJSg)