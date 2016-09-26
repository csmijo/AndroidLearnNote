#Service��ѧէ��

`Android` `Service`

--

##1. Service����������

![service����������](http://www.runoob.com/wp-content/uploads/2015/08/11165797.jpg "")

##2. �������ڽ���

����ͼ���Կ�����Android��ʹ��Service�ķ�ʽ�����֣�
* **startService()** ����service
* **bindService()** ����service
* �������ַ�������ͬʱʹ��

###1����ط������

* **onCreate()**����Service��һ�α������������ص��÷������÷�������������������**`ֻ�����һ��`**��
* **onDestory()**����Service���ر�ʱ��ص��÷������÷���**`ֻ��ص�һ��`**��
* **onStartCommand(intent,flag,startId)**�����ڰ汾��`onStart(intent,startId)`, ���ͻ��˵���`startService(Intent)`����ʱ��ص����ɶ�ε���StartService�������������ٴ����µ�Service���󣬶��Ǽ�������ǰ�������Service���󣬵�������ص�`onStartCommand()`������
* **IBinder onOnbind(intent)**���÷�����Service������ʵ�ֵķ������÷����᷵��һ�� IBinder����appͨ���ö�����Service�������ͨ�ţ�
* **onUnbind(intent)**������Service�ϰ󶨵����пͻ��˶��Ͽ�ʱ��ص��÷�����

###2��startService����service 

1. �״������ᴴ��һ��Serviceʵ��,���ε���`onCreate()`��`onStartCommand()`����,��ʱService ��������״̬,����ٴε���StartService����Service,�������ٴ����µ�Service����, ϵͳ��ֱ�Ӹ���ǰ�洴����Service����,��������`onStartCommand()`������
2. **��������Service�����ĵ������ޱ�Ȼ����ϵ**,����˵�������߽������Լ�����������, ����ֻҪ������stopService,��ôService���ǻ�������е�!
3. **���������˶��ٴ�Service,ֻ�����һ��StopService����ͣ��Service**

###3) bindService����service 

1. ���״�ʹ��bindService��һ��Serviceʱ,ϵͳ��ʵ����һ��Serviceʵ��,��������`onCreate()`��`onBind()`����,Ȼ������߾Ϳ���ͨ��IBinder��Service���н�����,�˺�����ٴ�ʹ��bindService��Service,ϵͳ���ᴴ���µ�Seviceʵ��,**Ҳ�����ٵ���`onBind()`����**,ֻ��ֱ�Ӱ�IBinder���󴫵ݸ������������ӵĿͻ���!
2. ������ǽ�������İ�,ֻ�����`unbindService()`,��ʱ`onUnbind()`��`onDestory()`�������ᱻ����!����һ���ͻ��˵����,�����Ƕ���ͻ��˰�ͬһ��Service�Ļ�,������� ��һ���ͻ���ɺ�service֮��Ļ����������� `unbindService()` ����������󶨡������еĿͻ��˶���service����󶨺�ϵͳ������service��������serviceҲ��`startService()`����������
3. ����,���������������ͬ,bindServiceģʽ�µ�Service����������໥������,�������Ϊ **"һ�������ϵ�����",Ҫ��һ����**,��bindService��,һ������������,��ôServiceҲ������ֹ!

**ͨ��BindService����Serviceʱ���õ�Context��bindService�Ľ���** `bindService(Intent Service,ServiceConnection conn,int flags)`

* **service**: ͨ����intentָ��Ҫ������Service
* **conn**: ServiceConnection����,�û�������������Service����������, ���ӳɹ��ص��ö����е�`onServiceConnected(ComponentName,IBinder)`����; ���Service���ڵ����������쳣��ֹ��������ԭ����ֹ,����Service������߼�Ͽ�����ʱ����`onServiceDisconnected(CompanentName)`������**����ͨ��unBindService() �����Ͽ������������������**!
* **flags**: ָ����ʱ�Ƿ��Զ�����Service(���Service��δ����), ����������0(���Զ�����),BIND_AUTO_CREATE(�Զ�����)

###4) startService����service��bindService��

�������Service�Ѿ���ĳ���ͻ���ͨ��`startService()`����,�������������ͻ����ٵ���`bindService()`�󶨵���Service��,����`unbindService()`��������,�ٵ���`bindService()`�󶨵�Service�Ļ�,��ʱ���������������ڷ�������:
>`onCreate( )->onStartCommand( )->onBind( )->onUnbind( )->onRebind( )`

**ǰ����**:**onUnbind()��������true!!!** ��������ֶ������ɻ���,������`unbindService()`��Service����Ӧ�õ���`onDistory()`����ô!��ʵ������Ϊ���Service�������ǵ�`startService()`�������� ,���������`onUnbind()`����ȡ����,ServiceҲ�ǲ�����ֹ��!

**�ó��Ľ���**: ��������ʹ��`bindService()`����һ��������Service,ע�����Ѿ�������Service!!! ϵͳֻ�ǽ�Service���ڲ�IBinder���󴫵ݸ�Activity,�����ὫService���������� ��Activity��,��˵���`unBindService()`����ȡ����ʱ,ServiceҲ���ᱻ���٣�

##3. bindService����service�������

* **ServiceConnection����**:������������Service����������,����ɹ�����,�ص�`nServiceConnected()`,����쳣��ֹ��������ԭ����ֹ����Service������߶Ͽ� ������ص�`onServiceDisconnected()`����,����`unBindService()`������ø÷���!
* `onServiceConnected()`��������һ��IBinder����,�ö��󼴿�ʵ���뱻��Service ֮���ͨ��!�����ٿ���Service��ʱ,Ĭ����Ҫʵ��`IBinder onBind()`����,�÷������ص�IBinder����ᴫ��ServiceConnection��������Ϊ`onServiceConnected()`�����Ĳ���,���ǾͿ���������ͨ�����IBinder��Service����ͨ��!

**�ܽ᣺**
>Step 1. ���Զ����Service�м̳�Binder,ʵ���Լ���IBinder����

>Step 2:ͨ��`onBind()`���������Լ���IBinder����

>Step 3:�ڰ󶨸�Service�����ж���һ��ServiceConnection����,��д��������, `onServiceConnected()`��`onDisconnected()`��Ȼ��ֱ�Ӷ�ȡIBinder���ݹ����Ĳ�������!

##4. IntentService��ʹ��

�����������ֱ�ӰѺ�ʱ�̷߳���Service��`onStart()`�����У���Ȼ�������������������������׻�����ANR�쳣(Application Not Response)����Android�ٷ�����������Service�ģ�
![IntentService](http://www.runoob.com/wp-content/uploads/2015/08/71905858.jpg "")

**ֱ�ӷ��룺**
* Service����һ�������Ľ���,��������Ӧ�ó�����ͬһ��������
* Service����һ���߳�,��������ζ������Ӧ�ñ�����Service�н��к�ʱ����

�������Ǻ���Android�������ṩ�˽��������������Ʒ����������Ҫ����**IntentService**�� IntentService�Ǽ̳���Service�������첽�����һ����,��IntentService���� һ�������߳��������ʱ����,�����Intent��¼�������С�

**�������̣�**

�����ͻ���ͨ��`startService(Intent)`������IntentService; ���ǲ�����Ҫ�ֶ���������IntentService,������ִ�����,IntentService���Զ�ֹͣ; ��������IntentService���,ÿ����ʱ�������Թ������еķ�ʽ��IntentService�� `onHandleIntent()`�ص�������ִ��,����ÿ��ֻ��ִ��һ�������߳�,ִ����һ���ٵ�����

##5. һ���򵥵�ǰ̨�����ʵ��

����ѧ�����ڣ����Ƕ�֪��Serviceһ�㶼�������ں����ģ�����Service��ϵͳ���ȼ� ���ǱȽϵ͵ģ���ϵͳ�ڴ治���ʱ�򣬾��п��ܻ������ں�̨���е�Service����������������ǿ���ʹ��ǰ̨���񣬴Ӷ���Service��΢û��ô���ױ�ϵͳɱ������Ȼ�����п��ܱ�ɱ���ġ�**��ν��ǰ̨�������״̬����ʾ��Notification**��

ʵ������Ҳ�ܼ򵥣����岽�����£�
* ���Զ����Service���У���д`onCreate()`
* �����Լ���������Notification
* ������Ϻ󣬵���startForeground(1,notification����)���ɣ�

```java
public void onCreate()
{
    super.onCreate();
    Notification.Builder localBuilder = new Notification.Builder(this);
    localBuilder.setContentIntent(PendingIntent.getActivity(this, 0, new Intent(this, MainActivity.class), 0));
    localBuilder.setAutoCancel(false);
    localBuilder.setSmallIcon(R.mipmap.ic_cow_icon);
    localBuilder.setTicker("Foreground Service Start");
    localBuilder.setContentTitle("Socket�����");
    localBuilder.setContentText("��������...");
    startForeground(1, localBuilder.getNotification());
}
```

##6. �򵥶�ʱ�ĺ�̨�����ʵ��

��������������ǰ̨�����⣬ʵ�ʿ�����Service����һ�ֳ������÷�������ִ�ж�ʱ���� ������ѯ������ÿ���һ��ʱ�������һ�η�������ȷ�Ͽͻ���״̬���߽�����Ϣ���µȣ���Android�и������ṩ�Ķ�ʱ��ʽ�����֣�ʹ��**`Timer��`**��**`Alarm����`**��

����ǰ�߲��ʺ�����Ҫ�����ں�̨���еĶ�ʱ����CPUһ�����ߣ�Timer�еĶ�ʱ������޷����У�Alarm�򲻴�����������������л���CPU�Ĺ��ܣ����⣬ҲҪ����CPU ��������Ļ���ѣ�
###1. ʹ������:
* **Step 1:���Service��**

```java
 AlarmManager manager = (AlarmManager)getSystemService(ALARM_SERVICE);
```
* **Step 2:ͨ��set��ʽ���ö�ʱ����**

```java
int anHour = 2 * 1000;
long triggerAtTime = SystemClock.elapsedRealtime() + anHour;
manager.set(AlarmManager.RTC_WAKEUP,triggerAtTime,pendingIntent);
```
* **Step 3:����һ��Service��**

������onStartCommand()�п���һ�������̣߳����ڴ���һЩ��ʱ�߼�
* **Step 4������һ��Broadcast(�㲥)��**

�����㲥��������service�����һ��Ҫ��AndroidManifest.xml�ļ��ж�Service��Broadcast����ע�ᡣ

###2. ������⣺
>`set(int type,long startTime,PendingIntent pi)`

**1.type: �������ѡֵ:**

* **AlarmManager.ELAPSED_REALTIME**: �������ֻ�˯��״̬�²����ã���״̬������ʹ�����ʱ�䣨�����ϵͳ������ʼ����״ֵ̬Ϊ3; 
* **AlarmManager.ELAPSED_REALTIME_WAKEUP**: ������˯��״̬�»ỽ��ϵͳ��ִ����ʾ���ܣ���״̬������Ҳʹ�����ʱ�䣬״ֵ̬Ϊ2�� 
* **AlarmManager.RTC**: ������˯��״̬�²����ã���״̬������ʹ�þ���ʱ�䣬����ǰϵͳʱ�䣬״ֵ̬Ϊ1��
* **AlarmManager.RTC_WAKEUP**: ��ʾ������˯��״̬�»ỽ��ϵͳ��ִ����ʾ���ܣ���״̬������ʹ�þ���ʱ�䣬״ֵ̬Ϊ0; 
* **AlarmManager.POWER_OFF_WAKEUP**: ��ʾ�������ֻ��ػ�״̬��Ҳ������������ʾ���ܣ�������5��״̬���õ�����״̬֮һ�� ��״̬������Ҳ���þ���ʱ�䣬״ֵ̬Ϊ4��**������״̬������SDK�汾Ӱ�죬ĳЩ�汾����֧��**

**2.startTime:**

�������ӵĵ�һ��ִ��ʱ�䣬�Ժ���Ϊ��λ�������Զ���ʱ�䣬����һ��ʹ�õ�ǰʱ�䡣 **��Ҫע�����**,���������һ�����ԣ�type���������:
* �����һ��������Ӧ������ ʹ�õ������ʱ�䣨ELAPSED_REALTIME��ELAPSED_REALTIME_WAKEUP������ô���� �Ծ͵�ʹ�����ʱ�䣨�����ϵͳ����ʱ����˵��,���統ǰʱ��ͱ�ʾΪ: `SystemClock.elapsedRealtime()`��
* �����һ��������Ӧ������ʹ�õ��Ǿ���ʱ�� (RTC��RTC_WAKEUP��POWER_OFF_WAKEUP��,��ô�����Ծ͵�ʹ�þ���ʱ�䣬 ���統ǰʱ��ͱ�ʾΪ��`System.currentTimeMillis()`��

**3.PendingIntent**

�����������ӵ�ִ�ж��������緢��һ���㲥��������ʾ�ȵȡ�PendingIntent ��Intent�ķ�װ�ࡣ

###3. ��Ҫע�����:

* �����ͨ��`��������`��ʵ��������ʾ�Ļ��� PendingIntent����Ļ�ȡ��Ӧ�ò���`Pending.getService (Context c,int i,Intent intent,int j)`����;
* �����ͨ��`�㲥`��ʵ��������ʾ�Ļ��� PendingIntent����Ļ�ȡ��Ӧ�ò��� `PendingIntent.getBroadcast (Context c,int i,Intent intent,int j)`������
* ����ǲ���`Activity`�ķ�ʽ��ʵ��������ʾ�Ļ���PendingIntent����Ļ�ȡ ��Ӧ�ò��� `PendingIntent.getActivity(Context c,int i,Intent intent,int j) `������
* ��������ַ��������˵Ļ�����Ȼ���ᱨ�����ǿ�����������ʾЧ����

**����:**

������4.4�汾��(API 19),Alarm����Ĵ���ʱ����ܱ�ò�׼ȷ,�п��ܻ���ʱ,��ϵͳ ���ںĵ��Ե��Ż�,�����Ҫ׼ȷ������Ե���setExtra()����~

###4. ���Ĵ��룺

```java
public class LongRunningService extends Service {
    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }

    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        //���￪��һ���߳�,����ִ�о�����߼�����:
        new Thread(new Runnable() {
            @Override
            public void run() {
                Log.d("BackService", new Date().toString());
            }
        }).start();
        AlarmManager manager = (AlarmManager) getSystemService(ALARM_SERVICE);
        //�����Ƕ�ʱ��,�������õ���ÿ�������ӡһ��ʱ��=-=,�Լ���
        int anHour = 2 * 1000;
        long triggerAtTime = SystemClock.elapsedRealtime() + anHour;
        Intent i = new Intent(this,AlarmReceiver.class);
        PendingIntent pi = PendingIntent.getBroadcast(this, 0, i, 0);
        manager.set(AlarmManager.ELAPSED_REALTIME_WAKEUP, triggerAtTime, pi);
        return super.onStartCommand(intent, flags, startId);
    }
}
```

**AlarmReceiver.java**
```java
public class AlarmReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        Intent i = new Intent(context,LongRunningService.class);
        context.startService(i);
    }
}
```

##7. Service�Ļ���������

����**androidϵͳ�����ԭ��֮һ�ǣ���֤�û���app�����ܾõ�����**����������IOS��ȫ�෴�������ѧ���������ԣ����Ҳ�̸������������androidϵͳ�ж�Serviceʵ���Ļ������⡣

����androidϵͳ�У���ʣ���ڴ������ʱ��ϵͳΪ�˱�֤�û����ڽ��еĹ������������Լ�ϵͳ�ؼ��Ĺ����ܹ���������������Ѿ�ʹ�õ��ڴ���в��ֻ��գ������Щ������Ҫ�Ľ��̡���̨Task��Activityʵ����Serviceʵ���Ƚ������١������û���Service����ʱ���ܱ����յġ������ᵽ��android�������ѧ����app�����ܾõ����У����ԣ����������ڴ�Σ����ȥ֮��androidϵͳ���ٳ����ؽ����������ٵ�ʵ��������Service����Ϳ��Ա�ϵͳ�����´�����������֮ǰ�Ĺ�����

����Service �� `onStartCommand()` �����ķ���ֵ��һ��������ȡֵ�������⼸���е�һ��**Service.START_NOT_STICKY**��**Service.START_STICKY**��**Service.START_REDELIVER_INTENT**���⼸������ֵ��Ӱ�쵽androidϵͳ��Service���ؽ�����Ȼ�������Serviceָ���ǡ�����������Service���⼸��ֵ��Service�ؽ���Ӱ�����£�

|����ֵ|ϵͳ����|����|
|---|:---:|:----:|
|**Service.START_NOT_STICKY**| ���ϵͳ��Service��onStarnCommand�����ص���֮�������˸�Service��ϵͳ���������ؽ���Service��ֱ�����µ��������������|ϵͳ�Դ���Service��̬���ǣ����پ������ˣ�����ν|
|**Service.START_STICKY**|���ϵͳ��Service��onStarnCommand�����ص���֮�������˸�Service��ϵͳ���������´�����Service�Ķ��󣬻����µ��ø�Service��OnStartCommand���������Ǵ��ݽ�ȥ��Intent������һ��null|ϵͳ�Դ���Service��̬���ǣ����ڴ治��ô���ŵ�ʱ���ؽ���Service�����ǲ������������Intent���󣬶��Ǵ���null|
|**Service.START_REDELIVER_INTENT**|���ϵͳ��Service��onStarnCommand�����ص���֮�������˸�Service��ϵͳ���������´�����Service�Ķ��󣬻����µ��ø�Service��OnStartCommand���������Ұ�������ǰ�����һ��Intent ���󴫵ݽ�ȥ����Ҫ������Ҫ�ָ��ֳ��ĵط������������ļ�|ϵͳ�Դ���Service��̬���ǣ����ڴ治��ô���ŵ�ʱ���ؽ���Service�����һ������ǰ���һ��Intent�������´��ݽ�ȥ|


--
�ο����ף�

* [Service����](http://www.runoob.com/w3cnote/android-tutorial-service-1.html "")
* [Service����](http://www.runoob.com/w3cnote/android-tutorial-service-2.html "")
* [Android ��� Service �о�](http://android.jobbole.com/84450/)