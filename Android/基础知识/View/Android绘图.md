#Android��ͼ

`Android` `��ͼ`

--

##1. Drawable��Դʹ��ע������

1. Drawable��Ϊ���֣�**һ��**������**��ͨ��ͼƬ��Դ**����Android Studio������һ��ŵ�`res/mipmap`Ŀ¼�£� ����ǰ��Eclipse��һ��Ŷ��������������ѹ����л���Android��Ŀģʽ������ֱ����`mipmap`Ŀ¼�¶�ͼƬ���ɣ�AS���Զ���hdpi��xhdpi...!**��һ��**�����Ǳ�д��**XML��ʽ��Drawable��Դ**������һ������Ƿŵ�`res/drawable`Ŀ¼ �£���������İ�ť��������л���Selctor��
2. ��XML����ֱ��ͨ��`@mipmap`����`@drawable`����Drawable���ɡ�����: `android:background = "@mipmap/iv_icon_zhu",   "@drawable/btn_back_selctor"` ������Java���������ǿ���ͨ��Resource��`getDrawable(R.mipmap.xxx)`���Ի��drawable��Դ �����Ϊĳ���ؼ����ñ���������ImageView�����ǿ���ֱ�ӵ��ÿؼ�`.getDrawale()`ͬ�� ���Ի��drawable����
3. Android��drawable�е���Դ������Լ���������ǣ�**[a-z0-9_.]������ֻ������ĸ���ּ���.��**�� ���Ҳ��������ֿ�ͷ���������ᱨ�� `Invalid file name: must contain only [a-z0-9.]`�� Сд����������Сд������Сд��������Ҫ����˵����~

##2. Drwable,Bitmap,Canvas,Matrix

1. **Drawable**:ͨ�õ�ͼ�ζ�������װ�س��ø�ʽ��ͼ�񣬼ȿ�����PNG��JPG������ͼ��Ҳ��ǰ��ѧ����13��Drawable���͵Ŀ��ӻ��������ǿ�������**һ�������Ż��ġ�������**��
2. **Bitmap(λͼ)**�����ǿ���**��������һ������**�������Ȱѻ��ŵ����棬Ȼ�����ǿ��Խ���һЩ���������ȡͼ���ļ���Ϣ������ת�и�Ŵ���С�Ȳ�����
3. **Canvas(����)**����������**����**�����ǿ�������������(����)����ȿ�����**Paint(����)**������������״����д�֣��ֿ�����**Path(·��)**�����ƶ���㣬Ȼ�����ӳɸ���ͼ�Σ�
4. **Matrix(����)**��**����ͼ����Ч�����**����ɫ����(ColorMatrix)������ʹ��Matrix����ͼ��� ƽ�ƣ����ţ���ת����б�ȣ�

##3. Paint��Canvas��Path���

�������÷����鿴��[������ͼ���������](http://www.runoob.com/w3cnote/android-tutorial-drawable-tool.html)

###1) Paint(����)

����**�������û��Ʒ��**,��:�߿�(�ʴ���ϸ),��ɫ,͸���Ⱥ������� ֱ��ʹ���޲ι��췽���Ϳ��Դ���Paintʵ��: `Paint paint = new Paint( );`

###2) Canvas(����)

1. Canvas��**���췽��**�����֣�
    * Canvas(): ����һ���յĻ���������ʹ��`setBitmap()`���������û��ƾ���Ļ�����
    * Canvas(Bitmap bitmap): ��bitmap���󴴽�һ����������**���ݶ�������bitmap**�ϣ����bitmap����Ϊnull��
2. **drawXXX()������**����һ��������ֵ�ڵ�ǰ��ͼ����ͼ������**ͼ�����ӣ� ������滭��ͼ��Ḳ��ǰ��滭��ͼ��**��
    * `drawPath(Path path, Paint paint)`������һ��·��������һΪPath·������
    * `drawBitmap(Bitmap bitmap, Rect src, Rect dst, Paint paint)` �� ��ͼ������һ�������ǳ����Bitmap���󣬲�������Դ����(������bitmap)�� ��������Ŀ������(Ӧ����canvas��λ�úʹ�С)����������Paint��ˢ���� ��Ϊ�õ������ź�����Ŀ��ܣ���ԭʼRect������Ŀ��Rectʱ���ܽ����д����ʧ��

3. **save()��restore()����**�� 
    * save( )����������Canvas��״̬��save֮�󣬿��Ե���Canvas��ƽ�ơ���������ת�����С��ü��Ȳ����� 
    * restore�����������ָ�Canvas֮ǰ�����״̬����ֹsave���Canvasִ�еĲ����Ժ����Ļ�����Ӱ�졣 
    * save()��restore()Ҫ**���ʹ��**(restore���Ա�save��,�����ܶ�)����restore���ô�����save��,�ᱨ��

���ο���
* [Canvas��save��restore](http://www.cnblogs.com/xirihanlin/archive/2009/07/24/1530246.html)

###3) Path(·��)

�����򵥵�˵������㣬����~�ڴ��������ǵ�Path·���󣬿��Ե���Canvas��`drawPath(path,paint)` ��ͼ�λ��Ƴ�����

##4. ˫���弼��

�����ȸ���һ�£�˫����ĺ��ļ���������ͨ��`setBitmap()`������Ҫ���Ƶ����е�ͼ�λ��Ƶ�һ��`Bitmap`�ϣ�Ȼ����������`drawBitmap()`�������Ƴ����`Bitmap`����ʾ����Ļ�ϡ�

����ʵ�ֲ������£�
```java
/*1. ����*/
Canvas bufferCanvas;
Bitmap bufferBitmap;
Paint paint;

/*2. ��������*/
bufferCanvas = new Canvas(bufferBitmap);
paint = new Paint();

/*3. �ڻ����л�ͼ*/
bufferCanvas.drawCircle(x,y,radius,paint);

/*4. ����Ļ�ϻ�ͼ*/
canvas.drawBitmap(bufferBitmap,0,0,paint);
```

##5. ��С��������

�����ж�`view`��`click` ��`move`����ʱ���������жϻ�������С���룬��׼д���� 
```java
int touchSlop = ViewConfigureation.get(context).getScaledTouchSlop();```