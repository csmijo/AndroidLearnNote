#�Զ���View

`Android` `view` `�ʼ�`

--
    
##1. ��������

* **����һ��** ��Androidϵͳ����ߵĽǶȣ�View������������ʲô�ģ�
* **�������** Androidϵͳ�����view�࣬������ЩĬ�Ϲ��ܺ���Ϊ������ʲô��������ʲô��
* **��������** ���Ҫ�ı����view����Ϊ����ۣ���ô��дview�еķ�����

##2. ����һ����Androidϵͳ����ߵĽǶȣ�View������������ʲô�ģ�

###1. �ٷ����壺
> This class represents the **basic building block for user interface components**. A view **occupies a rectangular area** on the screen and is **responsible for drawing and event handing**.

###2. ���

1. **View���û��ӿ�����Ļ��������顣**  ��Android�У��û���һ��Ӧ�ý�������ʵ���Ǻ�һ����view�ڽ��н�������Щview�����Ǽ򵥵�view��Ҳ����������view�ϳɵĸ���view������ViewGroup��
2. **View����Ļ��ռ��һ����������** **���ǽ�������ｻ�������⡣** ռ�ݾ���������Ϊ�˼򵥡�ͨ��������򣬿���ʵ�ֺ��û��Ľ���(������������϶���)��
3. **Viewͨ�������Լ����¼��������ַ�ʽ���û����н�����** **���ǽ����ν��������⡣** 
    * **ͨ�������Լ�ʵ�ֺ��û�������** ���磬�û����viewʱ���ı䱳����ɫ�ȡ�
    * **ͨ���¼�����ʵ�ֺ��û�������** ���磬�û����viewʱ������Toast�����û���ɵ����

##3. ����2��Androidϵͳ�����view�࣬������ЩĬ�Ϲ��ܺ���Ϊ������ʲô��������ʲô��

###1. view��α���ʾ����Ļ

* һ���������û�������һ��Window����ʾ��**Window����������е�View�ǡ�**
* Window���ȼ���һ��viewGroup���������������е�����view�����ViewGroup����**DecorView**��
* **ע��**�����DecorView���˰����û������ϵ���Щview������������Ϊ**Window���е�view����titleBar**��


###2. ȷ��ÿ��view��λ��
����DecorView֪������ͬ��ViewΪ������Լ��Ľ�����������Ҫ����Ļ�����С�ǲ�ͬ�ģ����ԣ�
* DecorView��ȷ����ÿ��View**�������Ļ�����С**ʱ��**������View�������**������һ�������ġ���������**measure����view�Ͱ�������viewGroupЭ��**
* ����ÿ��View**����Ļ�����е�λ��**�Ͳ�����View�Լ��������ˣ�����**��DecorViewһ�ֲٰ�**����������**layout�����ɰ���view��viewGroup����**

![�Զ���view_1.png](pic/�Զ���view_1.png "")

������ȻView�޷������Լ���ViewGroup�е�λ�ã����ǿ�����ʹ��Viewʱ������ViewGroup����Լ����õ�ViewҪ���������vertical LinearLayoutΪ����view�ڲ����ļ����ֵ�λ�þ���view��LinearLayout�г��ֵ�λ�ã�������ͨ��Layout_margin��Layout_gravity�Ƚ��н�һ�����������ԣ�
* **Layout_* ֮������ò�����view������**������ֻ��ʹ�ø�View��ʹ��������ϸ��������View��ViewGroup��λ�õġ�
* ��ЩLayout_* ֵ**��Inflateʱ������ViewGroup��ȡ**��Ȼ������һ��**ViewGroup�ض���LayoutParams**������ViewGroup��Ϊ����View����λ��ʱ���Ϳ��Բο����layoutParams�е���Ϣ�ˡ�

������ͬ��ViewGroupӵ�в�ͬ��LayoutParams�ڲ��࣬������Ϊ�����������View�����Լ�λ�õķ�ʽ�ǲ�һ���ġ�


������Щȷ��Viewλ�õĹ��̣�����װ��View��Layout�����С����ԣ�
* ���ڻ���view���ԣ�layout������û���õģ����Զ��ǿյġ���������**�Զ���View��ʱ���ø�дlayout����**
* ���ڷ���View������ViewGroup���ԣ���Ҫ��layout������Ϊ�Լ�����view����λ�á���������**�Զ���ViewGroup��Ҫ��дlayout����**

###3. ȷ��View�Ĵ�С

����Ҫȷ��View�Ĵ�С������һ��**�����ߡ�View��ViewGroup����Э��**�Ĺ��̡�

1. ����������д�����ļ�ʱ����Ϊviewд��layout_width,layout_height���������á����ǿ�������ViewGroup���ģ���ϣ�����View�Ĵ�С�Ƕ��١����������ÿ��ܵ�ȡֵ�����֣�
    * **����ֵ**������50dp
    * **match_parent**����ʾ��������ViewGroup˵���������е���Ļ���򶼸����View
    * **wrap_content**����ʾ��������ViewGroup˵��ֻҪ�����View����չʾ�Լ��Ŀռ伴�ɣ�**���ھ�������٣�����ҪViewGroup��View��ͨ��**

2. ViewGroup�յ��˿����߶�View��С��˵����Ȼ��**ViewGroup���ۺϿ����Լ��Ŀռ��С�Լ������ߵ�����Ȼ����������MeasureSpec����width��height������View��������������ViewGroup����View�����Ҫ��**�����൱�ڸ�����View�������Ѿ������ʹ���ߣ������ߣ��������ˣ����ڰ���������ȷ���Ľ�������㣬��Ŀ�Ȳ���Υ��width MeasureSpec�����Ҫ����ĸ߶Ȳ���Υ��height MeasureSpec�����Ҫ�����ڣ���Ͻ��������Ҫ��ȷ�����Լ�Ҫ���ռ䣬**ֻ���٣������Ŷ**����

    ����Ȼ��**���������󽫻ᴫ����View��`protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec)`������**����View����ô���أ����϶���Ҫ�ȿ���ViewGroup��Ҫ����ʲô�ɣ����ǣ����Ӵ�������������н����������Ϣ��
    
    ```java
    int widthMode = MeasureSpec.getMode(widthMeasureSpec);
    int widthSize =  MeasureSpec.getSize(widthMeasureSpec);
    int heightMode = MeasureSpec.getMode(heightMeasureSpec);
    int heightSize =  MeasureSpec.getSize(heightMeasureSpec);
    ```
    > **Mode��Sizeһ��׼ȷ������ViewGroup��Ҫ��**
    
    **Mode��ȡֵ�����֣����Ǵ�����ViewGroup������̬�ȣ�**
    * `EXACTLY`: ����ViewGroup��View˵����**ֻ����100dp**��ԭ���Ƕ����ģ��㲻�ܲ����ˣ���Ȼ��ﲻ������Ҫ�������ܾͲ������ˡ�
    * `AT_MOST`: ����**�����ֻ����100dp**��������Ϊ���ʹ����˵����ռ��wrap_content�Ĵ�С�����Ҹ������������ֲ�֪���㵽��Ҫռ������򣬵����Ҹ����㣬��ֻ��100dp�������Ҳֻ������ô�����
    * `UNSPCIFIED`: ���Լ����Ű죬����������Ĵ�С�����ң��ҿ��ǿ���

3. ��View�Ѿ�����������ViewGroup������ʹ���߶����Ĵ�С��������Ҫ���ˡ��²���Ҫ�ڸ�Ҫ������ȷ���Լ��Ĵ�С������ViewGroup�ˡ�

    ������view��ôȷ���Լ��Ĵ�С����ͬ��view�в�ͬ��̬�ȣ�����**�м�������Ĺ����Ҫ���ص�**��
    + **���һ��** **��ҪΥ��ViewGroup�Ĺ涨**��������õĳߴ�һ��Ҫ��ViewGroupҪ��ķ�Χ�ڣ������ǿ�Ȼ��Ǹ߶ȣ���
    + **��ض���** **����Ҫ�ڸ÷����е����Լ��Ļ��Ʋ���**����һ��ܺ���⣬�Ͼ�ViewGroup����˳ߴ�Ҫ��Ҫ��ʱ������һҪ������Լ��Ļ��ƣ����磬����Լ��ı���ͼƬ̫���Ǿ�����Ҫ���Ŷ��ٲź��ʣ���������һ�����������ֵ��
    + **�������** **����һ��Ҫ�����Լ����Ǻ�ĳߴ�**����������þ��൱��û�и���ViewGroup�Լ���Ҫ�Ĵ�С����ᵼ��ViewGroup�޷��������������õİ취������`onMeasure()`��������󣬵���`setMeasuredDimension()`������

    |childLayoutParams\parentSpecMode|EXACTLY|AT_MOST|UNSPECIFIED|
    |:---:|:---:|:---:|:---:|
    |dp/px|EXACTLY<br>childSize|EXACTLY<br>childSize|EXACTLY<br>childSize|
    |match_parent|EXACTLY<br>parentSize|AT_MOST<br>parentSize|UNSPECIFIED<br>0|
    |wrap_content|AT_MOST<br>parentSize|AT_MOST<br>parentSize|UNSPECIFIED<br>0|
    
###4. ����view

��������View�Ļ��ƣ��ǳ��򵥣�����һ������`onDraw()`��

##4. ����3�����Ҫ�ı����view����Ϊ����ۣ���ô��дview�еķ�����

![view-method-for-override.png](pic/view-method-for-override.png "")

* ����View��`inflated`������ϵͳ��ص���View��**`onFinishInflate()`**���������View��������������У���һЩ׼��������
* ������View������**Window�ɼ��Է����˱仯**��ϵͳ��ص���View��**`onWindowVisibilityChanged()`**��������Ҳ���Ը�����Ҫ���ڸ÷��������һ���Ĺ��������磬��Window��ʾʱ��ע��һ�������������ݼ������Ĺ㲥�¼��ı��Լ��Ļ��ƣ���Window���ɼ�ʱ�����ע�ᣬ��Ϊ��ʱ�ı��Լ��Ļ����Ѿ�û�������ˣ��Լ�ҲҪ����Window��ɲ��ɼ��ˡ�
* ��ViewGroup�е�**��View�������ӻ��߼���**������ViewGroup���Լ��������Ļ�����С�����仯ʱ��ϵͳ��ص�View��**`onSizeChanged()`**�������÷����У�View���Ի�ȡ�Լ����µĳߴ磬Ȼ���������ߴ���Ӧ�����Լ��Ļ��ơ�
* ���û���View��ռ�ݵ�**��Ļ�������˴�������**��ϵͳ�Ὣ�û��Ľ��������ֽ����DOWN��MOVE��UP��һϵ�е�MotionEvent�����Ұ���Щ�¼����ݸ�View��**`onTouchEvent()`**������View��������������н������û��Ľ�������
* ������Щ������View��ʵ����**�����ӿ�**�����£�
![�Զ���view_2.png](pic/�Զ���view_2.png "")

    �����ӿ��ǣ�
    * Drawable.Callback: ������View�е�Drawable�ܹ���Viewͨ�ţ�������AnimationDrawable�����Ǳ��������ûص�����ʵ�ֶԻ�Ч����
    * KeyEvent.Callback: ������������¼��ģ�����`onTouchEvent`�����������¼�����Ե�
    * AccessibilityEventSource


--
���ο���

* [���㲽��ΪӪ�����Զ���View](http://www.jianshu.com/p/d507e3514b65)
* [android����֡����](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2014/1106/1915.html)