#View�����������

`Android` `View`

--

##1. ����

��ȡ�����һЩ��������������ͼ��ʾ��

![view����ϵ](http://jbcdn2.b0.upaiyun.com/2016/08/37af6dff6bb770ac33823a9127b2700c.png "")

![��Ļview����ϵ](http://jbcdn2.b0.upaiyun.com/2016/08/f86ba7108f5389b0f0e6f43a6696a247.png "")

###1. view�ṩ�ķ���
* **getTop**: view����Ķ��ߵ��丸���ֶ��ߵľ���
* **getBottom**: view����ĵױߵ��丸���ֶ��ߵľ���
* **getLeft**: view�������ߵ��丸������ߵľ���
* **getRight**: view������ұߵ��丸������ߵľ���

###2. MotionEvent�ṩ�ķ���
* **getX()**: ��ȡ����¼���Կؼ���ߵ�x�����꣬������¼�����ؼ���ߵľ���
* **getY()**: ��ȡ����¼���Կؼ����ߵ�y�����꣬������¼�����ؼ����ߵľ���
* **getRawX()**: ��ȡ����¼����������Ļ��ߵ�x�����꣬������¼�����������Ļ��ߵľ���
* **getRawY()**: ��ȡ����¼����������Ļ���ߵ�y�����꣬������¼����������Ļ���ߵľ���

--
**[�ο�]**
* [android֮View����ϵ(view��ȡ��������ķ����͵���¼�������Ļ�ȡ)](http://blog.csdn.net/jason0539/article/details/42743531)

##2. ��ȡ

![Android4.0���ڻ���](http://jbcdn2.b0.upaiyun.com/2016/08/24eac3a9409b8a95190c2fe170393658.png "")


��������View��ViewGroup��˵��width��height��top��left������ֵ����Measure��Layout�������֮��ſ�ʼ��ȷ��ֵ�ģ���**Measure��Layoutȴ������onCreate����ִ�У�����onCreate��getLeft������ȡ����ֵ**��

�����������onCreate������ȡ��width��height��ֵ�أ��ο�һ�²��ͣ�
* [�����onCreate()�����л�ȡView��width��HeightΪ0��4�ַ���](http://www.cnblogs.com/kissazi2/p/4133927.html)
* [ onCreate��View��width,heightΪ0������](http://blog.csdn.net/codezjx/article/details/45341309)��

�ܽ����£�

1. ����Draw/Layout�¼���ViewTreeObserver
2. **��һ��runnable��ӵ�Layout�����У�View.post()**
3. ��дView��onLayout����
4. **��дActivity��onWindowFocusChanged�������ڸ÷����л�ȡ**

--

**[�ο�]**
* [Android4.0���ڻ��ƺʹ������̷���](http://bbs.51cto.com/thread-1072344-1.html)
* [�����onCreate()�����л�ȡView��width��HeightΪ0��4�ַ���](http://www.cnblogs.com/kissazi2/p/4133927.html)
* [ onCreate��View��width,heightΪ0������](http://blog.csdn.net/codezjx/article/details/45341309)

##3. ����

###1. Android�������᣺

![Android����ϵ](http://jbcdn2.b0.upaiyun.com/2016/08/72351a14d893c8da0311a817fd5e85bd.png "")

###2. ʵ��View�ƶ��ķ�����������ͼ��ʾ��
![View�ƶ��ķ������](http://jbcdn2.b0.upaiyun.com/2016/08/bac0e3eab708d9d498b73eabedf4efb8.png "")


###3. ����scrollTo��scrollBy��Ҫע�����������
**����һ��**


**�ƶ�����ֵ = �ʼ������ �C ����ƶ���������**

ԭ������Ϊ���ջ�����������
���� invalidateInternal(l �C scrollX, t �C scrollY, r �C scrollX, b �C scrollY, true, false);

**����l,t,r,bΪԭ������㣬scrollX,scrollYΪĿ������㣬ֻ�е�Ŀ�������ֵ�Ǹ���ʱ���ƶ�����λ�ò�Ϊ������**

����scrollTo ������Ҫ�ӣ�0,0���ƶ�����200,400������㣬��������Ĺ�ʽ��֪Ϊ��ֵ


**�������**

**Ϊʲô��Ҫ���� ((View)getParent())��**

TestTextView������View��**scrollTo��scrollBy�ƶ��Ķ���View��Content**��������ӵĻ���ʹ�õ�Ч������TestTextView������λ�ñ仯����TestTextView������仯��

**�����ViewGroup��ʹ��scrollTo��scrollBy�����ƶ�����ViewGroup�е�View**.����������Ҫ��TestTextView�ƶ�������Ҫ�� ((View)getParent())��Ȼ����((View)getParent()).scrollTo��


--

**[�ο�]**
* [��Щ��Ӧ��֪��ȴ��һ��֪���ġ�View�����������](http://android.jobbole.com/84285/)