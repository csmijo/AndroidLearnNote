#LayoutInflater(���ַ���)

`Android` `LayoutInflater`

--

##1. LayoutInflater����ؽ���

###1) LayoutInflater�Ľ���

����LayoutInflater��һ�����ڼ��ز��ֵ�ϵͳ���񣬾���ʵ������`Layout XML`�ļ���Ӧ��View���� ������ֱ��ʹ�ã���Ҫͨ��`getLayoutInflater()`������`getSystemService()`����������뵱ǰ`Context`�󶨵� `LayoutInflater`ʵ��!

###2) LayoutInflater���÷�

1. ��ȡLayoutInflaterʵ�������ַ�����
    * `LayoutInflater inflater1 = LayoutInflater.from(this);`
    * `LayoutInflater inflater2 = getLayoutInflater();`
    * `LayoutInflater inflater3 = (LayoutInflater)getSystemService(LAYOUT_INFLATER_SERVICE);`

2. ���ز��ֵķ���

    `public View inflate(int resource,ViewGroup root,boolean attachToRoot)`
    * **resource��** Ҫ���صĲ��ֶ�Ӧ����Դid
    * **root:** Ϊ�ò��ֵ��ⲿ��Ƕ��һ�㸸���֣��������Ҫ�Ļ���дnull����
    * **attToRoot��** �Ƿ�Ϊ���صĲ����ļ����������һ��root����

##2. ��Java������ز���

```java
public class MainActivity extends Activity{
    
    protected void onCreate(Bundle savedInstanceState){
        super.onCreate(savedInstanceState);
        
        /*1. �������������*/
        RelativeLayout rly = new RelativeLayout(this);   
        Button btn_one = new Button(this);
        Button btn_two = new Button(this);
        
        /*2. Ϊ��������������������*/
        btn_one.setText("��ťһ");
        btn_two.setText("��ť��");

        /*Ϊ��ťһ����һ��idֵ�������ֶ����ã�����RelativeLayout�Ĵ�������ص�ȱ��*/  
        btn_one.setId(123);      

        /*���ð�ťһ��λ�ã��ڸ������о���*/
        Relativelayout.LayoutParams params1 = new RelativeLayout.LayoutParams(LayoutParams.WRAP_CONTENT,LayoutParams.WRAP_CONTENT);
        params1.addRule(RelativeLayout.CENTER_IN_PARENT);
        
        /*���ð�ť����λ�ã��ڰ�ťһ���·������Ҷ��븸�����ұ�*/
        RelativeLayout.LayoutParams params2 = new RelativeLayout.LayoutParams(LayoutParams.WRAP_CONTENT,LayoutParams.WRAP_CONTENT);
        params2.addRule(RelativeLayout.BELOW,123);
        params2.addRule(RelativeLayout.ALIGN_PARENT_RIGHT);
        
        /*3. �������ӵ��ⲿ������*/
        rly.addView(btn_one,params1);
        rly.addView(btn_two,params2);
        
        /*4. ���õ�ǰ��ͼ���ص�view��rly*/
        setContentView(rly);
    }
}
```

##3. Java���붯̬��ӿؼ���xml����

###1) Java���붯̬���View

����**��̬��������д��������**�����������Ƿ���Ҫ��**setContentView(R.Layout.activity_main)**��

��д�������ļ���`activity_main.xml`
```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"  
    android:id="@+id/RelativeLayout1"  
    android:layout_width="match_parent"  
    android:layout_height="match_parent" >  
  
    <TextView   
        android:id="@+id/txtTitle"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:text="����xml�ļ����صĲ���"/>  
     
</RelativeLayout>  
```
####��һ�֣�����ҪsetContentView�����ȼ��ز����ļ� 
```java
public class MainActivity extends Activity {  
    @Override  
    protected void onCreate(Bundle savedInstanceState) {  
        super.onCreate(savedInstanceState);  
        Button btnOne = new Button(this);  
        btnOne.setText("���Ƕ�̬��ӵİ�ť");  
        RelativeLayout.LayoutParams lp2 = new RelativeLayout.LayoutParams(    
                LayoutParams.WRAP_CONTENT, LayoutParams.WRAP_CONTENT);    
        lp2.addRule(RelativeLayout.CENTER_IN_PARENT);    
       
        /*ʹ��LayoutInflater���ز����ļ���Ȼ���ڲ���RelativeLayout1*/
        LayoutInflater inflater = LayoutInflater.from(this);  
        RelativeLayout rly = (RelativeLayout) inflater.inflate(  
                R.layout.activity_main, null)  
                .findViewById(R.id.RelativeLayout1);  
        rly.addView(btnOne,lp2);  
        setContentView(rly);  
    }  
}
```

#####�ڶ��֣���ҪsetContentView�����ȼ��ز����ļ� 

```java
public class MainActivity extends Activity {  
    @Override  
    protected void onCreate(Bundle savedInstanceState) {  
        super.onCreate(savedInstanceState);  
        setContentView(R.layout.activity_main);  
        
        Button btnOne = new Button(this);  
        btnOne.setText("���Ƕ�̬��ӵİ�ť");  
        RelativeLayout.LayoutParams lp2 = new RelativeLayout.LayoutParams(    
                LayoutParams.WRAP_CONTENT, LayoutParams.WRAP_CONTENT);    
        lp2.addRule(RelativeLayout.CENTER_IN_PARENT);   
        
        /*�Ѿ�������activity_main��ֱ�Ӳ���RelativeLayout1*/ 
        RelativeLayout rly = (RelativeLayout) findViewById(R.id.RelativeLayout1);  
        rly.addView(btnOne,lp2);  
    }  
} 
```
###2) Java���붯̬����xml����

**activity_main.xml**
```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/RelativeLayout1"
    android:layout_width="match_parent"
    android:layout_height="match_parent" >
    <Button
        android:id="@+id/btnLoad"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="��̬���ز���"/>
</RelativeLayout>  
```

**inflate.xml**
```xml
<?xml version="1.0" encoding="utf-8"?>  
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"  
    android:layout_width="match_parent"  
    android:layout_height="match_parent"  
    android:gravity="center"  
    android:orientation="vertical"  
    android:id="@+id/ly_inflate" >  
  
    <TextView  
        android:layout_width="wrap_content"  
        android:layout_height="wrap_content"  
        android:text="����Java������صĲ���" />  
  
    <Button  
        android:layout_width="wrap_content"  
        android:layout_height="wrap_content"  
        android:text="���ǲ������һ��С��ť" />  
  
</LinearLayout> 
```

**MainActivity.java**
```java
public class MainActivity extends Activity {  
    @Override  
    protected void onCreate(Bundle savedInstanceState) {  
        super.onCreate(savedInstanceState);  
        setContentView(R.layout.activity_main);  
        
        /*1. ���LayoutInflater����*/  
        final LayoutInflater inflater = LayoutInflater.from(this);    
        //����ⲿ��������  
        final RelativeLayout rly = (RelativeLayout) findViewById(R.id.RelativeLayout1);  
        Button btnLoad = (Button) findViewById(R.id.btnLoad);  
        btnLoad.setOnClickListener(new OnClickListener() {  
            @Override  
            public void onClick(View v) {  
                //2. ����Ҫ��ӵĲ��ֶ���  
                LinearLayout ly = (LinearLayout) inflater.inflate(  
                        R.layout.inflate, null, false).findViewById(  
                        R.id.ly_inflate);  
                //3. ���ü��ز��ֵĴ�С��λ��  
                RelativeLayout.LayoutParams lp = new RelativeLayout.LayoutParams(    
                        LayoutParams.WRAP_CONTENT, LayoutParams.WRAP_CONTENT);    
                lp.addRule(RelativeLayout.CENTER_IN_PARENT);    
                //4. ��ӵ����������
                rly.addView(ly,lp);  
            }  
        });  
    }  
} 
```

