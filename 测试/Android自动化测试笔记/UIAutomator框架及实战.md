# UIAutomator��ܼ�ʵս

`����` `UIAutomator`

--

## 1. UIAutomator ���

`UIAutomator` �� `Android` �ٷ��ṩ��һ��**�ں��Զ������Կ��**��

### 1.1 ���÷�Χ

Ŀǰ `UIAutomator` **��֧��API Level 17 ������**�����ҿؼ�����**��֧�� Android ԭ���ؼ������� WebView ���޷�������**

`UIAutomator` ������**��Դ��** ������º;�Ʒ���жԱȲ��ԣ������Խ��� **��Ԫ���ԡ����ܲ��ԡ�ѹ������**��`UIAutomator` ���Խ��� ROM �㼶�Ĳ��ԣ����� APP ��Э�������̵Ĳ��ԡ�


## 2. UIAutomator ��������

UIAutomator ������æ���������̴����Ͽ��Է�Ϊ���µĲ��裺

1. ����Ӧ�� UI ����Ԫ�أ���ȡԪ������
2. ������������������ģ���û���������
3. ������Դ���Ϊ���� jar ����push ���ն�
4. ���豸�����в��ԣ��鿴���Խ��
5. �޸ķ��ֵ� BUG�� �޸������²���

### 2.1 ����Ԫ�ػ�ȡ

ʹ�� `uiautomatorviewer.bat` �鿴�ͻ�ȡ����Ԫ����Ϣ, һ��λ�� `Android SDK\tools\` Ŀ¼��

�����ʡ�

��������������ť��
* һ������ʾ�� "`Device Screenshot(uiautomator dump)`" ��
* һ������ʾ�� "`Device Screenshot with compressed Hierarchy(uiautomator dump --compressed)`"

��������������ʲô���� 

uiautomator dump --compressed �Ǽ�����Ϣ

http://blog.csdn.net/wanglha/article/details/42969439


### 2.2 ��Ŀ��������

1. ���� Java ��Ŀ���� Android ��Ŀ
2. ��������� jar ���� `android.jar` �� `uiautomator.jar` �������� jar ��һ��λ�� `\Android SDK\platforms\android-xx` Ŀ¼�£����� xx ��ʾ `API��Level`, ����ʹ�� `API 19` ���ϣ������� `UiSelector.resourceId` ϵ�з�����

![uiautomator���������в��Դ���](http://on9czqsf5.bkt.clouddn.com/uiautomator%E7%BC%96%E8%AF%91%E4%B8%8E%E8%BF%90%E8%A1%8C%E6%B5%8B%E8%AF%95%E4%BB%A3%E7%A0%81.PNG)

**ע�⣺** ���� build �ļ��������е� `-t` ��������ʾ����� Android �汾�ڱ�����PC���е���ţ���ͼ��

![uiautomator-anroid-list.PNG](http://on9czqsf5.bkt.clouddn.com/uiautomator-anroid-list.PNG?2017-05-16-09-56-46)

## 3. UiDevice API

�ο����ף�
* https://wenku.baidu.com/view/7fe534bfa32d7375a517804b.html###
* �ٷ��ĵ�: https://developer.android.com/reference/android/support/test/uiautomator/UiDevice.html



�����ַ�ʽ���Ե��� UIDevice��
* `UiDevice.getInstance()`
* `getUiDevice()`

**�Ƽ�ʹ�� `UiDevice.getInstance()` ������д**��

��Ϊ���ʹ�� `getUiDevice()` ���е��ã���ͬһ�����в��������⣬�������Ҫ���������еķ���ʹ���� `getDevcice()` �����õ������в������﷨���󣬵���ִ�е�ʱ������

### 3.1 click

`boolean click(int x,int y)`

### 3.2 freezeRotation

`void freezeRotation()`

���ô��������豸����ת���ڵ�ǰ����ת״̬����

### 3.3 getCurrentPackageName

`String getCurrentPackageName()`

���ص�ǰ����İ������ַ���

### 3.4 getDisplayHeight �� getDisplayWidth

* `int getDisplayHeight()`
* `int getDisplayWidth()`

��ȡ��ʾ���ĸ߶ȡ���ȣ�������Ϊ��λ

### 3.5 getDisplayRotation

`int getDisplayRotation()`

���ص�ǰ����ʾ��ת��0,90,180,270���ֱ��� 0,1,2,3 ������

### 3.6 getDisplaySizeDp

`Point getDisplaySizeDp()`

������ʾ DP ��С(�豸����������)���ص���ʾ��С����ÿ����Ļ��ת

### 3.7 getProductName 

`String getProductName()`

���ص�ǰ�豸�Ĳ�Ʒ��

### 3.8 ������

1. `void registerWatcher(String name, UiWatcher watcher)`

    ע��һ������������ǰ����ָ�����豻��ϵ�ʱ�򣬴����ж��쳣
    
2. `void removeWatcher(String name)`
3. `void resetWatcherTriggers()`
4. `void runWatchers()`

    ǿ���������еļ�����
    
5. `boolean hasAnyWatcherTriggered()`

    ����Ƿ��м�����������
    
6. `boolean hasWatcherTriggered(String watcherName)`

    ���ĳ���ض��ļ������Ƿ񴥷���
    
### 3.9 �����¼�

1. `boolean pressBack()`   ģ��̰����ؼ�. 
2. `boolean pressDPadCenter()`   �켣�� 
3. `boolean pressDPadDown()`    �켣�� 
4. `boolean pressDPadLeft()`    �켣�� 
5. `boolean pressDPadRight()`   �켣��
6. `boolean pressDPadUp()`      �켣��
7. `boolean pressDelete()`    **ģ��̰�ɾ����**. 
8. `boolean pressEnter()`   **ģ��̰��س���**. 
9. `boolean pressHome()`    **ģ��̰�HOME��**.  
10. `boolean  pressKeyCode(int keyCode, int metaState)`   ģ��̰����̴���.  ���̴�����Բο��ȸ������ https://developer.android.com/reference/android/view/KeyEvent.html
11. `boolean pressKeyCode(int keyCode)`   ģ��̰����̴���
12. `boolean pressMenu()`     **ģ��̰�MENU��**
13. `boolean pressRecentApps()`     **ģ��̰����Ӧ�ó��򰴼�**
14. `boolean  pressSearch()`   **ģ��̰�������**
 
### 3.10 ��ת

1. `void freezeRotation()`  ���ô������Ͷ���װ��������ת���䵱ǰ��ת״̬ 
2. `void unfreezeRotation()`    �������ô�����������������ת 
3. `boolean isNaturalOrientation()`    ��������Ƿ���������Ȼ��ת������λ���� 
4. `void setOrientationLeft()`    ͨ�����ô�������Ȼ��ģ���豸����ת�����ҹ̶�λ�� 
5. `void setOrientationNatural()`    ͨ�����ô�������Ȼ��ģ���豸ת������ȻĬ�ϵķ��򣬲��ҹ̶�λ�� 
6. `void  setOrientationRight()` 
ͨ�����ô�������Ȼ��ģ����������ת�����ҹ̶���������
 
### 3.11 �����뻽��

1. `void sleep()`   **����**  ģ�ⰴ��Դ���������Ļ�Ѿ��ǹرյ���û���κ����� 
2. `void wakeUp()`  **����**  ģ�ⰴ��Դ���������Ļ�ǻ��ѵ�û���κ����� 
3. `boolean isScreenOn()`   �����Ļ�Ƿ���

### 3.12 �ȴ�����

1. `void waitForIdle(long timeout)`  �ȴ���ǰӦ�ó����ڿ���״̬ 
2. `void  waitForIdle()`  �ȴ���ǰ��Ӧ�ó����ڿ���״̬ 
3. `boolean  waitForWindowUpdate(String packageName, long timeout)`    �ȴ��������ݸ����¼��ķ��� 

### 3.13 ��ͼ

1. `boolean  takeScreenshot(File storePath)`     �ѵ�ǰ���ڽ�ͼ������洢ΪpngĬ��1.0f�Ĺ�ģ(ԭ�ߴ�)��90%������ ����Ϊfile����ļ�·��  
2. `boolean  takeScreenshot(File storePath, float scale, int quality)`      �ѵ�ǰ���ڽ�ͼΪpng��ʽͼƬ�������Զ������ű�����ͼƬ����
 
    ������  
    * storePath���洢·��������Ϊpng��ʽ 
    * Scale�����ű�����1.0Ϊԭͼ  
    * Quality��ͼƬѹ����������ΧΪ0-100

    ���أ�  
    * True����ͼ�ɹ� 
    * False����ͼʧ��

### 3.14 ��ק�뻬��

1. `boolean swipe(Point[] segments, int segmentSteps)`    �ڵ������л�����5msһ��  
2. `boolean swipe(int startX, int startY, int endX, int endY, int steps)`     ͨ������**������Ļ**  
3. `boolean  drag(int startX, int startY, int endX, int endY, int steps)`   ��һ�����굽��һ���������**��ק** 

    ������
    * segments��Poing[]      �����У����Զ���� 
    * segmentSteps����������
    * StartX-StartY�� ��������ֵ 
    
    ���أ�  
    * True�������ɹ� 
    * False������

### 3.15 ֪ͨ������������

1. `boolean openNotification()`   ��֪ͨ��  
2. `boolean openQuickSettings()`   �򿪿�������

### 3.16 ���ڲ��ֽṹ

1. `void dumpWindowHierarchy(String fileName)`   ���ڵ���ת����ǰ���ڵĲ��ֲ�νṹ���ļ�������/data/local/tmp 
2. `void setCompressedLayoutHeirarchy(boolean compressed)`  ���û���ò��ֲ��ѹ����

## 4. UiSelector API

`UiSelector` ����ͨ������������ڵ��ϵ��λ��������ƥ�䵽���������򷵻ص�һ��ƥ�������� **����ʹ����ʽ���ö����������λ���**��

### 4.1 UiSelector ʹ��������Խ���

|����ֵ|ֵ����|ʾ��|
|:--|:--|:--|
|index|int |0|
|instance|int |5
|class|String|android.wideget.TextView
|package|String|com.csmijo.test
|Content-desc|String|string
|checkable|boolean|false
|checked|boolean|false
|clickable|boolean|true
|enabled|boolean|false
|focusable|boolean|false
|focused|boolean|false
|Scrollable|boolean|false
|Long-clickable|boolean|false
|password|boolean|false
|selected|boolean|false
|bounds|Rect|[366,999][708,1197]
|text|String|��ϵ��

### 4.2 ����ƥ���ϵ����

1. ��ȫƥ��(Ĭ��)
2. ����ƥ��(Contains)
3. ����ƥ��(Matches)�����԰�����������ƥ��
4. ��ʼƥ��(StartsWith)

### 4.3 �ڵ��ϵ����

1. xml �ĵ��ڵ��ϵ
    * ��    Parent
    * ��    Children
    * ͬ��  Sibling
    * �ȱ�  Ancestor
    * ���  Descendant

### 4.4 �������������ı�������

1. `UiSelector text(String text)`
2. `UiSelector textContains(String text)`
3. `UiSelector textMatches(String text)`
4. `UiSelector textStartsWith(String text)`
5. `UiSelector description(String text)`
6. `UiSelector descriptionContains(String text)`
7. `UiSelector descriptionMatches(String text)`
8. `UiSelector descriptionStartsWith(String text)`

### 4.5 ���������������������

1. �������Զ�λ����
    * `UiSelector className(String className)`
    * `UiSelector classNameMatches(String regex)`

2. �������Զ�λ����
    * `UiSelector packageName(String name)`
    * `UiSelector packageNameMatches(String regex)`

### 4.6 ������������������ʵ��

1. ������ʵ��˵��
    * ���� `index` ָ������ͬ�����еı�ţ����ֵܲ㼶�ı��
    * ʵ�� `instance` ָ������ͬһ�������ļ�ͬһ�����еı��

2. ������ʵ�����Զ�λ����
    * `UiSelector index(int index)`
    * `UiSelector instance(int instance)`

### 4.7 ����������������������ڵ�

1. �������Զ�λ����
    * `UiSelector checked(boolean val)`   ѡ������
    * `UiSelector clickable(boolean val)`   �ɵ������
    * `UiSelector enabled(boolean val)`     enabled����
    * `UiSelector focusable(boolean val)`     ��������
    * `UiSelector focused(boolean val)`       ��ǰ��������
    * `UiSelector longClickable(boolean val)`    ��������
    * `UiSelector scrollable(boolean val)`      ��������
    * `UiSelector selected(boolean val)`        ����ѡ������

2. �ڵ����Զ�λ����

* `UiSelector childSelector(UiSelector selector)`  �ӵ�ǰ�������µݹ��ҷ����������������(**һ������������**)��Ҳ����˵�ڵ�ǰ������������в��ҷ������������
* `UiSelector fromParent(UiSelector selector)`   �Ӹ������µݹ��ҷ������������ (**һ���������ֵ���**)

ʾ����

```
// childSelector() ��ʹ��
UiScrollable scrollable = new UiScrollable(new UiSelector().scrollable(true));   // �ҵ���ǰ����listview

UiScrollable scrollable = new UiScrollable(new UiSelector().scrollable(true)
.childSelector(new UiSelector().text("Android")));   // �ڵ�ǰ����������в��� text Ϊ Android �Ķ���

scrollable.click();
```

```
// fromParent() ��ʹ��
UiObject Obj = new UiObject(new UiSelector().resourceId("xxx"));  // �ҵ���ǰ����

UiObject parentObj = new UiObject(new UiSelector().resourceId("xxx")
.fromParent(new UiSelector().className("android.widget.LinearLayout").index(1)));  // �ӵ�ǰ����ĸ����в��� className Ϊ LinearLayout ���� index Ϊ 1 �Ķ���

parentObj.click();
```


### 4.8 ��������������ԴID

**ע�⣺** ֻ���� Android 4.3 �����ϲ���ʹ�ã���֮ǰ�İ汾����ʹ��

1. ��ԴID��λ����
    * `UiSelector resourceId(String id)`
    * `UiSelector resourceIdMatches(String regex)`


## 5. UiObject API

`UiObject` ����һ��������󣬶����кܶ�ģ��ʵ�ʲ����ֻ��ķ��������ԣ���Ҫ������ **���/�������϶�/���������ԣ������Ƿ���ڣ��ı���������������Ʋ�������ȡ����**

### 5.1 ����볤��

* `boolean click()`
* `boolean clickAndWaitForNewWindow(long timeout)`
* `boolean clickAndWaitForNewWindow()`
* `boolean clickBottomRight()`
* `boolean clickTopLeft()`
* `boolean longClick()`
* `boolean longClickBottomRight()`
* `boolean longClickTopLeft()`

### 5.2 ��ק�뻬��

������ק����һ������ϣ�������ק����һ������

* `boolean dragTo(UiObject destObj,int steps)`
* `boolean dragTo(int destX,int destY, int steps)`
* `boolean swipeDown(int steps)`
* `boolean swipeLeft(int steps)`
* `boolean swipeRight(int steps)`
* `boolean swipeUp(int steps)`
 

### 5.3 �����ı�������ı�

* `boolean setText(String text)` 
    * **ע�⣺ֻ������Ӣ�ģ�������Ҫ���⴦��**
    * �������������ֵ�����½������룬���Ƚ���ɾ��������Ȼ���ٽ����������
* `void clearTextField()`
    * ��ĳЩ�������ʹ�û�������������ϵ����������Ǿ���Ҫͨ���Զ����ɾ����������ɾ���������ƶ���굽��β����del ������ɾ��

### 5.4 ��ȡ��������������Ե��ж�

1. ��ȡ���������

* `Rect getBounds()`             ��ȡ����������꣬�������Ͻ���������½�����
* `int getChildCount()`      ��ȡ��һ����������
* `String getClassName()`     ��ȡ�����������Ե������ı�
* `String getContentDescription()`   
* `String getPackageName()`
* `String getText()`
* `Rect getVisibleBounds()`   ���ؿɼ���ͼ�ķ�Χ�������ͼ�Ĳ����ǿɼ��ģ����пɼ����ֱ���ķ�Χ

### 5.5 ���Ʋ���

* `boolean performMultiPointerGesture(PointerCoords[] ... touches)`
* `boolean performTwoPointerGesture(Point startPoint1,Point startPoint2,Point endPoint1,Point endPoint2)`
* `boolean pinchIn(int percent,int steps)`   ���У�percentָ���ǶԽ��ߵİٷֱ�
* `boolean pinchOut(int percent,int steps)`

### 5.6 �ж϶����Ƿ����

* `boolean waitForExists(long timeout)`      �ȴ��������
* `boolean waitUtilGone(long timeout)`    �ȴ�������ʧ
* `boolean exists()`      �������Ƿ����

## 6. UiCollection API

### 6.1 UiCollection �����

1. UiCollection ��˵��
    * UiCollection �� UIObject ������
    * UiCollection ����Ԫ����Ŀ���ϣ�����ͬһ�����͵ĺϼ�

2. UiCollection����˵��
    * �Ȱ���һ��������ö�ٳ�������������з�����������Ԫ��
    * �ٴӷ���������Ԫ���ٴ�ͨ��һ�����������ն�λ��Ҫ�����

3. UiCollection ʹ�ó���
    * һ��ʹ�������������Ϊ����
    * һ��ʹ������Ҫ����������������ĳЩ���ز��ö�λ
    * ��ȡĳһ������������ȡ��ϵ���б��µ�ǰ��ͼ����ϵ�˵�����

### 6.2 �Ӽ����в��Ҷ���

* `UiObject getChildByDescription (UiSelector childPattern, String text)`
* `UiObject getChildByText (UiSelector childPattern, String text)`
* `UiObject getChildByInstance (UiSelector childPattern, int instance)`

�� `UiSelector` ѡ�����Ĳ��������д��� `ui` Ԫ����������**�ݹ�Ѱ��**���з����������Ӽ����ٴ���`description/text/instance` ������ǰ�������Ӽ���λ����Ҫ��Ԫ��

������
* `childPattern`�� `UiSelector` ����Ԫ��������������һ
* `text,instance` ����������Ԫ�����ٴ��� `text/instance` ����������Ԫ��


���ҵ����� `UiCollection`��Ȼ���ҳ���������һ `UiSelector` ����������ļ��ϣ�Ȼ�����ڼ����и�����������һ��������Ҫ��Ŀ�����

### 6.3 ��ȡĳ�������������������

* `int getChildCount(UiSelector childPattern)`
* `int getChildCount()`

�ڶ����������ص��� `UiCollection` ��ֱ������ĸ�����**ֻ����ֱ������**���������������һ���������� `UiCollection` ��**�ݹ�Ĳ���**�������������������

## 7. UiScrollable API

### 7.1 UiScrollable �����

1. `UiScrollable` �� `UiCollection` ������
2. `UiScrollable` ��ר�Ŵ�������¼����ṩ���ֹ�������

### 7.2 ���ٹ���

1. `boolean flingBackward()`        �Բ���Ϊ5����
2. `boolean flingForward()`        �Բ���Ϊ5����
3. `boolean flingToBeginning(int maxSwipes)`        �Բ���Ϊ5����
4. `boolean flingToEnd(int maxSwipes)`        �Բ���Ϊ5����

### 7.3 ��ȡ�б���Ԫ��

![UiScrollable��ȡ�б���Ԫ��.png](http://on9czqsf5.bkt.clouddn.com/UiScrollable��ȡ�б���Ԫ��.png?2017-04-24-19-52-42)

**ע��**�� `getChildByInstance()` **�ǲ��ܹ�����**����ֻ��������ǰҳ������

### 7.4 ��ȡ��������������������ֵ

1. `int getMaxSearchSwipes()`      **Ĭ�ϳ���ֵΪ 30**
2. `UiScrollable setMaxSearchSwipes(int swipes)`

����ʱ���ڵ�ǰҳ����ң������ǰҳ�治���ڣ���**�Ȼ�����ԭ��**��Ȼ���ٴ�ԭ�㿪ʼѰ�ҡ����û������ `swipes` ��������Ĭ����໬�� 30 �ξ�ֹͣ�������ʱ����û���ҵ���Ҫ����������ȴ���ʱʱ�䣬**��ʱʱ��Ϊ10s**��֮����Խ���������쳣��

### 7.5 ����ȡ��У׼�����������ȡ

**У׼������** ָ���ǻ�����������ʱ��ƫ������������ȡƫ�Ʊ���
 
1. `double getSwipeDeadZonePercentage()`       **Ĭ��Ϊ0.1,10%**
2. `UiScrollable setSwipeDeadZonePercentage(double swipeDeadZonePercentage)`     ����һ�������Ĵ�С���ڻ���ʱ����Ϊ�޽Ӵ����İٷֱ�

ͨ������ `DeadZone` �İٷֱȿ��Կ��ƻ����ľ����Լ��������ٶȡ���`DeadZone` �İٷֱȴﵽ 50%ʱ��ֱ�ӱ�ɵ���¼������ٻ�����

### 7.6 ��ǰ������

![UiScrollable��ǰ������API.png](http://on9czqsf5.bkt.clouddn.com/UiScrollable��ǰ������API.png?2017-04-24-20-22-01)


### 7.7 ������ĳ������


![UiScrollable������ĳ������.png](http://on9czqsf5.bkt.clouddn.com/UiScrollable������ĳ������.png?2017-04-25-15-44-20)

### 7.8 ���ù�������

1. `UiScrollable setAsHorizontalList()`    ˮƽ���������ҹ�����
2. `UiScrollable setAsVerticalList()`     ������������¹�����

## 8. UIWatcher API

### 8.1 UiWatcher ��������жϼ����������

`UiWatcher`  ���ڴ���ű�ִ�й�����������Ԥ��Ĳ���

1. `public boolean checkForCondition()`
    
    **�ڲ��Կ���޷��ҵ�һ��ƥ��ʱ**��ʹ��`uiselector` ���Կ�ܻ��Զ����ô˷����Ŵ�����򷽷����ڳ�ʱδ�ҵ�ƥ����ʱ����ܵ��� `checkForCondition()` ���������豸�ϵ�������ע��ļ����������������ʹ�ô˷����������ж����Ᵽ֤���������������С�

### 8.2 ����������

1. `void registerWatcher(String name, UiWatcher watcher)`
2. `void removeWatcher(String name)`
3. `void resetWatcherTriggers()`
4. `void runWatchers()`


**ע�⣺**

1. ʹ��ѭ����ʱ������ for ѭ���壬һ��������������������ѭ����֮���ǲ����ٴν��뵽ѭ����֮�ڵ�
2. ʹ�÷�����ʱ��һ��������������������������֮��Ͳ����ٽ����ˣ�������ʹ���Լ��ķ���ʱ�����������޷����������ָ���
2. `UiDevice` �Ĳ����ǲ��ᴥ����������

## 9. Configurator API

`Configurator` �������ýű�������Ĭ����ʱ

![ConfiguratorAPI.png](http://on9czqsf5.bkt.clouddn.com/ConfiguratorAPI.png?2017-04-25-18-18-43)

## 10. UiAutomator ����鿴

### 10.1 �����鼰�鿴

1. ��������
    * ���Դ���`AssertionFailedError`
    * �ű�����`UiObjectNotFoundException��java�쳣�ȵ�`

2. ����״̬
    * ����״̬
    * ���״̬
    * ������Ϣ

3. ����״̬
    * 1  : ����ǰ
    * -1 : �������

4. ���״̬
    * 0  : ok
    * -1 : Errors   �ű�����
    * -2 : Failures  ���Դ���

5. ������Ϣ
    * ����ǰ��Ϣ   ״̬��Ϊ�� 1
    * ��������Ϣ
    * ���к���Ϣ   ״̬��Ϊ�� -1
6. ���к��ӡ�Ľ����Ϣ�У�
`Test results for WatcherResultPrinter= .` 
    * `.`  ��ʾû���κ��쳣
    * `.E` ��ʾ�ű�����
    * `.F` ��ʾ���Դ���

### 10.2 �����Ϣ������

1. �����Ϣʹ�õ� API ˵��
    * `Bundle`
    * `getAutomationSupport().sendStatus(int, Bundle)`

### 10.3 ����������ƽű�

1. ͨ�� `-e` �������ݵ������У��磺����һ���绰
2. ͨ�� `-e` ����������Ʋ������ƽű����磺����Ӧ������

* `Bundle bundle = new Bundle `    �½�һ�� Bundle ����
* `Bundle bundle = getParams()`    ��ȡ�����д���Ĳ���
* `String value = (String)bundle.get(key)`  ��ȡ�����д���ľ������ֵ
* `-e key value`  ͨ�������ĸ�ʽ�������н��в���������

## 11. UiAutomator ������ʽ��ʹ��

### 11.1 ������ʽ

![������ʽ����Ԫ�ַ�.png](http://on9czqsf5.bkt.clouddn.com/������ʽ����Ԫ�ַ�.png?2017-04-26-17-39-59)

![��ʾ������Ԫ�ַ�.png](http://on9czqsf5.bkt.clouddn.com/��ʾ������Ԫ�ַ�.png?2017-04-26-17-40-06)

|����|JAVA API|
|:--|:--|
|ƥ���ַ���|matcher(regex)|
|�滻�ַ���|replace(regex,input)|
|��ȡ�ַ���|Matcher.group()|
|����ַ���|split(regex)|


```
# ��ȡ
Stirng s = "testa1234bafasda";
Pattern pattern = Pattern.compile("\\d+");
Matcher matcher = pattern.matcher(s);
while(matcher.find()){
    System.out.println(m.group());
}
```

## 12. ���Ժ���

![���Ժ�������.PNG](http://on9czqsf5.bkt.clouddn.com/���Ժ�������.PNG?2017-04-26-19-59-52)

## 13. UiAutomator ͼ����

### 13.1 ��ͼƬ��Ƕ������

```
public Bitmap drawTextBitmap(Bitmap bitmap,String text){
	    int x = bitmap.getWidth();
	    int y = bitmap.getHeight();
	    
	    // ����һ����ԭ��ͼƬ�����λͼ
	    Bitmap newBitmap = Bitmap.createBitmap(x, y+80, Bitmap.Config.ARGB_8888);
	    Canvas canvas = new Canvas(newBitmap);
	    Paint paint = new Paint();
	    
	    // ��ԭͼλ�ã�0��0������һ��ͼƬ
	    canvas.drawBitmap(bitmap, 0, 0,paint);
	    // ������ɫ
	    paint.setColor(Color.parseColor("#FF0000"));
	    paint.setTextSize(30);
	    canvas.drawText(text, 20, y+55, paint);
	    canvas.save(Canvas.ALL_SAVE_FLAG);
	    canvas.restore();
	    return newBitmap;    
	}
```

### 13.2 ͼƬ�Ա�

```
public boolean imageSameAs(String targetImagePath,String comPath,double percent){
		Bitmap m1 = BitmapFactory.decodeFile(targetImagePath);
		Bitmap m2 = BitmapFactory.decodeFile(comPath);
		
		int width = m2.getWidth();
		int height = m2.getHeight();
		int numDiffPixels = 0;
		for(int x=0;x<width;x++){
			for(int y=0;y<height;y++){
				if(m2.getPixel(x, y) != m1.getPixel(x, y)){
					numDiffPixels++;
				}
			}
		}
		
		double totalPixels = height*width;
		double diffPercent = numDiffPixels/totalPixels;
		return percent <= 1.0 - diffPercent;
	}
```

## 14. UiAutomator �и��� APK ��ʹ��

### 14.1 �ڲ����е�����ʾ��

1. ʹ�� `am broadcast -a com.csmijo.test.action -e key value` ����һ���㲥
2. �½�һ�� Apk ��������һ�� `BroadcastReceiver` ������Ӧ `com.csmijo.test.action` ������ `action`��Ȼ���� `onReceive()` �����е��� һ���Ի���������ʾ `value`����Ϣ 

### 14.2 �ڲ�������������

���� `UiAutomator` Ĭ��ֻ������ `ASCII` �ַ�������Ϊ�������������͵����֣���Ҫʹ�� `UiAutomator Unicode` �������������룬�� **Jutf-7���뷨**

ʹ�ò��裺

1. ��װ `Jutf-7` ���뷨
2. ϵͳ���� --> ���Ժ����뷨 --> ���� UTF-7 ΪĬ�����뷨
3. UTF-7 UiAutomator �������������ű�
4. `UiObject.setText(Utf7lmeHelper.e("��������"));`

