#Fragment��ѧէ��

`Android` `Fragment`

--

##1. ��������

###1) Fragment�ĸ���

����Fragment��Android3.0�������һ���µ�API�������ֵĳ�����Ϊ����Ӧ����Ļ��ƽ����ԣ���Ȼ��������Ȼ��ƽ��APP UI��Ƶĳ��������������ͨ�ֻ�����Ҳ��������`Fragment`�� ���ǿ��԰���**����һ��С�͵�Activity���ֳ�`Activity`Ƭ��**��

�������룬���һ���ܴ�Ľ��棬�� ��һ�����֣�д����������ж��鷳��������������Ļ��ǹ�������Ҳ���鷳����ʹ��`Fragment` ���ǿ��԰�**��Ļ���ֳɼ��飬Ȼ����з��飬����һ��ģ�黯�Ĺ���**���Ӷ����Ը��ӷ���������й����ж�̬�ظ���`Activity`���û����棡

��������**`Fragment`�����ܵ���ʹ�ã�����ҪǶ����`Activity`��ʹ��**��������ӵ���Լ����������ڣ����ǻ��ǻ��ܵ�����Activity���������ڵ�Ӱ�죬����Activity ��destory�����ˣ���Ҳ��������٣�

###2) Fragment����������
![Fragment����������](http://www.runoob.com/wp-content/uploads/2015/08/31722863.jpg "")

###3) ����Ҫ��

1. 3.0�汾������,��minSdkҪ����11
2. `Fragment`��ҪǶ����`Activity`��ʹ��,��ȻҲ����Ƕ�׵�����һ��`Fragment`��,�������Ƕ�׵�`Fragment`Ҳ����ҪǶ����`Activity`�е�,��ӵ�˵��**Fragment������ҪǶ����Activity��**!! �ܼ���Activity����������Ӱ��,��Ȼ��Ҳ���Լ�����������!����**��������Fragment���� Ƕ��Fragment��ΪǶ���������Fragment�������ڲ��ɿ�**!!!
3. �ٷ��ĵ�˵����Fragmentʱ������Ҫʵ����������:`onCreate()`,`onCreateView()`,`OnPause()`; ����**ò��ֻдһ��`onCreateView()`Ҳ�ǿ��Ե�**...
4. Fragment���������ں�Activity�е����ƣ���**����״̬**:
    * Resumed:�������е�Fragment�ɼ���
    * Paused:����Activity�ɼ�,���ǵò������㣻
    * Stoped: 
        * ����addToBackStack(),Fragment����ӵ�Bcakջ 
        * ��Activityת���̨,���߸�Fragment���滻/ɾ��
5. ֹͣ״̬��fragment��Ȼ����(����״̬�ͳ�Ա��Ϣ��ϵͳ������),Ȼ��,�����û����ٿɼ�,�������`activity`���ɵ�,��Ҳ�ᱻ�ɵ�.

###4) `android.app.Fragment` Vs `andrioid.support.v4.app.Fragment`

�ڵ���Fragment���Ǿ�����ʹ���ĸ����µ�Fragment���أ���

������ʵ��ǰ��˵��Fragment��`Android 3.0(API 11)`������ģ���ô���������app��Ҫ��3.0���µİ汾���У���ô��ʹ��`andrioid.support.v4.app.Fragment`����Ϊv4����Ϳ��Լ��ݵ�1.6�汾�����������android 3.0���µİ汾����ʹ��`android.app.Fragment`���ɡ�

**ʹ��V4���µ�Fragmentʱע�����**
* �����ʹ����v4���µ�Fragment,��ô���ڵ��Ǹ�`Activity`��Ҫ�̳�`FragmentActivity`Ŷ! 
* `Fragment`,`FragmentManager`,`FragmentTransaction`�����õ�v4����
* `getFragmentManager()`�ĳ�`getSupportFragmentManager()`

##2. ����һ��Fragment

###1) ��̬����Fragment

![��̬����Fragment](http://www.runoob.com/wp-content/uploads/2015/08/14443487.jpg "")

###2) ��̬����Fragment

![��̬����Fragment](http://www.runoob.com/wp-content/uploads/2015/08/29546434.jpg "")

##3. Fragment������Fragment����

![Fragment������Fragment����](http://www.runoob.com/wp-content/uploads/2015/08/97188171.jpg "")

##4. Fragment��Activity�Ľ���

![Fragment��Activity�Ľ���](http://www.runoob.com/wp-content/uploads/2015/08/45971686.jpg "")

###1) Fragment�������ݸ�Activity
* **Step1������һ���ص��ӿ�(Fragment��)**

    ```java
    /*�ӿ�*/  
    public interface CallBack{  
        /*����һ����ȡ��Ϣ�ķ���*/  
        public void getResult(String result);  
    }  
    ```
* **Step2:�ӿڻص�(Fragment��)**

    ```java
    /*�ӿڻص�*/  
    public void getData(CallBack callBack){  
        /*��ȡ�ı������Ϣ,��Ȼ��Ҳ���Դ��������͵Ĳ���,������*/  
        String msg = editText.getText().toString();  
        callBack.getResult(msg);  
    }  
    ```
* **Step3:ʹ�ýӿڻص�������ȡ����(Activity��)**

    ```java
    /* ʹ�ýӿڻص��ķ�����ȡ���� */  
    leftFragment.getData(new CallBack() {  
     @Override  
           public void getResult(String result) {              /*��ӡ��Ϣ*/  
                Toast.makeText(MainActivity.this, "-->>" + result, 1).show();  
                }
            }); 
    ```
    
###2) Fragment��Fragment֮������ݻ���

������ʵ��ܼ�,�ҵ�Ҫ�������ݵ�`fragment����`,ֱ�ӵ���`setArguments`�����ݽ�ȥ�Ϳ����ˡ�
* ͨ���Ļ���replaceʱ,��fragment��ת��ʱ�����ݵ�,��ôֻ��Ҫ�ڳ�ʼ��Ҫ��ת��`Fragment`���������`setArguments()`�����������ݼ���!
* ���������`Fragment`��Ҫ��ʱ������,������ת�Ļ�,����Ҫ����`Activity`���f1������������, �ٴ���f2��,������**ActivityΪý��**~

**ʾ���������£�**

```java
FragmentManager fManager = getSupportFragmentManager( );
FragmentTransaction fTransaction = fManager.beginTransaction();
Fragment t1 = new Fragment();
Fragment t2 = new Fragment();
Bundle bundle = new Bundle();
bundle.putString("key",id);
t2.setArguments(bundle); 
fTransaction.add(R.id.fragmentRoot, t2, "~~~");  
fTransaction.addToBackStack(t1);  
fTransaction.commit(); 
```

##5. ��һ����������

1. `Activity`����`Fragment`��ʱ��,���ε�������ķ���:**onAttach -> onCreate -> onCreateView -> onActivityCreated -> onStart ->onResume**
2. ������Ū��һ�������ĶԻ������`Activity`,��������,����**��Fragment���ڵ�Activity�ɼ�,������ý���**����ʱ��״̬Ϊ��**onPause**
3. ���Ի���ر�,`Activity`�ֻ���˽���,״̬�ֱ�Ϊ**onResume**
4. �������滻`Fragment`,������`addToBackStack()`������ӵ�Backջ�� **onPause -> onStop -> onDestoryView** ����**ע��**����ʱ��`Fragment`��û�б�����Ŷ!!!
5. �����ǰ��¼��̵Ļ��˼���`Fragment`���ٴ���ʾ����: **onCreateView -> onActivityCreated -> onStart -> onResume**
6. ��������滻��,������`commit`֮ǰû�е���`addToBackStack()`������ `Fragment`��ӵ�backջ�еĻ�;�ֻ����˳���`Activity`�Ļ�,��ô`Fragment`���ᱻ��ȫ����, `Fragment`���������״̬**onPause -> onStop -> onDestoryView -> onDestory -> onDetach**

--
**�ο����ף�**

* [Fragment��������](http://www.runoob.com/w3cnote/android-tutorial-fragment-base.html "")