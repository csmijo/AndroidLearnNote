#Activity��ѧէ��

`Android` `Activity`

--

##1. Activity�ĸ������������ͼ

![Activity�ĸ������������ͼ](http://www.runoob.com/wp-content/uploads/2015/08/18364230.jpg "Activity�ĸ������������ͼ")

>`ע�⣺`AlertDialog��PopWindow ���ᴥ��onPause()��onStop()����

##2. Activity/ActionBarActivity/AppCompatActivity������
����
`Activity`�Ͳ���˵������������������Ϊ�˵Ͱ汾���ݶ������������ģ����Ƕ���v7���£� ~~ActionBarActivity~~�ѱ������������־�֪����ActionBar~������`5.0`�󣬱�Google�����ˣ������� ToolBar...������������Android Studio����һ��`Activity`Ĭ�ϼ̳еĻ��ǣ�**`AppCompatActivity`**! ��Ȼ��Ҳ����ֻд`Activity`������AppCompatActivity�������ṩ��һЩ�µĶ������ѣ� 

##3. �������л���״̬���������

����App�������л���ʱ������ٵ�ǰ��`Activity`Ȼ�����´���һ����������������������� ��ÿ�������ﶼ��Ӵ�ӡLog����䣬�������жϣ��ֻ�����һ����ťһ��TextView�����ť���޸�TextView �ı���Ȼ��������л���������ķ���TextView�ı����֮ǰ�������ˣ� �������л�ʱAct�������������ڣ�
>**onPause-> onStop-> onDestory-> onCreate->onStart->onResume**

###���ں������л����������������⣺

**1. ��ֹ��Ļ�������Զ��л�**

�����ܼ򵥣���`AndroidManifest.xml`��Ϊ`Activity`���һ�����ԣ� `android:screenOrientation`�� ��������ѡֵ��

>* `unspecified`:**Ĭ��ֵ**, ��ϵͳ���ж���ʾ����.�ж��Ĳ����Ǻ��豸��صģ����Բ�ͬ���豸���в�ͬ����ʾ����
* `landscape`:������ʾ����ȸ�Ҫ����
* `portrait`:������ʾ(�߱ȿ�Ҫ��)
* `user`:�û���ǰ��ѡ�ķ���
* `behind`:�͸�Activity������Ǹ�Activity�ķ���һ��(��Activity��ջ�е�)
* `sensor`:������ĸ�Ӧ��������������û���ת�豸����Ļ��������л���
* `nosensor`:���������Ӧ���������Ͳ��������û���ת�豸�������ˣ�"unspecified"���ó��⣩��

**2. ������ʱ����ز�ͬ�Ĳ���**

����**1��׼�����ײ�ͬ�Ĳ���**

����Android���Լ����ݺ��������ز�ͬ���֣� �������������ļ��У�layout-land����,layout-port���� Ȼ��������ײ����ļ��������ļ�����ļ���һ����Android�ͻ������жϣ�Ȼ�������Ӧ�����ˣ�

����**2���Լ��ڴ����н����ж�**

�����Լ������ʲô�ͼ���ʲô������һ������onCreate()�����м��ز����ļ��ģ����ǿ���������Ժ�������״̬�����жϣ��ؼ��������£�
>```android
if (this.getResources().getConfiguration().orientation == Configuration.ORIENTATION_LANDSCAPE){  
     setContentView(R.layout.����);
}else if (this.getResources().getConfiguration().orientation ==Configuration.ORIENTATION_PORTRAIT) {  
    setContentView(R.layout.����);
}
```

**3. ״̬��������**

����ͨ��һ��`Bundle savedInstanceState`����������ɣ� �������ķ�����
>```android
onCreate(Bundle savedInstanceState);
onSaveInstanceState(Bundle outState);
onRestoreInstanceState(Bundle savedInstanceState);
```

������ֻ��д`onSaveInstanceState()`�����������bundle��д�����ݣ����磺
> savedInstanceState.putInt("num",1);

������Ȼ������`onCreate`����`onRestoreInstanceState`�оͿ����ó�����洢�����ݣ�������֮ǰҪ�ж����Ƿ�Ϊ`null`Ŷ��
> savedInstanceState.getInt("num");

##4. Activity�������ݴ���

![Activity�������ݴ���](http://www.runoob.com/wp-content/uploads/2015/08/7185831.jpg "Activity�������ݴ���")

**`ע��`�� ʹ��Bundle��������ʱ��Bundle�Ĵ�С�������Ƶģ�Ҫ��`< 0.5MB`������������ֵ���ͻᱨ`TransactionTooLargeException`�쳣�ġ�**

##5. ���Activity֮��Ľ���

1. ʹ��`startActivityForResult(Intent intent,int requestCode)`������һ��`Activity`��������A��ʹ�ø÷�������B
2. ��������`Activity`����д`onActivityResult(int requestCode,int resultCode,Intent data)`,������A����д�÷���������`requestCode`�����������ڸ�`Activity`�в�ͬ��������ʽ������������ͬ��ť����ͬһ��`Activity`,���ݵ����ݿ��ܲ�ͬ������Ϳ��������`requestCode`������`resultCode`����`Activity`ͨ��`setResult()`���ص���
3. ����Activity����д `setResult(int resultCode,Intent data)`

##6. ����Activityȫ���ķ�����

**1.��������ActionBar**

������`Activity`��`onCreate()`�����е���`getActionBar.hide()`����

**2.ͨ��`requestWindowFeature`����**
����
>`requestWindowFeature(Window.FEATURE_NO_TITLE); `

����**�ô�����Ҫ��setContentView ()֮ǰ���ã���Ȼ�ᱨ������**

**3.ͨ��AndroidManifest.xml��theme**

��������Ҫȫ����Activity�ı�ǩ������
>`theme = @android:style/Theme.NoTitleBar.FullScreen`

##7. onWindowFocusChanged�������ã�

�����������¹ٷ�����������Ľ��ܣ�

![onWindowFocusChanged](http://www.runoob.com/wp-content/uploads/2015/08/17084157.jpg "")

�������ǣ���`Activity`�õ�����ʧȥ�����ʱ�򣬾ͻ�ص��÷����������������`Activity`�Ƿ������ϣ��Ϳ����õ����������~ �������˽�Ŀ��Ʋ�����ƪ���£� [onWindowFocusChanged�������](http://blog.csdn.net/yueqinglkong/article/details/44981449)

##8. Activity��Window��View�Ĺ�ϵ

![Activity��Window��View�Ĺ�ϵ](http://www.runoob.com/wp-content/uploads/2015/08/93497523.jpg "")

**���̽�����** Activity����startActivity���������attach������Ȼ����PolicyManagerʵ��һ��Ipolicy�ӿڣ�����ʵ��һ��Policy���󣬽��ŵ���makenewwindow(Context)�������÷����᷵��һ��PhoneWindow���󣬶�PhoneWindow ��Window�����࣬�����PhoneWindow����һ��DecorView���ڲ��࣬������Ӧ�ô��ڵĸ�View����View���ϴ� ֱ�ӿ���Activity�Ƿ���ʾ(������˾��ԭ��..)���ðɣ�����������һ��LinearLayout��������������FrameLayout���Ƿֱ�����װActionBar��CustomView��**������setContentView()���صĲ��־ͷŵ����CustomView��**��

##9. Activity�����ּ���ģʽ���

![Activity���ּ���ģʽ](http://www.runoob.com/wp-content/uploads/2015/08/50179298.jpg "")

**1. standardģʽ**

������׼����ģʽ��Ҳ��activity��Ĭ������ģʽ��������ģʽ��������activity���Ա����ʵ����������ͬһ�������п��Դ��ڶ��activity��ʵ����ÿ��ʵ�����ᴦ��һ��Intent�������Activity A������ģʽΪstandard������A�Ѿ���������A���ٴ�����Activity A��������startActivity��new Intent��this��A.class����������A�������ٴ�����һ��A��ʵ��������ǰ�ėC�е�״̬ΪA-->A��

![standard-1](http://www.jcodecraeer.com/uploads/20150520/1432087372621766.jpg "")

![standard-2](http://www.jcodecraeer.com/uploads/20150520/1432087374604123.jpg "")

**2. singleTopģʽ**

�������һ����singleTopģʽ������Activity��ʵ���Ѿ�����������ջ��ջ���� ��ô���������Activityʱ�����ᴴ���µ�ʵ������������λ��ջ�����Ǹ�ʵ���� ���һ���ø�ʵ����**onNewIntent()**������Intent���󴫵ݵ����ʵ���С� ������˵�����A������ģʽΪsingleTop������A��һ��ʵ���Ѿ�������ջ���У� ��ô�ٵ���startActivity��new Intent��this��A.class��������Aʱ�� �����ٴδ���A��ʵ������������ԭ����ʵ�������ҵ���ԭ��ʵ����onNewIntent()������ ��ʱ����ջ�л�������һ��A��ʵ���������singleTopģʽ������activity��һ��ʵ�� �Ѿ�����������ջ�У����ǲ���ջ������ô������Ϊ��standardģʽ��ͬ��Ҳ�ᴴ�����ʵ����

![singleTop](http://www.jcodecraeer.com/uploads/20150520/1432087389219419.jpg "")

**3. singleTaskģʽ**

����ֻ������ϵͳ����һ��Activityʵ�������ϵͳ���Ѿ�����һ��ʵ���� �������ʵ���������ƶ���������ͬʱintent����ͨ��**onNewIntent()**���͡� ���û�У���ᴴ��һ���µ�Activity���÷��ں��ʵ������С�

![singleTask](http://www.jcodecraeer.com/uploads/20150520/1432087394416117.jpg "")

**4. singleInstanceģʽ**

������֤ϵͳ���۴��ĸ�Task����Activity��ֻ�ᴴ��һ��Activityʵ��,�����������µ�Taskջ����Ҳ����˵����ʵ������������activity���Զ���������һ��Task�С� ���ٴ�������activity��ʵ��ʱ���������Ѵ��ڵ������ʵ�������һ�������ʵ����onNewIntent()��������Intentʵ�����ݵ���ʵ���С���singleTask��ͬ��ͬһʱ����ϵͳ��ֻ�����һ��������Activityʵ����

![singleInstance](http://www.jcodecraeer.com/uploads/20150520/1432087655129646.jpg "")

--
�ο��ĵ���
* [Activity��ѧէ��](http://www.runoob.com/w3cnote/android-tutorial-activity.html)
* [Activity�����ž�](http://www.runoob.com/w3cnote/android-tutorial-activity-start.html "")
* [Activity��������](http://www.runoob.com/w3cnote/android-tutorial-activity-intro.html "")