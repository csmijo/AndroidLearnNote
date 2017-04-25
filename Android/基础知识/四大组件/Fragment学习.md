#Fragmentѧϰ

`Android` `Fragment`

--

##1. android.app.Fragment Vs support.v4.Fragment

����Fragment����Android3.0��API 11������ģ��������AndroidManifest.xml �е�minSDK> 11������ʹ��android.app.Fragment��
����

�������Ҫ��API<11����֧�֣�����ʹ��support.v4.Fragment

##2. FragmentManager API

��������Ҫ��ʹ�õİ�����һ��
###a. android.app.Fragment 
```java
FragmentManager  fm = getFragmentManager();
MyFragment mFragment = (MyFragment)fm.findFragmentByid(R.id.fragment1);
```

###b. support.v4.Fragment

��������ActivityҪʹ��FragmentActivity
```java
FragmentManager fm = getSupportFragmentManager();
MyFragment mFragment = (MyFragment)fm.findFragmentByid(R.id.fragment1);
```
##3. FragmentTransaction API

```java
public void addFragment(View view){
    //1. ���FragmentManager
    FragmentManager fm = getFragmentManager();
    //2. ͨ��FragmentManager�õ�FragmentTransaction
    FragmentTransaction ft = fm.beginTransaction();
    //3. ��Fragment��ӵ�������
    MyFragment fragment = new MyFrament();
    //����1������id������2��Fragment���󣻲���3��Fragment��tag
    ft.add(R.id.layout,fragment,"test");
    //4. �ύ
    ft.commit();
}
```

##4. Fragment ʹ�õ�һЩע������

* [Android Fragment ��ʹ�ã�һЩ�㲻�ɲ�֪��ע������](http://yifeng.studio/2016/12/15/android-fragment-attentions/)