# gradleѧϰ�ʼ�

`gradle`

---
## 0. ��Ҫ

* [Gradle�汾����-�����뽵��](http://hucaihua.cn/2016/09/27/Gradle_upgrade/)
* [compileSdkVersion , targetSdkVersion �� minSdkVersion](http://hucaihua.cn/2017/01/10/sdkversion/)

�ǳ���������˵����gradle ���������顣

## 1. Android studio �е� Gradle

### 1.1 �Զ�����

ÿһ��**���µ��빤��ʱ**, ��ΪĬ�ϻ�ʹ�� `Use default gradle    wrapper (recommended)` ����, ���� `As` ������ `gradle-wrapper.properties` �� `distributionUrl` ��ָ���� `gradle` �汾. ��������ڹ����ձ�����ޱ�. �ҵĽ������ҵ������ļ�, **�����޸� distributionUrl** Ϊ�����ع��� gradle �汾(������֮ǰ�Ѿ����ع� `gradle-2.14.1` ��), ��������ֱ�Ӵ���.

ʵ����, ���������λ�� `As` �Զ����ɵ������ļ�(`.idea/gradle.xml`) 

#### 1.1.1 �½�����

�������裺 `File --> New --> New Project` �½���Ŀ

�����½���Ŀ��As ���������������ɵģ�

1. �� project �� `.idea/gradle.xml` �п��Կ��� `GradleProjectSettings` ���������Ĳ������� 

    ```
     <GradleProjectSettings>
        <option name="distributionType" value="LOCAL" />
        <option name="externalProjectPath" value="$PROJECT_DIR$" />
        <option name="gradleHome" value="D:\program\Android Studio\gradle\gradle-2.14.1" />    // �ص�
        <option name="gradleJvm" value="1.8" />
        <option name="modules">
          <set>
            <option value="$PROJECT_DIR$" />
            <option value="$PROJECT_DIR$/learnanimation" />
            <option value="$PROJECT_DIR$/learnview" />
          </set>
        </option>
      </GradleProjectSettings>
    ```
    
2. ���� AndroidStudio �� `Settings` �ı����������ģ� 
    
    ```
    Gradle --> Project-level settings: 
        Use local gradle distribution:
             Gradle Home: D:\program\Android Studio\gradle\gradle-2.14.1
    ```
    
3. �ɼ���As �������޶��� gradle �İ汾����Ȼ�����ָ������� gradle �汾�����ڵĻ���һ����ȥ���ء�
    

### 1.1.2 Open ����

�������裺 `File --> Open` (**ע��**������ `Reopen`) ��һ����Ŀ


1. �� project �� `.idea/gradle.xml` �п��Կ��� `GradleProjectSettings` ���������Ĳ������� 

    ```
    <GradleProjectSettings>
        <option name="distributionType" value="DEFAULT_WRAPPED" />
        <option name="externalProjectPath" value="$PROJECT_DIR$" />
        <option name="modules">
          <set>
            <option value="$PROJECT_DIR$" />
            <option value="$PROJECT_DIR$/app" />
          </set>
        </option>
        <option name="resolveModulePerSourceSet" value="false" />
      </GradleProjectSettings>  
    ```
    
2. ���� AndroidStudio �� `Settings` �ı����������ģ� 
    
    ```
    Gradle --> Project-level settings: 
        Use default gradle wrapper(recommended)
    ```
3. Ҳ����˵, ÿ���� Open һ����Ŀ��ʱ��, As �������֮ǰ���õ� gradle �汾, ��ʹ�� wrapper �ļ�����ָ���İ汾. ������ clone �����Ĵ����һ�δ򿪶��Ῠ�ܾõ�ԭ��, ������Ϊ���������� wrapper �е� gradle ����

### 1.2 gradle-wrapper.properties

AS �����Ĺ���, �ڸ�Ŀ¼���� `gradlew.bat` �� `gradlew.sh` �ļ�. �������ļ����ȡ `gradle/wrapper/gradle-wrapper.properties` ��ʹ������ָ���� `gradle` �汾���б���. һ��������׻������� `CI` ��������������ÿ�α��붼��ͬ���Ļ�����.

```
#Mon Dec 28 10:00:20 PST 2015
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
distributionUrl=https\://services.gradle.org/distributions/gradle-2.14.1-all.zip
```

1. `GRADLE_USER_HOME` Ĭ��ֵ�ǵ��Ե� `USER_HOME/.gradle`(windows ���� `c:��\Users\<username>\.gradle`, linux ���� `~/.gradle` )
2. ���� `gradlew` ����, �������·��û���ҵ���ִ�е� `gradle` �ļ�, ���ʹ�� `distributionUrl` ����ָ���� url ���غ���ִ��.


[����]

1. Android studio new project ��һ��ʲô���Ĺ��̣���
    1. new project ������������Щ��������download gradle �汾���� use defalut �� use local �����𣿣� gradlew.bat ��ô���ʹ�ã���

2. Android studio open project ����һ��ʲô���Ĺ��̣���
3. Android studio reopen project���� 
4. �����ַ�ʽ�� project �����𣿣�


### 1.3 Android Plugin for Gradle 

#### 1.3.1 ���

```
1. The Android Studio build system is based on Gradle. (Android studio ʹ�� Gradle �����б���)
2. The Android plugin for Gradle adds several features that are specific to building Android apps. (Android plugin for Gradle �����һЩ����Android app������)
3. Although the Android plugin is typically updated in lock-step with Android Studio, the plugin (and the rest of the Gradle system) can run independent of Android Studio and be updated separately. (��Ȼ Android plugin ������ Android studio �ĸ��¶����µģ��������� Android plugin�� Gradle�����ǿ��Զ����� Android studio ���к͸��µ�)
```

#### 1.3.2 ��Ӧ��ϵ

�ο���[Android Plugin for Gradle Release Notes](https://developer.android.com/studio/releases/gradle-plugin.html#revisions)

|Plugin version|Required Gradle version|Required version of SDK Build Tools|
|:--:|:--:|:--:|
|1.0.0|2.2.1--2.3.x|21.1.1 or higher|
|1.0.1|2.2.1--2.3.x|21.1.1 or higher|
|1.1.0|2.2.1 or higher|21.1.1 or higher|
|1.1.1|2.2.1 or higher|21.1.1 or higher|
|1.1.2|2.2.1 or higher|21.1.1 or higher|
|1.1.3|2.2.1 or higher|21.1.1 or higher|
|1.2.0|2.2.1 or higher|21.1.1 or higher|
|1.3.0|2.2.1 or higher|21.1.1 or higher|
|1.3.1|2.2.1 or higher|21.1.1 or higher|
|1.5.0|2.2.1 or higher|21.1.1 or higher|
|2.0.0|2.10  or higher|21.1.1 or higher|
|2.1.0|2.10  or higher|23.0.2 or higher|
|2.1.3|2.14.1 or higher|23.0.2 or higher|
|2.2.0|2.14.1 or higher|23.0.2 or higher|
|2.3.0|3.3 or higher|25.0.0 or higher|
|2.3.1|3.3 or higher|25.0.0 or higher|
|2.3.2|3.3 or higher|25.0.0 or higher|
|2.3.3|3.3 or higher|25.0.0 or higher|

### 1.4 Android stuido��θ��� gradle �汾

�ο���[Android studio��θ���gradle�汾��](http://www.10tiao.com/html/430/201609/2650037559/1.html)

1. �޸� `Android studio` ����Ŀ¼�µ� `build.gradle`���޸ĸ��ļ��ģ�
    ```
     dependencies {
            classpath 'com.android.tools.build:gradle:x.x.x'
        }
    ```
    �޸� `Android Plugin for Gradle` �汾��Ϊ�㱾�ذ�װ `Gradle` ��Ӧ�İ汾�ţ��ο����� 1.3.2 �Ķ�Ӧ��ϵ�б�
    
2. ��λ�� ��Ŀ `gradle` Ŀ¼�� `gradle-wrapper.properties` �ļ����޸� `distributionUrl` �еİ汾��Ϊ�㱾�ذ�װ�� `gradle` �汾
3. �� `Android studio` --> `settings` --> `Gradle` --> `Project-level settings` ������ `Use local gradle distribution`, ѡ�񱾵ذ�װ `gradle` ��·��
4. `Sync Now` ���ɸ��ĳɹ�




## 2. Groovy

### 2.2 Groovy ��װ

�� Ubuntu16.04 Ϊ����

1. curl -s "https://get.sdkman.io" | bash
2. source "$HOME/.sdkman/bin/sdkman-init.sh"  ���ߴ��µ� terminal
3. sdk install groovy
4. groovy -version 

### 2.1 Groovy һЩǰ��֪ʶ

1. Groovyע�ͱ�Ǻ�Javaһ����֧��//����/**/ 
2. Groovy�����Բ��÷ֺŽ�β��GroovyΪ�˾������ٴ�������룬ȷʵɷ�ѿ��� 
3. Groovy��֧�ֶ�̬���ͣ���**���������ʱ����Բ�ָ�������͡�Groovy�У������������ʹ�ùؼ���def��ע�⣬��Ȼdef���Ǳ���ģ�����Ϊ�˴������������黹��ʹ��def�ؼ���**
4. ��������ʱ��**����������Ҳ���Բ�ָ��**������
    ```
    String testFunction(arg1,arg2){//����ָ����������
      ...
    }
    ```
    
5. ���˱���������Բ�ָ�������⣬**Groovy�к����ķ���ֵҲ�����������͵�**��
6. ��������ֵ��Groovy�ĺ�������Բ�ʹ��return xxx������xxxΪ��������ֵ�������ʹ��return���Ļ������������һ������ִ�н�������óɷ���ֵ��
7. Groovy���ַ���֧���൱ǿ�󣬳��������һЩ�ű����Ե��ŵ�
    * ������''�е������ϸ��ӦJava�е�String������$���Ž���ת��
    * ˫����""��������ͽű����ԵĴ����е�������ַ�����$�ŵĻ���������$���ʽ����ֵ��
    * ��������'''xxx'''�е��ַ���֧�����⻻��

8. ����ÿ�д��벻�üӷֺ��⣬Groovy�к������õ�ʱ�򻹿��Բ�������



### 2.2 Groovy �е���������

Groovy�е������������Ǿͽ������ֺ�Java��̫һ���ģ�

* һ����Java�еĻ����������͡� 
* ����һ����Groovy�е������ࡣ 
* ���һ���ǳ���Ҫ���Ǳհ���

#### 2.2.1 ������������


��Ϊ��̬���ԣ�Groovy�����е��������ﶼ�Ƕ������ԣ�**int��boolean��ЩJava�еĻ����������ͣ���Groovy��������ʵ��Ӧ�������ǵİ�װ�������͡�����int��ӦΪInteger��boolean��ӦΪBoolean**

#### 2.2.2 ������

Groovy�е�������ܼ򵥣������֣�

* List��������ײ��ӦJava�е�List�ӿڣ�һ����ArrayList��Ϊ������ʵ���ࡣ 
* Map����-ֵ����ײ��ӦJava�е�LinkedHashMap�� 
* Range����Χ������ʵ��List��һ����չ�� 

ʵ����

1. list �ࣺ 

    ```
    def aList = [5,'string',true] //List��[]���壬��Ԫ�ؿ������κζ���
    
    ������ȡ������ֱ��ͨ��������ȡ�����Ҳ��õ�������Խ�硣�������������ǰ�����ȣ�List���Զ������������Ԫ��
    ```
    
2. Map �ࣺ

    ```
    def aMap = ['key1':'value1','key2':true] 

    Map��[:]���壬ע�����е�ð�š�ð�������key���ұ���Value��key�������ַ�����value�������κζ������⣬key������''��""��������Ҳ���Բ������Ű�����������
    
    def aNewMap = [key1:"value",key2:true] //���е�key1��key2Ĭ�ϱ�������ַ���"key1"��"key2",����KeyҪ�ǲ�ʹ�����Ű������Ļ���Ҳ�����һ��������
    ```
   
3. Range ��

    ```
    def aRange = 1..5  <==Range���͵ı��� ��beginֵ+������+endֵ��ʾ������aRange����1,2,3,4,5��5��ֵ

    �������������һ��Ԫ�أ���
    
    def aRangeWithoutEnd = 1..<5  <==����1,2,3,4��4��Ԫ��
    println aRange.from
    println aRange.to
    ```

#### 2.2.3 �հ�

�հ�����һ���������ͣ���������һ�ο�ִ�еĴ��롣���������£�
```
def aClosure = {//�հ���һ�δ��룬������Ҫ�û�����������..  
    Stringparam1, int param2 ->  //�����ͷ�ܹؼ�����ͷǰ���ǲ������壬��ͷ�����Ǵ���  
    println"this is code" //���Ǵ��룬���һ���Ƿ���ֵ��  
   //Ҳ����ʹ��return����Groovy����ͨ����һ��  
}  
```

�����֮��Closure�Ķ����ʽ�ǣ�

```
def xxx = {paramters -> code}  //����  
def xxx = {�޲�������code}  ����case����Ҫ->����
```

**˵ʵ������C/C++���ԵĽǶȿ����հ��ͺ���ָ�����**���հ�����ú�Ҫ�������ķ������ǣ�
* �հ�����.call(����)  
* ���߸�����ָ����õķ������հ�����(����)  

���磺
```
aClosure.call("this is string",100)  ����  
aClosure("this is string", 100) 
```


�ڱհ��У�����Ҫע��һ�㣺

**����հ�û��������Ļ�����������һ������������������ֽ�it����this���������ơ�it����հ��Ĳ�����**

���磺

```
def greeting = { "Hello, $it!" }
assert greeting('Patrick') == 'Hello, Patrick!'
```

��ͬ�ڣ�

```
def greeting = { it -> "Hello, $it!" }
assert greeting('Patrick') == 'Hello, Patrick!'
```


**���ǣ�����ڱհ�����ʱ��������������д�������ʾ�հ�û�в�����**

```
def noParamClosure = { -> true }
```

���ʱ�����ǾͲ��ܸ�noParamClosure�������ˣ�

```
noParamClosure ("test")  <==����ร�
```

#### 2.2.4 Closure ʹ�õ�ע���

1. ʡ��Բ����

```
def iamList = [1,2,3,4,5]  //����һ��List
iamList.each{  //��������each����δ���ĸ�ʽ�������˰ɣ�each�Ǹ�������Բ����ȥ���ˣ�
      println it
}
```

�������������֪ʶ�㣺
* each�������õ�Բ���Ų����ˣ�ԭ����**Groovy�У������������һ�������Ǳհ��Ļ�������ʡ��Բ���š�**------������ر����Ҫ������

## 3. Gradle

**Gradle ��һ����̿��**�����Ա�д��ν�ı���ű�����ʵ������ Gradle �� API�� ����API��https://docs.gradle.org/current/javadoc/org/gradle/api/Project.html

### 3.1 �������

1. Gradle�У�ÿһ��������Ĺ��̶���**һ��Project**��
2. ÿһ��Project�ڹ�����ʱ�򶼰���**һϵ�е�Task**��
3. һ��Project���װ������ٸ�Task����ʵ���ɱ���ű�ָ����**���**�����������ʲô�أ����������������Task��������ִ����ЩTask�Ķ�����
4. Gradle��һ����ܣ���Ϊ��ܣ�**�����������̺͹���**��������ı��빤������ͨ������ķ�ʽ����ɵġ�


1. **ÿһ��Project����������һ��build.gradle�ļ�**�����������ݣ���������������˵�� 
2. **����multi-projects build����Ҫ�ڸ�Ŀ¼��Ҳ��һ��build.gradle����һ��settings.gradle��** 
3. **һ��Project��������tasks����ɵģ���gradle xxx��ʱ��ʵ������Ҫ��gradleִ��xxx����������������ɾ���Ĺ�����** 
4. ��Ȼ������Ĺ����Ͳ�ͬ�Ĳ���й�ϵ������JavaҪʹ��Java���������Android APP��Ҫʹ��Android APP�������Щ���Ƕ������������� 

### 3.2 gradle �������

1. gradle projects �鿴������Ϣ
2. gradle tasks �鿴������Ϣ
    * gradle \<project-path\>:tasks ���У�\<project-path\> ��Ŀ¼��������������ð��

3. gradle \<task-name\> ִ������ 
    * gradle tasks���г�ÿ�������������ͨ�����������Ǵ����֪����Щ�����Ǹ�ʲô�ģ�Ȼ��gradle task-nameִ�����ͺá�
    * Task��Task֮���������й�ϵ�ģ�**�������ν��������ϵ**�����磬assemble task����������task��ִ�У�assemble����������յ������

### 3.3 gradle ��������

1. Gradle��һ����ʼ������(Initiliazation phase)�����ʱ��settings.gradle��ִ�С� 
2. �����ý׶�(Configration phase)��ÿ��Project �� build.gradle ���ᱻ���������ڲ�������Ҳ�ᱻ��ӵ�һ������ͼ����ڽ��ִ�й����е�������ϵ�� 
3. Ȼ�����ִ�н׶�(Execution phase)������gradle xxx��ָ��ʲô����gradle�ͻὫ���xxx�������ϵ���������ȫ��������˳��ִ��һ�飡 

### 3.4 gradle���ģ�ͼ� APIʵ�����

**��Ҫ�ĵ���** https://docs.gradle.org/current/dsl/


---

[�ο�����]
* [android gradle ����һƪ�͹���](http://android.walfud.com/android-gradle-����һƪ�͹���/)
* [�������gradle](http://www.infoq.com/cn/articles/android-in-depth-gradle)
* [Android Plugin for Gradle Release Notes](https://developer.android.com/studio/releases/gradle-plugin.html#revisions)
* [Android studio��θ���gradle�汾��](http://www.10tiao.com/html/430/201609/2650037559/1.html)
* [Gradle�汾����-�����뽵��](http://hucaihua.cn/2016/09/27/Gradle_upgrade/)