#BroadcastReceiver��ѧէ��

`Android` `BroadcastReceiver`

--
##1. ���ֹ㲥���ͣ�

![���ֹ㲥����](http://www.runoob.com/wp-content/uploads/2015/08/72916726.jpg "")

##2. ����ϵͳ�㲥

###1) ����ע��㲥�ķ�ʽ

����ϵͳ��ĳЩʱ��ᷢ����Ӧ��ϵͳ�㲥����������ͻ��߳��㣬�������꣬������������뷨�ı�ȡ��������Ǿ��������ǵ�APP����ϵͳ�㲥�� ����֮ǰ������ҪΪ���ǵ�APPע��㲥������Ŷ����ע��ķ����ַ�Ϊ�������֣�**��̬**��**��̬**��

![��̬ע��㲥](http://www.runoob.com/wp-content/uploads/2015/08/17322218.jpg "")
![��̬ע��㲥](http://www.runoob.com/wp-content/uploads/2015/08/93737904.jpg "")

###2) ��̬ע��㲥ʵ��

��������ı仯�����

**MyBRReceiver.java**

```java
public class MyBRReceiver extends BroadcastReceiver{
    @Override
    public void onReceive(Context context, Intent intent) {
        Toast.makeText(context,"����״̬�����ı�~",Toast.LENGTH_SHORT).show();
    }
}
```

**MainActivity.java�ж�̬ע��㲥��**

```java
public class MainActivity extends AppCompatActivity {

    MyBRReceiver myReceiver;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        // ���Ĳ��ִ���
        myReceiver = new MyBRReceiver();
        IntentFilter itFilter = new IntentFilter();
        itFilter.addAction("android.net.conn.CONNECTIVITY_CHANGE");
        registerReceiver(myReceiver, itFilter);
    }

    //�����˽��㲥ȡ����Ŷ~
    @Override
    protected void onDestroy() {
        super.onDestroy();
        unregisterReceiver(myReceiver);
    }
}
```

**ȱ�㣺**

������̬�㲥��Ҫ��**App�Ѿ�����**������²ſ��Խ��չ㲥������������Ҫ��App��û������������»��ܽ��չ㲥���Ǿ���Ҫʹ��**��̬ע��㲥**�ķ�ʽ�ˡ�

###3) ��̬ע��㲥ʵ��

��������������

**1. �Զ���һ��BroadcastReceiver����дonReceive���������**

```java
public class BootCompleteReceiver extends BroadcastReceiver {
    private final String ACTION_BOOT = "android.intent.action.BOOT_COMPLETED";
    @Override
    public void onReceive(Context context, Intent intent) {
    if (ACTION_BOOT.equals(intent.getAction()))
        Toast.makeText(context, "�������~", Toast.LENGTH_LONG).show();
    }
}
```
**2.��AndroidManifest.xml�жԸ�BroadcastReceiver����ע�ᣬ��ӿ����㲥��intent-filter!
���ˣ������˼���android.permission.RECEIVE_BOOT_COMPLETED��Ȩ��Ŷ��**

```xml
<receiver android:name=".BootCompleteReceiver">
    <intent-filter>
        <action android:name = "android.intent.cation.BOOT_COMPLETED">
    </intent-filter>
</receiver>

<!-- Ȩ�� -->
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>
```
**ע��**��

����Android 4.3���ϵİ汾������������װ��SD���ϵģ�������ĳ����ǰ�װ��SD�� �ģ��ͻ��ղ��������㲥��

###4) ʹ�ù㲥��ע������

����**��Ҫ�ڹ㲥����ӹ����߼����߽����κκ�ʱ����**,��Ϊ��**�㲥���ǲ��������̵߳�**, ��`onReceiver()`�������нϳ�ʱ��`(����10��)`��û�н����Ļ�����ô����ᱨ��**`(ANR)`**, �㲥�����ʱ����ݵ���һ������������Ľ�ɫ,��������Service,Notification��ʾ, Activity�ȣ�

##3. ����ȫ�ֹ㲥

###1) ��η���

**a. ���͹㲥ǰ��Ҫ�ȶ���һ���㲥��������**
* �Զ���һ��BroadcastReceiver����дonReceive()����
* ��AndroidManifest.xml��ע���BroadcastReceiver
* ��AndroidManifest.xml�ж�Intent-filterͨ��`android:priority="100"`���������ȼ���ֵԽ�������ȼ�Խ�ߣ�Խ�Ƚ��ܵ��㲥�����ȼ���ѡֵ�ķ�Χ��**`-1000~1000`**
* ����`����㲥`�������Ե���`abortBroadcast()`�ضϹ㲥�ļ������ݡ�

**b. ���͹㲥**
* **��׼�㲥**��`sendBroadcast(intent) `
* **����㲥**��`sendOrderedBroadcast(intent,null)`

###2) ���͹㲥

**1. MyBroadcastReceiver.java**
```java
public class MyBroadcastReceiver extends BroadcastReceiver {
    private final String ACTION_BOOT = "com.example.broadcasttest.MY_BROADCAST";
    @Override
    public void onReceive(Context context, Intent intent) {
        if(ACTION_BOOT.equals(intent.getAction()))
        Toast.makeText(context, "�յ������~",Toast.LENGTH_SHORT).show();
    }
}
```

**2. Ȼ��AndroidManifest.xml��ע���£�д��Intent-filter��**
```xml
<receiver android:name=".MyBroadcastReceiver">
    <intent-filter>
        <action android:name="com.example.broadcasttest.MY_BROADCAST"/>
    </intent-filter>
</receiver>
```

**3. ��MainActivity.java�з��͹㲥**
```java
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Button btn_send = (Button) findViewById(R.id.btn_send);
        btn_send.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
            // ���ͱ�׼�㲥
                sendBroadcast(new Intent("com.example.broadcasttest.MY_BROADCAST"));
            // ��������㲥
             sendOrderedBroadcast(new Intent("com.example.broadcasttest.MY_BROADCAST"),null);
            }
        });
    }
}
```

**4. ȫ�ֹ㲥��ȱ�㣺**

���������õ��Ķ���**ȫ�ֹ㲥**��Ҳ��������Ӧ��Ҳ���յ����ǵĹ㲥���������ܻ�����һЩ**��ȫ������**��

##4. ���ͱ��ع㲥

###1) �����÷���
ʹ��`LocalBroadcastManager`������㲥��
* ����`LocalBroadcastManager.getInstance()`���ʵ��������`localBrManager`
* ����`localBrManager.registerReceiver()`ע��㲥
* ����`localBrManager.sendBroadcast()`���͹㲥
* ����`localBrManager.unregisterReceiver()`ȡ��ע��

###2) ע�����
* ���ع㲥**�޷�ͨ����̬ע��**�Ľ�����������
* �ڹ㲥������`Activity`�Ļ�����ҪΪ`intent`����`FLAG_ACTIVITY_NEW_TASK`�ı�ǣ���Ȼ�ᱨ����Ϊ��Ҫһ��ջ������´򿪵�Activity
* �㲥�е�����`Alertdialog`�Ļ�����Ҫ���öԻ��������Ϊ`TYPE_SYSTEM_ALERT`����Ȼ�޷�����

###3) ���͹㲥

**1. MyBcReceiver.java**

```java
public class MyBcReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(final Context context, Intent intent) {
        AlertDialog.Builder dialogBuilder = new AlertDialog.Builder(context);
        dialogBuilder.setTitle("���棺");
        dialogBuilder.setMessage("�����˺��ڱ𴦵�¼�������µ�½~");
        dialogBuilder.setCancelable(false);
        dialogBuilder.setPositiveButton("ȷ��",
                new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialog, int which) {
                        ActivityCollector.finishAll();
                        Intent intent = new Intent(context, LoginActivity.class);
                        intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);//intent���FLAG_ACTIVITY_NEW_TASK�ı�ǣ���Ȼ�ᱨ��
                        context.startActivity(intent);
                    }
                });
        AlertDialog alertDialog = dialogBuilder.create();
        alertDialog.getWindow().setType(
                WindowManager.LayoutParams.TYPE_SYSTEM_ALERT);  //dialog����TYPE_SYSTEM_ALERT����Ȼ�޷�����
        alertDialog.show();
    }
}
```

**ע��**

����������`AndroidManifest.xml`�м���ϵͳ�Ի���Ȩ�ޣ� `< uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />`

**2. ��MainActivity�У�ʵ����localBroadcastManager�����������ز�������������ʱ ע��unregisterReceiver��**

```java
public class MainActivity extends BaseActivity {

    private MyBcReceiver localReceiver;
    private LocalBroadcastManager localBroadcastManager;
    private IntentFilter intentFilter;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        localBroadcastManager = LocalBroadcastManager.getInstance(this);  // ���LocalBroadcastManager��ʵ��

        // ��ʼ���㲥�����ߣ����ù�����
        localReceiver = new MyBcReceiver();
        intentFilter = new IntentFilter();
        intentFilter.addAction("com.jay.mybcreceiver.LOGIN_OTHER");
        localBroadcastManager.registerReceiver(localReceiver, intentFilter); //ע��㲥

        Button btn_send = (Button) findViewById(R.id.btn_send);
        btn_send.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent("com.jay.mybcreceiver.LOGIN_OTHER");
                localBroadcastManager.sendBroadcast(intent);  //���͹㲥
            }
        });
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        localBroadcastManager.unregisterReceiver(localReceiver); // ȡ��ע�ᣬһ��Ҫ�ǵ�ȡ��ע��㲥��
    }
}
```
##5. Android 4.3���ϰ汾�������������㲥����������

������Android 4.3���ϵİ汾���������ǽ�Ӧ�ð�װ��SD�ϣ����Ƕ�֪����ϵͳ���� ���һС��ʱ��󣬲�װ��SD���ģ��������ǵ�Ӧ�þͿ��ܼ�����������㲥�ˣ� ����������Ҫ�ȼ��������㲥�ּ���SD�����ع㲥��
���⣬��Щ�ֻ����ܲ�û��SD���������������㲥�������ǲ���д��ͬһ��`Intetn-filter`�� ����Ӧ��д�����������ô������£�

```xml
<receiver android:name=".MyBroadcastReceiver">
    <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
    </intent-filter>
    <intent-filter>
        <action android:name="ANDROID.INTENT.ACTION.MEDIA_MOUNTED"/>
        <action android:name="ANDROID.INTENT.ACTION.MEDIA_UNMOUNTED"/>
        <data android:scheme="file"/>
    </intent-filter>
</receiver>
```


--
**�ο����ף�**
* [BroadcastReceiverţ��С��](http://www.runoob.com/w3cnote/android-tutorial-broadcastreceiver.html "")
* [BroadcastReceiver�Ҷ���ţ](http://www.runoob.com/w3cnote/android-tutorial-broadcastreceiver-2.html "")