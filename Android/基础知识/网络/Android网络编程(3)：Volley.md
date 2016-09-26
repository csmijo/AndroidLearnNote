#Android������(3):Volley

`Android` `Volley`

--

##1. Volley���

����Volley�ȿ��Է�������ȡ�����ݣ�Ҳ���Լ���ͼƬ�����������ܷ���Ҳ�����˴���ȵĵ�����**�������Ŀ����Ƿǳ��ʺ�ȥ�������������󣬵�ͨ��Ƶ�����������**�������ڴ����������������������˵�����ļ��ȣ�Volley�ı��־ͻ�ǳ���⡣

##2. Volley�����������

����Volley�������綼�ǻ���������еģ�������ֻҪ�����������������оͿ����ˣ�������л����ν�������һ������£�һ��Ӧ�ó��������������û���ر�Ƶ������ȫ����ֻ��һ��������У���ӦApplication��������ǳ��������������������һ��Activity��Ӧһ������������У����Ҫ����������ˣ����ȴ������У�
```java
RequestQueue mQueue = Volley.newRequestQueue(getApplicationContext());
```

##3. StringRequest���÷�

```java
        //�����������
        RequestQueue mQueue = Volley.newRequestQueue(getApplicationContext());
        StringRequest mStringRequest = new StringRequest(Request.Method.GET, "http://www.baidu.com",
                new Response.Listener<String>() {
                    @Override
                    public void onResponse(String response) {
                        Log.i("wangshu", response);
                    }
                }, new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {
                Log.e("wangshu", error.getMessage(), error);
            }
        });
        //��������������������
        mQueue.add(mStringRequest);
```

##4. Volley�ṹͼ

��������������![Volley�ṹͼ.png](pic/Volley�ṹͼ.png "")

��������ͼ���Կ���Volley��Ϊ�����̣߳��ֱ���**���߳�**��**��������߳�**����**��������߳�**��

1. �����������뻺����У�������ֿ����ҵ���Ӧ�Ļ�������ֱ�Ӷ�ȡ���沢������Ȼ��ص������̣߳�
2. ����ڻ�����û���ҵ������������������뵽��������У�Ȼ����HTTP���󣬽�����Ӧ��д�뻺�棬���ص������̡߳�

##5. ʹ��Volley�ϴ��ļ�

###1. .hprof�ļ����

```
HPROF file is a Java Hprof Data. HProf is a tool built into 
JDK for profiling the CPU and heap usage within a JVM.
```

* **MIME ���ͣ�** `application/octet-stream`
* **ħ���ֽ�(HEX):**  `-`
* **ħ���ַ���(ASCII):**  `-`

###2. �ύ��

ץȡһ���ύ���������������£�

<pre>
<code>
Connection: keep-alive
Content-Length: 123
X-Requested-With: ShockwaveFlash/16.0.0.296
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/40.0.2214.93 Safari/537.36
Content-Type: multipart/form-data; boundary=Ij5ei4KM7KM7ae0KM7cH2ae0Ij5Ef1
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.8
Cookie: bdshare_firstime=1409052493497

--Ij5ei4KM7KM7ae0KM7cH2ae0Ij5Ef1
Content-Disposition: form-data; name=&quot;position&quot;

1425264476444
--Ij5ei4KM7KM7ae0KM7cH2ae0Ij5Ef1
Content-Disposition: form-data; name=&quot;editorIndex&quot;

ue_con_1425264252856
--Ij5ei4KM7KM7ae0KM7cH2ae0Ij5Ef1
Content-Disposition: form-data; name=&quot;cm&quot;

100672
--Ij5ei4KM7KM7ae0KM7cH2ae0Ij5Ef1--
</code>
</pre>

�ó�һ���ϴ����ݽ��з�����
<pre>
<code>1 --Ij5ei4KM7KM7ae0KM7cH2ae0Ij5Ef1
2 Content-Disposition: form-data; name=&quot;cm&quot;
3 
4 100672
5 --Ij5ei4KM7KM7ae0KM7cH2ae0Ij5Ef1--</code>
</pre>

1. **��һ�У�**

    ��ʽΪ����--�� + boundary + ��\r\n����
    * ���С�--�������ݿ�ʼ��־��
    * boundary��ΪHttpʵ���ඨ������ݷָ��ߣ�boundary����Ϊ������ַ�
    * ��\r\n�� �ǻس�����
    
2. **�ڶ���**

    ��ʽΪ��Content-Disposition��form-data;name="��������"+\r\n
    * Content-Disposition ���ϴ�����������
    * form-data���Ա�����ʽ�ϴ�
    
3. **������**

    ��ʽΪ����\r\n�����س�����
    
4. **������**

    ��ʽΪ��value + ��\r\n��
    * value�ǲ�����ֵ����������key��value���

5. **�����У�������**

    ��ʽΪ����--�� + boundary + ��--�� + ��\r\n��
    **ע�⣺**���е����ݽ���֮����Ҫ�������β��־
    
**����ж�����������ظ�1��2��3��4��ֱ�����һ���������Ͻ����С�**

ֻ��̳� Request �Ϳ��Զ���һ��ʹ��Volley�ϴ������࣬�м���ע�⣺

1.  **Volley����Request��ʱ����Ҫ��д��ȡʵ��ķ���**

    ```java
    public byte[] getBody() throw AuthFailureError{}
    ```
    
2. **�Ѳ���ͨ�������Ƶ���ʽ��������������Ȼ�Ͳ���Ҫ��д��ȡ�����ķ���**

    ```java
    protected Map<String,String> getParams() throws AuthFailureError{}
    ```
3. **Request �л���һ���ؼ��ĵط�����Ҫ�� http ͷ����������������Ϊ������**

    <pre>
    <code>Content-Type: multipart/form-data; boundary=Ij5ei4KM7KM7ae0KM7cH2ae0Ij5Ef1</code>
    </pre>
    
    ������Ҫ��д����ķ���Ϊ��
    ```java
    private String MULTIPART_FROM_DATA = "multipart/form-data";
    private String BOUNDARY = "Ij5ei4KM7KM7ae0KM7cH2ae0Ij5Ef1";
    
    public String getBodyContentType(){
        return MULTIPART_FORM_DATA + ";boundary=" + BOUNDARY;
       }
    ```

###3. �ϴ��ļ�

ץȡһ���ύ���������������£�

<pre><code>POST <a href="http://chuantu.biz/upload.php">http://chuantu.biz/upload.php</a> HTTP/1.1
Host: chuantu.biz
Connection: keep-alive
Content-Length: 4459
Cache-Control: max-age=0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,<em>/</em>;q=0.8
Origin: <a href="http://chuantu.biz">http://chuantu.biz</a>
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/40.0.2214.93 Safari/537.36
Content-Type: multipart/form-data; boundary=WebKitFormBoundaryS4nmHw9nb2Eeusll
Referer: <a href="http://chuantu.biz/">http://chuantu.biz/</a>
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.8
Cookie: __cfduid=d9215d649e6e648e0eac7688b406a3d911425089350

--WebKitFormBoundaryS4nmHw9nb2Eeusll
Content-Disposition: form-data; name=&quot;uploadimg&quot;; filename=&quot;spark_bg.png&quot;
Content-Type: image/png

JFIFC
    %# , #&amp;&#39;)*)-0-(0%()(C
    (((((((((((((((((((((((((((((((((((((((((((((((((((&quot;
    }!1AQa&quot;q2#BR$3br
    %&amp;&#39;()*456789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz
    w!1AQaq&quot;2B  #3Rbr
    $4%&amp;&#39;()*56789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz?PNG
--WebKitFormBoundaryS4nmHw9nb2Eeusll--</code></pre>


�ó�һ�����з�����
<pre>
<code>1 --WebKitFormBoundaryS4nmHw9nb2Eeusll
2 Content-Disposition: form-data; name=&quot;uploadimg&quot;; filename=&quot;spark_bg.png&quot;
3 Content-Type: image/png
4 
5 JFIFC
    %# , #&amp;&#39;)*)-0-(0%()(C
    (((((((((((((((((((((((((((((((((((((((((((((((((((&quot;
    }!1AQa&quot;q2#BR$3br
    %&amp;&#39;()*456789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz
    w!1AQaq&quot;2B  #3Rbr
    $4%&amp;&#39;()*56789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz?PNG
6 --WebKitFormBoundaryS4nmHw9nb2Eeusll--</code>
</pre>


1. **��һ��**

    ��ʽΪ����--�� + boundary + ��\r\n��
    * ����ͬ���ύ�����еĽ���

2. **�ڶ���**

    ��ʽΪ��Content-Diposition:form-data;name="����������";filename="�ϴ��ļ����ļ���" + "\r\n"
    * �������ͨ���ύ������һ��`filename = "�ϴ��ļ����ļ���"`

3. **������**

    ��ʽΪ��Content-Type:�ļ���mime���� + "\r\n"
    * **��һ�����ϴ��ļ�����ģ�����ͨ�ļ��ύ����п���**�� mime������Ҫ�����ĵ���ѯ��
    
4. **������**

    ��ʽΪ��"\r\n"
    
5. **������**

    ��ʽΪ���ļ��Ķ��������� + "\r\n"
    
6. **������:������**

    ��ʽΪ��"--" + boundary + "--" + "\r\n"

**�ļ�Ҳ����ͬʱ�ϴ�����ļ����ϴ�����ļ�ʱ��ֻ��Ҫ�ظ�1��2��3��4��5�����ɣ�������һ���ļ���ĩβ����ͳһ�Ľ����С�**

���Կ������ļ��ϴ������ͨ�ı���ύ����������ͬ�ĵط���
1. �ڶ���������һ���ļ�������
2. ������һ�� Content-Type���ļ���mime���� + "\r\n"

--
**[�ο�]**
* [Android �����̣�3����Volley�÷�ȫ����](http://mp.weixin.qq.com/s?__biz=MzA3MDMyMjkzNg==&mid=2652261891&idx=1&sn=ff70183bc983577da4a584cde5a7f4ed&scene=1&srcid=0822q8tHD8Coxq1xFGQRxskX#wechat_redirect)
* [Android �����̣�4��: ��Դ�����Volley���ϣ�](http://mp.weixin.qq.com/s?__biz=MzA3MDMyMjkzNg==&mid=2652261893&idx=1&sn=f0ac821aeeea42414caf7d923f65db54&scene=1&srcid=0822hMQo4XYoguBXSG1KHfEq#wechat_redirect)
* [Android �����̣�4��: ��Դ�����Volley���£�](http://mp.weixin.qq.com/s?__biz=MzA3MDMyMjkzNg==&mid=2652261893&idx=2&sn=99c2b1404ad168112a2f481cc2a3c46b&scene=1&srcid=0822MaKKvSr6Zoby59dhJsfl#wechat_redirect)
* [��ϸ���ļ���չ�� .hprof](https://www.filedesc.com/zh/file/hprof)
* [Android Volley�ļ��ϴ���һ��](http://blog.csdn.net/hong15007046964/article/details/51153562)
* [Android Volley�ļ��ϴ�������](http://blog.csdn.net/hong15007046964/article/details/51153771)
* [Android���Զ���MultipartEntityʵ���ļ��ϴ��Լ�ʹ��Volley��ʵ���ļ��ϴ�](http://blog.csdn.net/bboyfeiyu/article/details/42266869)