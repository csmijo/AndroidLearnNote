#���ScrollViewǶ��ListView��GridView��ʾ��ȫ

`Android`

--

�ܶ࿪����Ա���������������󣬾���ScrollView�ڲ�Ƕ��ListView������ListView���������ǲ�ȷ����
��������Ҫ����Ϊ�������ݣ�Ȼ��ͻᷢ��ListView�ͻ���ʾ��һ�г�����Ȼ��ͻ�ٶȵ�һ������������̳�ListView����дonMeasure������

##1. �������


����ͨ����дListView ���� GridView �� onMeasure() �����������ʾ��ȫ���⡣

```java
@Override  
protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {  
    int expandSpec = MeasureSpec.makeMeasureSpec(Integer.MAX_VALUE >> 2, MeasureSpec.AT_MOST);  
    super.onMeasure(widthMeasureSpec, expandSpec);  
}  
```

* [���ScrollView��Ƕ��ListView��GridView��ʾ��ȫ������(��ͻ)](http://blog.csdn.net/cs_li1126/article/details/12906203)
* [���Ƕ��ListView��ScrollView������ʾ��ȫ������](http://blog.csdn.net/hanhailong726188/article/details/46136569)

##2. ԭ��

ListView �� onMeasure() ������

```java
if (heightMode == MeasureSpec.UNSPECIFIED) {
      heightSize = mListPadding.top + mListPadding.bottom + childHeight +
                   getVerticalFadingEdgeLength() * 2;
}

if (heightMode == MeasureSpec.AT_MOST) {
     // TODO: after first layout we should maybe start at the first visible position, not 0
     heightSize = measureHeightOfChildren(widthMeasureSpec, 0, NO_POSITION, heightSize, -1);
}
```

* �� `heightMode` �� `MeasureSpec.UNSPECIFIED` ʱ���߶Ⱦ͵��ڵ�һ�еĸ߶�ֵ��
* �� `heightMode` �� `MeasureSpec.AT_MOST` ʱ���߶Ⱦ͵���������view�ĸ߶�
* GridView �� onMeasure() ������Ч��һ��

���ԣ����ǲ²��������Ϊ`ScrollView`������һ��`UNSPECIFIED`���Ƹ�`ListView`��

ͨ��`ScrollView` ��`onMeasure()` Դ����Է��֣�`ScrollView` �� `measureChildWithMargins()` ����
`ListView` �� `onMeasure()` ����������һ��`UNSPECIFIED` �����ơ�

Ϊʲô�أ����룬**��ΪScrollView���������ǿ�������ֱ��������Ĳ���**�����ԣ����������е���View�ĸ߶Ⱦ���UNSPECIFIED��
��˼���ǣ�**��������View�ж��**����Ϊ�ұ���������Ҫ��ֱ�����ģ����ı��������ˣ�����������View�߶Ȳ����κ����ơ�


* [Android View��ܵ�measure����](http://blog.csdn.net/hjf_huangjinfu/article/details/51147636)

