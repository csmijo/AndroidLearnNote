#padding��layout_margin������

`Android` 

--

##1. ����

Android��Padding��layout_margin��html�е���һ���ġ�����ͼ��ʾ��

![padding��layout_margin](http://images.cnblogs.com/cnblogs_com/ghj1976/201104/201104261840454974.png "")
![padding&margin.jpg](pic/padding&margin.jpg "")

1. ����һ��
    * Padding Ϊ�ڱ߿�ָ�ؼ�������Կؼ��ı߿�ľ���
    * layout_margin  Ϊ��߿�ָ�ؼ���Ը��ؼ��߿�ľ���
    
2. ��������
    * padding����**��������Ŀؼ�A** Ϊparent�ؼ������ڲ�����������ؼ�A�ļ�ࡣ**padding��վ�ڸ�view�ĽǶ���������**������ʾ����������������������view�߽�ľ��롣
    * layout_margin����A�ؼ�**���ڵĿؼ�**Ϊparent�ؼ�����A����ļ�ࡣ**margin��վ���Լ��ĽǶ����������**������ʾ�Լ����������������ң�view֮��ľ��룬���ͬһ��ֻ��һ��view����ô����Ч�������Ϻ�paddingһ����

3. ��������

 
To help me remember the meaning of padding, I think of a big coat with lots of thick cotton padding. I'm inside my coat, **but me and my padded coat are together. We're a unit.**

But to remember margin, I think of, "Hey, give me some **margin**!" **It's the empty space between me and you**. Don't come inside my comfort zone -- my margin.
 

![padding&margin_2.PNG](pic/padding&margin_2.PNG "")

##2. ���÷�����Ϣ�ܽ�

1. **view �е� width��height Դ�붨��**

    |����|����ֵ|˵��|
    |:--|:--:|:--|
    |view.getWidth()|mRight-mLeft|The width of your view, in pixels.|
    |view.getHeight()|mBottom-mTop|The height of your view, in pixels.|
    
2. **view �е� left, top, right, bottom Դ�붨��**

    |����|����ֵ|˵��|
    |:--|:--:|:--|
    |view.getLeft()|mLeft|1. Left position of this view relative to its parent. <br/>2. The left edge of this view, in pixels.|
    |view.getRight()|mRight|1. Right position of this view relative to its parent.<br/>2. The right edge of this view, in pixels.|
    |view.getTop()|mTop|1. Top position of this view relative to its parent. <br/>2. The top of this view, in pixels.|
    |view.getBottom()|mBottom|1. Bottom position of this view relative to its parent.<br/>2. The bottom of this view, in pixels.|

   
3. **ViewGroup�� LayoutParams �� leftMargin��topMargin��rightMargin��bottomMargin Դ�붨��**

    LayoutParams ��ȡ��ʽ�� **view.getLayoutParams()**

    |����|����ֵ|˵��|
    |:--|:--:|:--|
    |params.leftMargin|leftMargin|1. The left margin in pixels of the child.<br/>2. Margin values should be positive.<br/>3. Call {@link ViewGroup#setLayoutParams(LayoutParams)} after reassigning a new value to this field.|
    |params.topMargin|topMargin|1. The top margin in pixels of the child.<br/>2. Margin values should be positive.<br/>3. Call {@link ViewGroup#setLayoutParams(LayoutParams)} after reassigning a new value to this field.|
    |params.rightMargin|rightMargin|1. The right margin in pixels of the child.<br/>2. Margin values should be positive.<br/>3. Call {@link ViewGroup#setLayoutParams(LayoutParams)} after reassigning a new value to this field.|
    |params.bottomMargin|bottomMargin|1. The bottom margin in pixels of the child.<br/>2. Margin values should be positive.<br/>3. Call {@link ViewGroup#setLayoutParams(LayoutParams)} after reassigning a new value to this field.|
    
4. **view �е� leftPadding, topPadding, rightPadding, rightPadding Դ�붨��**

    |����|����ֵ|˵��|
    |:--|:--:|:--|
    |view.getPaddingLeft()|mPaddingLeft|1. Returns the left padding of this view. If there are inset and enabled scrollbars, this value may include the space required to display the scrollbars as well.<br/>2. the left padding in pixels|
    |view.getPaddingRight()|mPaddingRight|1. Returns the right padding of this view. If there are inset and enabled scrollbars, this value may include the space required to display the scrollbars as well.<br/>2. the right padding in pixels|
    |view.getPaddingTop()|mPaddingTop|1. Returns the top padding of this view. If there are inset and enabled scrollbars, this value may include the space required to display the scrollbars as well.<br/>2. the top padding in pixels|
    |view.getPaddingBottom()|mPaddingBottom|1. Returns the bottom padding of this view. If there are inset and enabled scrollbars, this value may include the space required to display the scrollbars as well.<br/>2. the bottom padding in pixels|
    |view.getPaddingStart()|(getLayoutDirection() == LAYOUT_DIRECTION_RTL) ? mPaddingRight : mPaddingLeft;|1. Returns the start padding of this view **depending on its resolved layout direction**. If there are inset and enabled scrollbars, this value may include the space required to display the scrollbars as well.<br/>2. the start padding in pixels|
    |view.getPaddingEnd()|(getLayoutDirection() == LAYOUT_DIRECTION_RTL) ? mPaddingLeft : mPaddingRight;|1. Returns the end  padding of this view  **depending on its resolved layout direction**. If there are inset and enabled scrollbars, this value may include the space required to display the scrollbars as well.<br/>2. the end padding in pixels|
    
    ���У�LAYOUT_DIRECTION_RTL ��ʾ Horizontal layout direction of this view is from Right to Left.
    
5. **����Ҫ��**
    * **To measure its(view) dimensions, a view takes into account its padding.** The padding is expressed in pixels for the left, top, right and bottom parts of the view. **Padding can be used to offset the content of the view by a specific amount of pixels.** For instance, a left padding of 2 will push the view's content by 2 pixels to the right of the left edge. Padding can be set using the **setPadding(int, int, int, int)** or** setPaddingRelative(int, int, int, int)** method and queried by calling getPaddingLeft(), getPaddingTop(), getPaddingRight(), getPaddingBottom(), getPaddingStart(), getPaddingEnd().
        * ��λ�˵����view �ڼ������Ĵ�С��Ҳ���� getWidth(),getHeight() ʱ��**�� padding ��ֵҲ��������**��
    * **Even though a view can define a padding, it does not provide any support for margins.** **However**, view groups provide such a support. Refer to **ViewGroup** and **ViewGroup.MarginLayoutParams** for further information.
        * ��λ�˵����view �ڼ������Ĵ�Сʱ��**���� margin ��ֵ��������**�� 
    
    
    
    



--
**�ο�����**
* [ android:padding��android:margin������](http://blog.csdn.net/xxdbupt/article/details/20450915)
* [Android��padding��layout_margin���������÷�](http://www.it165.net/pro/html/201503/35285.html)
* [Difference between a View's Padding and Margin](http://stackoverflow.com/questions/4619899/difference-between-a-views-padding-and-margin)
* [View](https://developer.android.com/reference/android/view/View.html)