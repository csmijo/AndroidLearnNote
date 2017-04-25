#Android SurfaceView 

`Android` `SufaceView`

--

## 1. ����

###1. ��ͨ view ��ȱ�ݣ�

1. View ȱ��˫�������
2. ��������Ҫ����view �ϵ�ͼƬʱ����������ػ� View ����ʾ������ͼƬ
3. ���߳��޷�ֱ�Ӹ��� view ���
4. ˢ��ʱ��Ҫ������������ invalidate() ���� postInvalidate()������view �Ƚϱ���

###2. SurfaceView ����Ҫ���ƣ�

1. SurfaceView ��ˢ�´���������������Ƶ���ĸ��»���
2. SurfaceView �Ļ��������߳̽��У�������UI �̵߳�����
3. SurfaceView �ڵײ�ʵ����һ��˫������ƣ�Ч�ʴ������

###3. SurfaceView ��ʹ��

1. �Զ��� SurfaceView �����̳� SurfaceView ʵ�� SurfaceHolder.Callback �ӿ�
2. ʵ�� SurfaceHolder.Callback �е����� SurfaceView �������ڣ��ֱ�Ϊ����
    * surfaceCreated(SurfaceHolder holder)�� ��Surface��һ�δ�������������øú�������������ڸú�������Щ�ͻ��ƽ�����صĳ�ʼ��������һ������¶�����������߳������ƽ��棬���Բ�Ҫ����������л���Surface��
    * surfaceChanged(SurfaceHolder holder, int format, int width, int height)����Surface��״̬����С�͸�ʽ�������仯��ʱ�����øú�������surfaceCreated���ú�ú������ٻᱻ����һ�Ρ� 
    * surfaceDestroyed(SurfaceHolder holder)

3. SurfaceView ͨ���� SurfaceHolder ���ʹ�ã�SurfaceHolder ��������֮������ SurfaceView �ϻ�ͼ������ SurfaceView �� getHolder() �������ɻ�ȡ SurfaceView ������ SurfaceHolder��

����˼�飬������ͱ��ص���ʱ����
1. ��surfaceCreated�����￪��һ�����̡߳�
2. ��������߳��п���һ����Flag���Ƶ�Whileѭ�������ڲ��ϵػ��ơ�
3. ��ѭ����ͨ��SurfaceHolder�����**lockCanvas����**���һ��Canvas�������ڻ��ơ�
4. ÿ�λ������ͨ��SurfaceHolder����**unlockCanvasAndPost����**����Canvas������ɸ��¡�
5. ���Ҫ��surfaceDestroyed������ȥ�ı�whileѭ����FlagΪfalse���������̵߳Ļ��ơ�

��ע�⡿�� ������ SurfaceHolder �� unlockCanvasAndPost() ����֮�󣬸÷���֮ǰ�����Ƶ�ͼ�λ����ڻ������У���һ�� lockCanvas() ����������������ܻ�"�ڵ�"����

##2. Դ�����

###1. SurfaceView �� MVC �ܹ�

1. Surface��SurfaceHolder �� SurfaceView ����֮��Ĺ�ϵʵ���Ͼ��ǹ�Ϊ��֪�� MVC�����У�
    * Surface����Model������ģ�ͣ�����
    * SurfaceView����View����ͼ����������
    * SurfaceHolder����Controller��������

###2. Surface

1. **android.view.SurfaceView**��Surface ʵ���� Parcelable �ӿڽ������л���������Ҫ�����ڽ��̼䴫�� surface ���󣩣�����������Ļ��ʾ�����������ݣ�Դ���ж�����ע��Ϊ��** Handle onto a raw buffer that is being managed by the screen compositor**�� Surface��ԭʼͼ�񻺳�����raw buffer����һ���������ԭʼͼ�񻺳���������Ļͼ��ϳ�����screen compositor������ġ�
2. ��ȻSurface�����˵�ǰ���ڵ��������ݣ�������ʹ�ù�������**��ֱ�Ӻ�Surface�򽻵�**�ģ���SurfaceHolder��Canvas lockCanvas()����Canvas lockCanvas(Rect dirty)��������ȡCanvas����ͨ����Canvas�ϻ����������޸�Surface�е����ݡ�

###3. SurfaceHolder

1. **android.view.SurfaceHolder**�� SurfaceHolder ʵ������һ���ӿڣ����䵱���� Controller �Ľ�ɫ��
2. Callback �� SurfaceHolder �ڲ���һ���ӿڣ��ӿ�������������������
    * **public void surfaceCreated(SurfaceHolder holder)**; 
        * Surface ��һ�α�����ʱ�����ã����� SurfaceView �Ӳ��ɼ�״̬���ɼ�״̬ʱ
        * ��������������õ� surfaceDestroyed ����������֮ǰ�����ʱ�䣬Surface �����ǿ��Ա������ģ��� SurfaceView ��˵������� SurfaceView ֻҪ���ڽ����Ͽɼ�������£��Ϳ��Զ������л�ͼ�ͻ��ƶ��� 
        * **���ﻹ��һ����Ҫע��**��Surface ��һ���߳��д�����Ҫ��Ⱦ��ͼ�����ݣ�������Ѿ�����һ���߳����洦����������Ⱦ���Ͳ���Ҫ�����￪���̶߳� Surface ���л�����
    * **public void surfaceChanged(SurfaceHolder holder, int format, int width, int height)**; 
        * Surface ��С�͸�ʽ�ı�ʱ�ᱻ���ã�����������л�ʱ�����Ҫ�� Sufface ��ͼ��Ͷ������д�������Ҫ������ʵ�� 
        * ��������� surfaceCreated ֮�����ٻᱻ����һ��
    * **public void surfaceDestroyed(SurfaceHolder holder)**; 
        * Surface ������ʱ�����ã����� SurfaceView �ӿɼ������ɼ�״̬ʱ
        * ��������������ù�֮�󣬾Ͳ��ܹ��ٶ� Surface ��������κβ�����������Ҫ��֤��ͼ���߳��������������֮���ٶ� Surface ���в���������ᱨ��

###4. SurfaceView

1. **android.view.SurfaceView**��SurfaceView������������ʾ Surface ���ݵ� View��ͨ�� SurfaceView ������ Surface �����ݡ�
2. Provides a dedicated drawing surface embedded inside of a view hierarchy. 

    ����Ļ��ʾ����ͼ����Ƕ����һ������ͼ����Ƶ� Surface ��ͼ
    
3. the SurfaceView punches a hole in its window to allow its surface to be displayed. 

    SurfaceView ����Ļ�����˸����������������Ƶ�ͼ��

4. �ڶ���ʲô��
    * **��������һ��Z��ĸ��SurfaceView ��ͼ���ڲ㼶��Z��λ����С������������ Activity ���ڵ� Layer �� Z ��ģ�����˵��ʵ SurfaceView ʵ������ʾ�� Activity ���ڵ���ͼ���·���**
    * ��ô��������ˣ�Ϊʲô�����ܿ��� SurfaceView������һ���˵����������ǽ������һ�����εĶ���Ȼ���ڶ���װ�˿鲣��������ܿ���ǽ����Ķ����ˡ�SurfaceView ���������������飬���� Activity ���ڵĲ㵱����ǽ
    
5. The Surface will be created for you while the SurfaceView's window is visible. 

    ����˵���˶�����ʲôʱ��ʼ�ģ��� SurfaceView �ɼ�ʱ���Ϳ��Կ�ʼ�� Canvas �ϻ���ͼ�񣬲���ͼ�����ݴ��ݸ� Surface ������ʾ�� SurfaceView ��

6. you should implement SurfaceHolder.Callback#surfaceCreated and SurfaceHolder.Callback#surfaceDestroyed to discover when the Surface is created and destroyed as the window is shown and hidden. 

    ��ʹ�� SurfaceView �ĵط���Ҫʵ�� SurfaceHolder.CallBack �ص������� Surface �Ĵ��������ٽ��м����Լ�����Ӧ�Ĵ�������Ĵ���ָ���ǿ�ʼ�� Canvas ���л��Ʋ������ݴ��ݸ� Surface ������ʾ



--

[�ο�����]

* [Android SurfaceView�Ļ���ʹ��](http://www.jianshu.com/p/07fa4180f0a5)
* [Android SurfaceView Դ�������ʹ��](http://tech.youzan.com/surfaceview-sourcecode/)