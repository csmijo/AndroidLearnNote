# UiAutomator2ѧϰ�ʼ�

---


## 1. InstrumentationRegistry 

## 1.1 ���

����һ����¶��ע��ʵ�������� `instrumentation` ���н��̺����Ĳ��������ṩ��һ�����ķ������� `instrumentation`, `application context` �� `instrumentation` ����

![instrumentationRegistry_api.PNG](http://on9czqsf5.bkt.clouddn.com/instrumentationRegistry_api.PNG?2017-05-16-20-04-58)

**ע�⣺** ��Ͱ汾�� `Andriod 4.3` ���ϣ�Ҳ���� `API 18` ����


����ʵ�����룺

```
@Test
public void testCase() throws IOException{
    
    // ��ȡ����ʱ�Ĳ���
    Bundle args = InstrumentationRegistry.getArguments();
    // ��������б�����
    instrumentation.setStatus(100,args);
    
    // ��ȡ���԰��� Context
    Context testContext = InstrumentationRegistry.getContext();
    // ��ȡ����Ӧ�õ� Context
    Context targetContext = InstrumentationRegistry.getTargetContext();
    
    // ͨ�� Context ������һ�� Activity�����磺�����
    String url = "https://www.baidu.com";
    Intent i1 = new Intent(Intent.ACTION_VIEW);
    i1.setData(Uri.parse(url));
    i1.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
    testContext.startActivity(i1);
    
    // ͨ��Ŀ�� Context ���������Ź���
    Intent i2 = new Intent(Intent.ACTION_CALL);
    i2.setData(Uri.parse("tel:"+10086);
    i2.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
    targetContext.startActivity(i2);

    Bundle inputBundle = new Bundle();
    inputBundle.putString("key","value");
    // ע��һ�� Bundle
    InstrumentationRegistry.registerInstance(instrumentation,inputBundle);
    // ��������������
    instrumentation.sendStatus(110,inputBundle);
}
```



## 2. UiDevice ���� API

![UiDevice����APi.PNG](http://on9czqsf5.bkt.clouddn.com/UiDevice����APi.PNG?2017-05-16-20-17-13)

## 3. BySelector ��By ��̬��

### 3.1 BySelector �����

* **���ã�** ָ��ƥ�� UI Ԫ�صı�׼��������
* **ʹ�ã�** ͨ�� `UiDevice.findObject(BySelector)` ����ʹ��
* ���صĶ����� `UiObject2` ����

### 3.2 By �����

* **���ã�** ��һ��ʹ�ó����࣬ͨ���������Լ��ķ�ʽ���� `BySelector`��������Ҫ����ʱʹ�������﷨�ṩ��̬������������ `BySelector`��
* **ʹ�ã�** 
    *  `findObject(By.text("foo"))`  ���ַ�ʽ������ķ�ʽ�͸��ӵļ��
    *  `findObject(new BySelector().text("foo"))`  ���� `new BySelector()` �ǲ���ֱ��ʹ�õģ���Ϊ���캯������ `public` ��

* ������ `BySelector` ���еķ��� `By` �ж��У�����һЩ���⡣

### 3.3 ������������

![������������.PNG](http://on9czqsf5.bkt.clouddn.com/������������.PNG?2017-05-19-09-46-32)
![������������2.PNG](http://on9czqsf5.bkt.clouddn.com/������������2.PNG?2017-05-19-09-48-38)

�� `UiSelector` �Ĳ�ͬ�㣺

1. ʹ�ü�д����ʽ�����̴��볤��
2. ������ `EndsWith()` �Ľ�βƥ�䷽��
3. ��ʹ������ƥ���ʱ����Ҫ�ȴ���һ�� `Pattern`�����Ĳ��������� `String`

### 3.4 �������

![�������.PNG](http://on9czqsf5.bkt.clouddn.com/�������.PNG?2017-05-19-09-59-13)

1. `����` ��ָ��ǰ�㼶֮�µ�ֱ�Ӳ㼶��`���` ��ָ��ǰ�㼶֮�µ����в㼶��
2. `Դ����ܴ������⣬ʹ��ʱС�ģ�`

### 3.5 �߼���������

�� `UiSelector` �����Զ�һ��

### 3.6 �����㼶��ȿ��ƣ���Ҫ���£�

**���** ��Ⱦ��� `UI �㼶�����`


![�������API.PNG](http://on9czqsf5.bkt.clouddn.com/�������API.PNG?2017-05-19-10-20-56)

1. `By.depth(int exactDepth)` ֻ����һ������ʹ�� `By` ��ֱ�ӵ��ã����������������ԣ����Ƕ����� `BySelector` ��
2. ����������ʹ�÷���Ϊ�� ��ʹ�� `By` ������һ���������õ����ص� `BySelector`��Ȼ���ٵ��÷���


## 4. UiAutomator2 Until 

�ٷ��ĵ��� https://developer.android.com/reference/android/support/test/uiautomator/Until.html

### 4.1 ״̬���� <UiObject2Condition>

1. ״̬�ı�ͨ�����Եĸı�������
2. һ�� `UiObject2Condition` ���� `UiObject2` ����ĳ���������ض�״̬
    * `UiObject2` ����ʹ�� API�� `public <R> R wait(UiObject2Condition<R> condition, long timeout)`


��Щ��������**��̬����**�����Կ���ֱ��ʹ�� `Until.xxx` ������

![Util״̬����API.PNG](http://on9czqsf5.bkt.clouddn.com/Util״̬����API.PNG?2017-05-19-10-45-36)

![Util״̬����API2.PNG](http://on9czqsf5.bkt.clouddn.com/Util״̬����API2.PNG?2017-05-19-10-48-33)

### 4.2 �������� <SearchCondition>

1. `SearchCondition` ��������һ����������Ҫ���ҵ� UI Ԫ�أ���Ҫ�����ж��Ƿ����ĳ�������


|��������|API|˵��|
|:--|:--|:--|
|`static SearchCondition<UiObject2>`|`findObject(BySelector selector)`|Returns a SearchCondition that is satisfied when at least one element matching the selector can be found.|
|`static SearchCondition<List<UiObject2>>`|`findObjects(BySelector selector)`|Returns a SearchCondition that is satisfied when at least one element matching the selector can be found.|
|`static SearchCondition<Boolean>`|`gone(BySelector selector)`|Returns a SearchCondition that is satisfied when no elements matching the selector can be found. �� selector ��������ƥ��������ʧ|
|`static SearchCondition<Boolean>`|`hasObject(BySelector selector)`|Returns a SearchCondition that is satisfied when at least one element matching the selector can be found.|


### 4.3 �¼����� <EventCondition>

1. `EventCondition` ��һ����������������һ��ʱ���һ��ϵ���¼���������Ҫ�����ж�ĳ���¼��Ƿ����ˡ�

|��������|API|˵��|
|:--|:--|:--|
|`static EventCondition<Boolean>`|`newWindow()`|Returns a condition that depends on a new window having appeared.|
|`static EventCondition<Boolean>`|`scrollFinished(Direction direction)`|Returns a condition that depends on a scroll having reached the end in the given direction.|
 


## 5. UiAutomator2 Gradle ִ�в���

### 5.1 Gradle Task����

#### 5.1.1 Gradle ����

1. `Gradle` ��һ�� `��������/�Զ�����������`���� `ant/maven` һ�����������в�֮ͬ������������ `Groovy����`����û��ʹ�� `xml` ���ԡ���ʹ�������ӵļ�顢����ǿ����ǣ�`gradle` ��ȫ���� `maven`��
2. `Project`: ��Ŀ����һ�����ڹ��������(��һ�� jar �ļ�)������һ����Ҫ��ɵ�Ŀ��(�粿��Ӧ�ó���)
3. `Task`: ����������һ����С����
4. Gradle ��װ����
    1. ��װ `JDK`������ `JAVA_HOME` ��������
        * ��Ϊ `Gradle` ���� `Groovy` ��д�ģ��� `Groovy` ���� `Java`
    2. ���� `Gradle`
        * ��ַ�� http://www.gradle.org/downloads
    3. ��ѹ `gradle-xx-all.zip`
    4. ���û�������
        * ��ӻ��������� `GRADLE_HOME` ֵΪ�� `gradle` ��Ŀ¼
        * ��ӵ� `PATH`�� `%GRADLE_HOME/bin` �ӵ� `PATH` �Ļ������� 
    5. ��֤��װ
        * �������֮������ `gradle -v`������Ƿ�װ���� 


### 5.2 Android Gradle Task

![android-gradle-task.PNG](http://on9czqsf5.bkt.clouddn.com/android-gradle-task.PNG?2017-05-19-11-20-19)

1. ʹ�� `gradle tasks` �Ϳ��Բ鿴֧�ֵ� `task`
2. `assemble`�� Ҳ���Ǳ��� `apk`��ʹ�� `gradle assemble` �Ϳ��Ա��� `apk`
3. `assembleAndroidTest`: Ҳ���Ǳ�����װ���� apk

### 5.3 Gradle ִ�в���

#### 5.3.1 ִ�в��Բ���

1. �� `Android Studio` �� `Terminal` ���ߴ� `cmd` �����У����빤��Ŀ¼
2. �����ֻ��� PC ���������`gradle connectedCheck` ���� `gralde cC`
3. ��ʼִ�У��ȴ��������
    * ����Ŀ¼�� `app/build/reports/androidTests/connected/index.html`



