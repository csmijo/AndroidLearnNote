#����������֮View��������

`Android` `View` `�ʼ�`

--

##1. View���Ļ�������

��`Activity`���յ������ʱ�����ᱻ������Ʋ���,�������� `Android framework` ����.**�����ǴӸ��ڵ㿪ʼ���Բ��������� `measure` �� `draw`**������ `View` ���Ļ�ͼ������`ViewRoot.java`���`performTraversals()`����չ�����ú��������Ĺ�����**�򵥸ſ�**Ϊ:
* �Ƿ���Ҫ���¼�����ͼ��С(measure)
* �Ƿ���Ҫ���°�����ͼ��λ��(layout)
* �Լ��Ƿ���Ҫ�ػ�(draw)

**����ͼ����:**
![view_mechanism_flow.png](pic/view_mechanism_flow.png "")

**View �������̺���������**

![view_draw_method_chain.png](pic/view_draw_method_chain.png "")

**ע�⣺**

�����û���������`request`��**ֻ��ִ��**`measure`��`layout`���̣���**����ִ��**`draw`���̡�

##2. ���measure��layout��

����������Measure��Layout�����������ִ������ͼ��ʾ��
![measure_layout.png](pic/measure_layout.png "")

###�������
####1. measure����

����measure������`measure(int,int)`�������𣬴��ϵ�������Ĳ���View����measure���̵����ÿ����ͼ�洢�Լ��ĳߴ��С�Ͳ������

����measure���̻�Ϊһ��View�������ӽڵ��`mMeasuredWidth`��`mMeasuredHeight`������ֵ����ֵ����ͨ��`getMeasuredWidth()`��`getMeasuredHeight()`������á�

**measure���̴��ݳߴ��������**
* `ViewGroup.LayoutParams` (View����Ĳ��ֲ���)
* `MeasureSpecs` (����ͼ������ͼ�Ĳ���Ҫ��)

1. **ViewGroup.LayoutParams**

    ���������ָ��**��ͼ�ĸ߶ȺͿ�ȵȲ���**������ÿ����ͼ��height��width�����������¼���ѡ��ֵ��
    * **����ֵ**
    * **MATCH_PARENT** ��ʾ����ͼϣ���͸���ͼһ����(**������paddingֵ**)
    * **WRAP_CONTENT** ��ʾ����ͼ��СΪ�����ܰ��������ݴ�С(**����paddingֵ**)

2. **MeasureSpecs**
    
    ������񣬰���**����Ҫ��ͳߴ����Ϣ**��������ģʽ��
    * **UNSPECIFIED**�� ����ͼ��������ͼ���κ�Լ���������Դﵽ������������ߴ硣(**һ���Զ���View���ò���**)
    * **EXACTLY**�� ����ͼΪ����ͼָ��һ��ȷ�еĳߴ磬������������ͼ����������������ڸ�ָ����С�ı߽��ڣ�**��Ӧ������Ϊ match_parent �����ֵ**��
    * **AT_MOST**������ͼΪ����ͼָ��һ�����ߴ硣����ͼ����ȷ�����Լ���������ͼ������Ӧ�ڸóߴ緶Χ�ڣ�**��Ӧ������Ϊ wrap_content**������ģʽ�£����ؼ��޷�ȷ���� View �ĳߴ磬ֻ�����ӿؼ��Լ���������ȥ�����Լ��ĳߴ磬**����ģʽ���������Զ�����ͼ��Ҫʵ�ֲ����߼������**��
    
3. **measure���ķ���**
    * `measure(int widthMeasureSpec,int heightMeasureSpec)`
        
        �÷������ɸ�д�������ջ����view/viewGroup��`onMeasure()`����
    * `onMeasure(int widthMeasureSpec,int heightMeasureSpec)`

        **�÷������������Զ�����ͼ��ʵ�ֲ����߼��ķ���**���÷����Ĳ����Ǹ���ͼ������ͼ�� `width` ��` height` �Ĳ���Ҫ��������������Զ�����ͼ�У�Ҫ���ľ��Ǹ��ݸ� `widthMeasureSpec` �� `heightMeasureSpec` ������ͼ��` width` �� `height`����ͬ��ģʽ����ʽ��ͬ��
    * `setMeasureDimension()`
    
         **�����׶��ռ�����**����`onMeasure(int widthMeasureSpec, int heightMeasureSpec)` �����е��ã�������õ��ĳߴ磬���ݸ��÷����������׶μ�������**�÷���Ҳ�Ǳ���Ҫ���õķ���������ᱨ�쳣**�����������Զ�����ͼ��ʱ�򣬲���Ҫ����ϵͳ���ӵ� Measure ���̵ģ�**ֻ�����**`setMeasuredDimension()`���ø��� `MeasureSpec` ����õ��ĳߴ缴��.
         
![measurechildflow.png](pic/measurechildflow.png "")
         
####2. layout����
    
����layout������`layout(int,int,int,int)��������Ҳ�����϶��½��б������ڸù����У�ÿ������ͼ�����`measure`���̵õ��ĳߴ����ڷ��Լ�������ͼ��

��������Ҫ��ȷ���ǣ�**����ͼ�ľ���λ�ö�������ڸ���ͼ���Ե�**��View �� `onLayout`����Ϊ��ʵ�֣��� `ViewGroup` �� `onLayout` Ϊ `abstract` �ģ���ˣ�**����Զ���� View Ҫ�̳� ViewGroup ʱ������ʵ�� onLayout ����**��

������ layout �����У�����ͼ�����`getMeasuredWidth()`��`getMeasuredHeight()`������ȡ�� `measure` ���̵õ��� `mMeasuredWidth` �� `mMeasuredHeight`����Ϊ�Լ��� `width` �� `height`��Ȼ��**����ÿһ������ͼ��`layout(l, t, r, b)`��������ȷ��ÿ������ͼ�ڸ���ͼ�е�λ��**��

####3. draw����

�ȿ�һЩ��draw������صĺ�����
* `View.draw(Canvas canvas)`: ���� ViewGroup ��û�и�д�˷�������ˣ����е���ͼ���ն��ǵ��� `View` �� `draw` �������л��Ƶġ�**���Զ������ͼ�У�Ҳ��Ӧ�ø�д�÷��������Ǹ�д onDraw(Canvas) �������л���**������Զ������ͼȷʵҪ��д�÷�������ô���ȵ��� super.draw(canvas)���ϵͳ�Ļ��ƣ�Ȼ���ٽ����Զ���Ļ��ơ�
* `View.onDraw()`: View ��onDraw��Canvas��Ĭ���ǿ�ʵ�֣�**�Զ�����ƹ�����Ҫ��д�ķ���**��������������ݡ�
* `dispatchDraw()`: ���������ͼ�Ļ��ơ�View ��Ĭ���ǿ�ʵ�֣�**ViewGroup ��д��`dispatchDraw()`����������ͼ���л���**���÷�������**����ȥ��**���Զ���� `ViewGroup` **��Ӧ��**��dispatchDraw()���и�д��
* `drawChild(canvas, this, drawingTime)`
ֱ�ӵ����� `View` �� `child.draw(canvas, this,drawingTime)` �������ĵ���Ҳ˵���ˣ����˱�`ViewGroup.drawChild()` �����⣬�㲻Ӧ���������κεط�ȥ��д����ø÷����������� `ViewGroup`����`View.draw(Canvas)`�����������Զ���ؼ��п��Ը�д�ķ�����������Բο�������`view.draw(Canvas)`��˵�����Ӳ����п��Կ�����`child.draw(canvas, this, drawingTime)` �϶��Ǵ����˺͸���ͼ��ص��߼����� `View` �����ջ��ƣ����� `View.draw(Canvas)`������
* `invalidate()`: �����ػ�View������draw���̣�������ͼ��Сû�з����仯�Ͳ������`layout()`���̣�����ֻ������Щ������`invalidate()`������view
* `requestLayout()`: �����ֱ仯��ʱ�򣬱��緽�򣬳ߴ�仯ʱ����ø÷��������Զ������ͼ�У�**���ĳЩ�����ϣ�����²����ߴ��С��Ӧ���ֶ�ȥ���ø÷��������ᴥ��`measure()`��`layout()`���̣���������� `draw`**��

![draw_method_flow.png](pic/draw_method_flow.png "")
--
���ο���
* [����������֮ View ��������](http://b.codekk.com/blogs/detail/54cfab086c4761e5001b253f)