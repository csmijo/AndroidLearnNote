#Android HTTP����ʽ��HttpURLConnection

`Android` `HttpURLConnection`

--

##1. HttpURLConnection�Ľ���

��������һ�ֶ���;����������HTTP�ͻ��ˣ�ʹ����������HTTP�������������ڴ������Ӧ�ó��� ��Ȼ`HttpURLConnection`��API�ṩ�ıȽϼ򵥣�����ͬʱ��Ҳʹ�����ǿ��Ը������׵�ȥʹ�ú���չ����**�̳���URLConnection�������࣬�޷�ֱ��ʵ��������ͨ������`openCollection()` ������ö���ʵ����Ĭ���Ǵ�gzipѹ����**��


##2. HttpURLConnectionʹ��ʾ��

###1��������

����������HttpURLConnection��Get��Post��ʽʱ��ʹ��conn.getInputStream()��õ���һ����������������Ҫһ���ཫ**��**ת����**����������**��

```java
public class StreamTool {
    // ������ȡ����
    public static byte[] read(InputStream inStream) throws Exception{
        ByteArrayOutputStream outStream = new ByteArrayOutputStream();
        byte[] buffer = new byte[1024];
        int len = 0;
        while((len = inStream.read(buffer)) != -1)
        {
            outStream.write(buffer,0,len);
        }
        inStream.close();
        return outStream.toByteArray();
    }
}
```

���⣬������ʹ��read�ķ�ʽ����**��**ֱ��ת��**�ַ���**��
```java
public static String read2(InputStream inStream) throws Exception{
BufferedReader reader = new BufferedReader(new InputStreamReader(in));
        StringBuilder response = new StringBuilder();
        String line;
        while ((line = reader.readLine()) != null){
            response.append(line);
        }
        /*��Դ�ͷ�*/
        in.close();
        // �����ַ���
        return response.toString();
}
```

###2) HttpURLConnection����Get�����ʾ��

```java
public class GetData {
    // 1. ��ȡ����ͼƬ����:
    public static byte[] getImage(String path) throws Exception {
        URL url = new URL(path);
        HttpURLConnection conn = (HttpURLConnection) url.openConnection();
        // �������ӳ�ʱΪ5��
        conn.setConnectTimeout(5000);
        // ������������ΪGet����
        conn.setRequestMethod("GET");
        // �ж�����Url�Ƿ�ɹ�
        if (conn.getResponseCode() != 200) {
            throw new RuntimeException("����urlʧ��");
        }
        InputStream inStream = conn.getInputStream();
        byte[] bt = StreamTool.read(inStream);
        inStream.close();
        return bt;
    }

    // 2. ��ȡ��ҳ��htmlԴ����
    public static String getHtml(String path) throws Exception {
        URL url = new URL(path);
        HttpURLConnection conn = (HttpURLConnection) url.openConnection();
        conn.setConnectTimeout(5000);
        conn.setRequestMethod("GET");
        if (conn.getResponseCode() == 200) {
            InputStream in = conn.getInputStream();
            byte[] data = StreamTool.read(in);
            in.close();
            String html = new String(data, "UTF-8");  //�Զ��������ݽ���UTF-8����
            return html;
        }
        return null;
    }
}
```

**ע�⣺**��Ҫ���Ǽ�������Ȩ��

`<uses-permission android:name="android.permission.INTERNET" />`


###3) HttpURLConnection����Post�����ʾ��

```java
public class PostUtils {
    public static String LOGIN_URL = "http://172.16.2.54:8080/HttpTest/ServletForPost";
    public static String LoginByPost(String number,String passwd)
    {
        String msg = "";
        try{
            HttpURLConnection conn = (HttpURLConnection) new URL(LOGIN_URL).openConnection();
            /* ��������ʽ,����ʱ��Ϣ */
            conn.setRequestMethod("POST");
            conn.setReadTimeout(5000);
            conn.setConnectTimeout(5000);
            //������������,���:
            conn.setDoOutput(true);
            conn.setDoInput(true);
            //Post��ʽ���ܻ���,���ֶ�����Ϊfalse
            conn.setUseCaches(false);
            //�������������:
            String data = "passwd="+ URLEncoder.encode(passwd, "UTF-8")+
                    "&number="+ URLEncoder.encode(number, "UTF-8");
            //�������дһЩ����ͷ�Ķ���...
            //��ȡ�����
            OutputStream out = conn.getOutputStream();
            out.write(data.getBytes());
            out.flush();
            
             if (conn.getResponseCode() == 200) {  
                    // ��ȡ��Ӧ������������  
                    InputStream is = conn.getInputStream();  
                    byte[] data = StreamTool.read(in);
                    // �����ַ���  
                    msg = new String(data,"UTF-8");  
                    return msg;
             }
        }catch(Exception e){e.printStackTrace();}
        return msg;
    }
}
```

--
**�ο����ף�**
* [Android HTTP����ʽ:HttpURLConnection](http://www.runoob.com/w3cnote/android-tutorial-httpurlconnection.html "")