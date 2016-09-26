#Activity״̬�ָ��ķ���

`Android`

--

## 1. Activity״̬�ָ�

��дActivity������������
*  onSaveInstanceState(Bundle outState)   
*  onCreate()
*  onRestoreInstanceState()

### 1. onSaveInstanceState(Bundle outState)

1. �������õ�ʱ����
    * ϵͳ��������Activity�ع�ǰ����
    * ��Դ���㣬ϵͳ��Ϊ���Activity�п��ܱ�����ʱ�ᱻ����
    * ����outState����ϵͳ����ά���ʹ��룬���������Ҫ���ֵ�����
    
2. Ҫ��
    * outState��һ��key��value����ʽ

##2. ��ֹActivity״̬�ָ�

�޸�android:configChanges���ԣ�
*  �����manifest��Ϊactivityָ���˸����ԣ���ô���������е����ñ仯�����ٵ���activity���ع�
* �ᴥ��activity��**`onConfigurationChanged()`**�����Ļص�
* ������Ҳ��ʹ���������л��������activity���������ı��Լ�������

##3. �����ع���׼��
* ����ͨ��configChanges���Խ�ֹ���ع���Ҳ�޷���ֹ���ڴ治��ʱactivity������
* ���Ա��뿼�Ǳ��ع�ʱ���߼�
* ����ͨ��config�ı���ģ�������ع�

##4. Android�������л�С��
������ϵ�����С����⼸������ص��龰��

1. **������Activity��android:configChangesʱ**�����������µ��ø����������ڣ��к���ʱ��ִ��һ�Σ�������ʱ��ִ�����Σ���������4.0�豸�Ϸ����к�������������ִ��һ�Σ�����������˵����ִ�����ε��������֪���Ƿ���ǰ�汾�ֻ�������������
2. **����Activity��android:configChanges="orientation"ʱ**���������ǻ����µ��ø����������ڣ��кᡢ����ʱֻ��ִ��һ�Σ�
3. **����Activity��android:configChanges="orientation|keyboardHidden"ʱ**�������������µ��ø����������ڣ�ֻ��ִ��onConfigurationChanged������

**ע�⣺** ��
* **������������Android3.2��ǰ**�����ȱ����**keyboardHidden**ѡ����ܷ�ֹActivity������������Ҳ�Ͳ���ִ��onConfigurationChanged�����ˡ�
* **��Android3.2֮��**���������**screenSize**���Բſ������ε���Activity���������ڣ�����һЩ�豸���ײ���Բ���ҪkeyboardHidden��ֻҪscreenSize�Ϳ����ˣ����Ǳ���������Ǽ�������keyboardHidden�ɣ���



##5. android:screenOrientation����ֵ

����ȱʡ����£����ֻ�û�йرպ������л�����ʱ��ϵͳһ�������������л�����ǰ���App����ͻ���к������л������ں���������ĳߴ�Ȳ�����ͬ�����Ծ�Ҫ�Ժ��������в�ͬ�����䡣�еĿ�����Ϊ�˱��ⲻ��Ҫ���鷳������App��ֹ�������������Ҫ��`AndroidManifest.xml`������`activity`��`android:screenOrientation`������ʵ�֡�

��������������һ��`android:screenOrientation`������ֵ��

|����ֵ|˵��|
|:--|:--|
|**unspecified**|Ĭ��ֵ����ϵͳ���ж���ʾ�����ж��Ĳ��Ժ��豸�йأ����Բ�ͬ���豸���в�ͬ����ʾ����|
|**landscape**|������ʾ(��� > �߶�)|
|**portrait**|������ʾ(��� < �߶�)|
|**user**|�û���ǰ��ѡ�ķ���|
|**behind**|�͸�Activity�µ��Ǹ�Activity�ķ��򱣳�һ��(��Activity��ջ��)|
|**sensor**|������ĸ�Ӧ��������������û���ת�豸���ᵼ����Ļ�������л�|
|**nosensor**|����������Ӧ���������Ͳ��������û���ת�豸��������("unspecified"����)|

##6. ����Activity�ĺ������л�

����ȱʡ��r�£�Activityÿ�κ������л��������µ���һ��`onPause--> onStop--> onDestory--> onCreate--> onStart--> onResume`�������Ӷ�����ԭ����Activity���󣬴����µ�Activity����������Ϊͨ������£�������֮���л�������Ŀ�߻ᷢ��ת�����Ӷ�����Ҫ��ͬ�Ĳ��֡�

��������Ĳ����л�����ͨ���������ַ�ʽ��ʵ�֣�
* ��`res`Ŀ¼�½���`layout-land`��`land-port`Ŀ¼����Ӧ��layout�ļ������䡣`layout-land`�Ǻ�����layout��`layout-port`��������layout���������л�ʱϵͳ�Լ������Activity��`onCreate`�������Ӷ����ݵ�ǰ����Ļ�����Զ�������Ӧ�Ĳ����ļ���
* Ҳ�����ڴ������жϵ�ǰ�ĺ����������Ȼ�������Ӧ�Ĳ����ļ������磺
```java
@Override
protected void onCreate(Bundle icicle) {
 super.onCreate(icicle);

 int mCurrentOrientation = getResources().getConfiguration().orientation;
 if ( mCurrentOrientation == Configuration.ORIENTATION_PORTRAIT ) {
         // If current screen is portrait
         Log.i("info", "portrait"); /* ���� */
         setContentView(R.layout.mainP);
 } else if ( mCurrentOrientation == Configuration.ORIENTATION_LANDSCAPE ) {
         //If current screen is landscape
         Log.i("info", "landscape"); // ����
         setContentView(R.layout.mainL);
 }
 init();//��ʼ������ֵ�Ȳ���
 findViews();//��ÿؼ�
}
``` 

��������Activity��δ�Ӵ��������±�Ȼ�������ݵĶ�ʧ�����»�ȡ�������û�����ǳ��Ϊ�˾���Ҫ���л�ǰ�����ݽ��б��棬�л�����������ݽ��лָ���
###1. onSaveInstanceState(Bundle outState)
����������Activity��ʼֹͣʱ��ϵͳ�����`onSaveInstanceState()`�Ա�����Activity���Ա�����м�ֵ�Լ��ϵ�״̬��Ϣ�� �˷�����Ĭ��ʵ�ֱ����й�Activity��ͼ��ε�״̬��Ϣ������ EditText С�����е��ı���ListView �Ĺ���λ�á�

����Ҫ����Activity�ĸ���״̬��Ϣ��������ʵ��`onSaveInstanceState()`������ֵ������� Bundle ���� ���磺
```java
static final String STATE_SCORE = "playerScore";
static final String STATE_LEVEL = "playerLevel";
...

@Override
public void onSaveInstanceState(Bundle savedInstanceState) {
    // Save the user's current game state
    savedInstanceState.putInt(STATE_SCORE, mCurrentScore);
    savedInstanceState.putInt(STATE_LEVEL, mCurrentLevel);

    // Always call the superclass so it can save the view hierarchy state
    super.onSaveInstanceState(savedInstanceState);
}
```
����������Activity����ǰ����֮�����´���ʱ�������Դ�ϵͳ��Activity���ݵ� Bundle �ָ��ѱ����״̬��`onCreate()` �� `onRestoreInstanceState()` �ص����������հ���ʵ��״̬��Ϣ����ͬ Bundle��

`onCreate()`�лָ����ݣ�
```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState); // Always call the superclass first

    // Check whether we're recreating a previously destroyed instance
    if (savedInstanceState != null) {
        // Restore value of members from saved state
        mCurrentScore = savedInstanceState.getInt(STATE_SCORE);
        mCurrentLevel = savedInstanceState.getInt(STATE_LEVEL);
    } else {
        // Probably initialize members with default values for a new instance
    }
    ...
}
```

����������ѡ��ʵ��ϵͳ�� `onStart()` ����֮����õ� `onRestoreInstanceState()` ����������onCreate() �ڼ�ָ�״̬�� **ϵͳֻ�ڴ���Ҫ�ָ����ѱ���״̬ʱ����`onRestoreInstanceState()` ������������� Bundle �Ƿ�Ϊ null��**
```java
public void onRestoreInstanceState(Bundle savedInstanceState) {
    // Always call the superclass so it can restore the view hierarchy
    super.onRestoreInstanceState(savedInstanceState);

    // Restore state members from saved instance
    mCurrentScore = savedInstanceState.getInt(STATE_SCORE);
    mCurrentLevel = savedInstanceState.getInt(STATE_LEVEL);
}
```
**Ҫ�ر�ǿ������**��`onSaveInstanceState` �������������ڷ�����Android ϵͳ**������֤��ɱ�� `activity`ǰһ��������**��

�� `activity` �����̨���߱�����ʱ `onPause()` �ܻᱻ�������� `activity` ������ʱ `onStop()` �ܻᱻ�������� `onSaveInstanceState()` ���ᱻ���������������
* �� `activity B` ������ `activity A` ���棬������B������������Aδ��ɱ����ϵͳ����ΪA���������������ΪA�Ա�����ԭ�����û�������״̬��
* ���û������ؼ��� `activity B` ���ص� `activity A`��ϵͳ����ΪB���������������ΪB��ʵ���ѱ����٣�����û�б�Ҫ�ָ�״̬��

**��תʱ�����ĵ�������:**
```
��ת�����ˣ�activity ʵ�������٣�
onPause() // �洢��������
onSaveInstanceState(Bundle) // �洢��ʱ���ݣ���onStopǰ������
onStop()
onDestroy()

�ؽ� activity ʵ����
onCreate(Bundle) // ��ȡ�ݴ�����
onStart()
onRestoreInstanceState(Bundle) // Ҳ�������ȡ�ݴ����ݣ���onStart�󱻵���
onResume() // ����Ӧ��onPause�Ļָ��Ĺ���
```
###2. onRetainNonConfigurationInstance

�������Activity�ؽ���Ҫ�ķѴ�����Դ����Ҫ�������絼��ʱ��ܳ�������ʵ��`onRetainNonConfigurationInstance()`���������������ȱ��浽һ�������������������
```java
@Override 

public Object onRetainNonConfigurationInstance() { 
    final MyDataObject data = collectMyLoadedData(); 
    return data; 
}
```
��onCreate()�����е���`getLastNonConfigurationInstance()`����ȡ`onRetainNonConfigurationInstance()`���������:
```java
@Override
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.main);

    final MyDataObject data = (MyDataObject) getLastNonConfigurationInstance();
    if (data == null) {//��ʾ��������Configuration�ı䴥����onCreate()
        data = loadMyData();
    }
    ...
}
```
**��Ҫע�����:**

�������ǲ�Ӧ�ñ�����Щ����Activity�����ݣ�����Drawable��Adapter��View�����κ���Context����������ݣ������ᵼ���ڴ�й¶��

##7. ������Activity�ĺ������л�

������Ȼ����ActivityΪ�����ṩ�˱������ݺͶ�ȡ���ݵķ�ʽ����������Ҳ����ͨ��������Activity�ķ�ʽ��Ӧ�Ժ��������л���AndroidҲΪ�����ṩ�˽������������ͨ��onConfigurationChanged���غ������任���Ӷ����б�Ҫ�����²��ֺ��л������������������£�

1. ��AndroidManifest��Ϊ��Ӧ��Activity����`android:configChanges`���ԣ�ָ����Ҫ���Ե�Configuration���ԣ��Ӷ�ʹActivity�������ؽ����̣��������£�
    * **Android3.2��ǰ**
    
        ```
        android:configChanges="orientation|keyboardHidden"
        ```

##8. setRequestOrientation()

--
[�ο�]
* [Android�������л�С��](http://www.cnblogs.com/franksunny/p/3714442.html)
* [���´���Activity](https://developer.android.com/training/basics/activity-lifecycle/recreating.html#SaveState)
* [�����Android�豸��תʱ�ݴ������Ա�����ǰ�Ľ���״̬��](https://segmentfault.com/a/1190000003965285#articleHeader7)
* [Android ����������л��¼�](http://ipjmc.iteye.com/blog/1265991)

