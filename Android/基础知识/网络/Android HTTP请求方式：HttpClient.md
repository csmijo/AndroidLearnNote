#Android HTTP����ʽ:HttpClient

`Android` `HttpClient`

--

##1. HttpClient����

����HttpClient������**��Google����**�ˣ�������������ƽʱҲ������HttpClient��ץ�°������Jsoup������ҳЧ�����ѣ�HttpClient ���ڽ���/����Http����/��Ӧ�����������������Ӧ����ִ��HTMLҳ��Ǳ���JS���룬�����ҳ������ �����κν���������

##2. HttpClientʹ������

1. ����HttpClient����`HttpClient client = new HttpClient()`��
2. ����Get���󣬴���HttpGet���󣻷���Post���󣬴���HttpPost����
3. ����������������߶�����ʹ��`setParams(HttpParams)`;Post��������`setEntry(HttpEntity)`������
4. ����HttpClient�����execute�����������󣬸÷�������һ��HttpResponse���󣬸ö����װ�˷���������Ӧ���ݣ�
5. �Է��ص�HttpResponse�������`getAllHeaders()`��`getHeaders(name)`�ȷ�����÷���������Ӧͷ������`getEntry()`����ȡ��HttpEntity����

##3. ʹ��HttpClient����Get����

```java
public void GetUtil(){
    HttpClient httpClient = new DefaultHttpClient();
    HttpGet httpGet = new HttpGet("http://www.w3cschool.cc/python/python-tutorial.html");
    HttpResponse httpResponse = httpClient.execute(httpGet);
    if (httpResponse.getStatusLine().getStatusCode() == 200) {
         HttpEntity entity = httpResponse.getEntity();
         detail = EntityUtils.toString(entity, "utf-8");
    }
}
```

�������⣬����Ǵ��в�����GET����Ļ������ǿ��Խ������ŵ�һ��List�����У��ٶԲ�������URL���룬 ����URLƴ���¾ͺ��ˣ�
```java
List<BasicNameValuePair> params = new LinkedList<BasicNameValuePair>();  
params.add(new BasicNameValuePair("user", "��С��"));  
params.add(new BasicNameValuePair("pawd", "123"));
String param = URLEncodedUtils.format(params, "UTF-8"); 
HttpGet httpGet = new HttpGet("http://www.baidu.com"+"?"+param);

```

##4. ʹ��HttpClient����Post����

����POST�����GET��΢����һ�㣬������`HttpPost`�����ͨ��`NameValuePair`�������洢�ȴ��ύ�Ĳ����������������ݵ�`UrlEncodedFormEntity`�У�������`setEntity(entity)`��ɣ� `HttpClient.execute(HttpPost)`���ɡ�

```java
private void PostByHttpClient(final String url)
{
    new Thread()
    {
        public void run() 
        {
            try{
                HttpClient httpClient = new DefaultHttpClient();
                HttpPost httpPost = new HttpPost(url);
                List<NameValuePair> params = new ArrayList<NameValuePair>();
                params.add(new BasicNameValuePair("user", "����"));
                params.add(new BasicNameValuePair("pawd", "123"));
                UrlEncodedFormEntity entity = new UrlEncodedFormEntity(params,"UTF-8");
                httpPost.setEntity(entity);
                HttpResponse httpResponse =  httpClient.execute(httpPost);
                if (httpResponse.getStatusLine().getStatusCode() == 200) {
                    HttpEntity entity2 = httpResponse.getEntity();
                    detail = EntityUtils.toString(entity2, "utf-8");
                    handler.sendEmptyMessage(SHOW_DATA);
                }
            }catch(Exception e){e.printStackTrace();}
        };
    }.start();
}
```