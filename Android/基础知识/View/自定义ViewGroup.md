#�Զ���ViewGroup

`Android` `ViewGroup` `�ʼ�`

--

##1. ViewGroup��Viewְ�����

��Api�ĽǶȶ�ViewGroup��View����ǳ����

1. View��ְ���Ǹ���ViewGroup����Ĳ���ֵ�Ͳ���ģʽ�����Լ��Ŀ�߽���ȷ��(`onMeasure()`�����)��Ȼ����`onDraw()`����ɶ��Լ��Ļ���
2. ViewGroup����Ҫ��View����View�Ĳ���ֵ�Ͳ���ģʽ(`onMeasure()`�����)�����Ҷ��ڴ�ViewGroup�ĸ����֣��Լ�Ҳ��Ҫ��`onMeasure()`��ɶ��Լ���ߵ�ȷ�������⣬����Ҫ��`onLayout()`����ɶ���childView��λ��ָ����

![measurechildflow.png](pic/measurechildflow.png "")

##2. �Զ���ViewGroup���ʾ͸�һ���¡���layout

ViewGroup**���������ְ��**�������Լ����ڲ�����ÿһ��view/viewGroup��һ�����ʵ�λ�ã�Ҳ���ǵ������ǵ�`layout()`������

```java
public void layout(int left, int top, int right, int bottom)
```

**ע�⣺**

1. **����`left`,`right`,`top`,`bottom`**�� ���Ƕ�������ֵ�������ǲ��յ�**����ϵ����ViewGroup�趨��**���������ϵ����ViewGroup���Ͻ�Ϊԭ�㣬���� X�� ���� Y���������ġ�
2. ViewGroup���Լ���layout�����У������parent���Լ��趨�ĳߴ��С����**availableWidth**��**availableHeight**�����ֵ�൱��parent����ViewGroup��������������Ͻ�ΪԲ�㣬����Ϊx������Ϊy������ϵ�������ÿһ����Viewȷ��λ�úʹ�С���ҿ������㱣֤���������ϵ�еĵ�P1��0��0������P2��availableWidth��0������P3��0��availableHeight������P4��availableWidth,availableHeight����ɵķ��������ڵ���View�����Ի�����ֻ���Ļ������ָӲ�������ϵ���Ļ����չʾ�Լ��Ļ��ᡣ�������֮�����View���ܲ������ֻ���Ļ��չʾ�Լ����Ҿ͹ܲ����ˡ������������ǿ�����**parent�����ǵ�ViewGroup�趨�ĳߴ磬����һ������ȫ��Ӧ���ֻ���Ļ�ϵ�һ����ͬ��С������**������Щ����£�parent�����ǵ�ViewGroup�趨������ߴ���ܱ������ֻ���Ļ���󡣵��ǣ�parent��Ȼ�����Ǳ�֤���ڸ�������layout����View�����ܻ�����ֻ���Ļ��չʾ�Լ��Ļ��ᣬparent�����������һ����أ����ǣ�**ͨ��parent��scroll���ܡ�**
3. ��������һ��ViewGroup���Ұ�һ����View��һ����layout����parent�����������ڣ�**��һ���ֳ����˸�����**�������View�ǲ������ֻ�ܻ�ò���չʾ�Լ��Ļ��᣿�����û��ɣ����ǣ�**Yes��**
4. ��ν��layout��parent�޶��������view����ʾ��������ѡ��
    * **ѡ��һ��** ��Ҫ����View �ŵ��������֮��
    * **ѡ�����** �����ViewGroupʵ��scroll���ܣ��Ӷ�ȷ��parent�޶����������ViewҲ�ܹ��л���չʾ�Լ���
    * **ѡ������** �����ViewGroup��parent����ScrollView���������ViewGroup�Ͳ����Լ�ʵ��scroll�����ˡ�����ScrollViewֻ��������View�ĸ߶ȳ����Լ�����������View�Ŀ�ȳ����Լ������ԣ���ΪViewGroup�������ڲ�����availableWidth������£�����View layout ������ĸ߶��ϡ�
    * **ԭ����ǣ�** **�����߶ȣ�������ȣ�**


##3. ����*

### 1. getWith(),getMeasuredWidth(),getIntricWidth()??

Դ���ж��壺

|����|����ֵ|˵��|
|:---:|:---:|:---|
|`getWidth()`|**mRight-mLeft**|return the width of you view, in pixels.|
|`getMeasuredWidth()`|**mMeasuredWidth & MEASURED_SIZE_MASK**|like `getMeasuredWidthAndState()`,but only returns the **raw width** component(that is the result is masked by `MASURED_SIZE_MASK`)|
|`getMeasuredWidthAndState()`||1. Return the full width measurement information for this view as computed by the most recent call to `#measure(int, int)`. <br>2. This result is a bit mask as defined by  `#MEASURED_SIZE_MASK` and `#MEASURED_STATE_TOO_SMALL`<br> 3. This should be used during measurement and layout calculations only.<br> 4. Use `#getWidth()` to see how wide a view is after layout.|
   
**�ܽ᣺**

1. `getMeasuredWidth()`�� ��õ�ֵ��`setMeasuredDimension()`�������õ�ֵ������ֵ��`measure()`�������к�ͻ�ȷ����
2. `getWidth()`�� ��õ�ֵ��`layout`�����д��ݵ��ĸ������е�`mRight-mLeft`������ֵ��`layout()`�������к�ȷ����
3. һ���������`onLayout`������ʹ��`getMeasure  dWidth()`���������ڳ�`onLayout`����֮��ĵط���`getWidth`����

**getMeasuredWidth():**
![getMeasuredWidth.png](pic/getMeasuredWidth.png "") 

**getWidth():**
![getWidth.png](pic/getWidth.png "") 


��������
* [Android����֮getMeasuredWidth��getWidth�����Դ�����](http://blog.csdn.net/dmk877/article/details/49734869)

###2. getPaddingLeft??  padding?? margin???
 
�����鿴�ʼ� **#padding��layout_margin������**��
###3. getLeft()???

Դ���ж��壺

|����|����ֵ|˵��|
|:---:|:---:|:---|
|`getLeft()`|**mLeft**|1.Left position of this view relative to its parent <br> 2. return the left edge of this view, in pixels.|

�ο������**`getWidth()`**

--
��������
* [���㲽��ΪӪ�����Զ���ViewGroup](http://www.jianshu.com/p/5e61b6af4e4c)
* [Android �ְ��ֽ����Զ���ViewGroup��һ��](http://blog.csdn.net/lmj623565791/article/details/38339817)