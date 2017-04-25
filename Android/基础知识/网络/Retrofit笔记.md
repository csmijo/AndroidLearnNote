#Retrofit�ʼ�

`Android` `Retrofit`

--

##1. Retrofitע�����

����Retrofit����22��ע�⣬���Է�Ϊ������н��͡�

### 1. ��һ�ࣺ HTTP���󷽷�

![HTTP���󷽷�ע��](http://upload-images.jianshu.io/upload_images/1724103-db95c51539b62c96.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240 "HTTP���󷽷�ע��")

������������ܵ�**HTTP** ע����Դ�������������һ��ע�⣬�����������ԣ�`method`,`path`,`hasBody`��
* method ��ʾ����ķ����������ִ�Сд
* path ��ʾ·��
* hasBody ��ʾ�Ƿ���������

**ʾ����**

```java
public interface BlogService{

    @HTTP(method = "get", path = "blog/{id}", hasBody = false)
    Call<ResponseBody> getFirstBlog(@Path("id") int id);
}
```


### 2. �ڶ��ࣺ �����
![�����](http://upload-images.jianshu.io/upload_images/1724103-4d09b5595bfb3291.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 3. �����ࣺ������
![������](http://upload-images.jianshu.io/upload_images/1724103-073abf80aacf492e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* **עһ��** {ռλ��}��`Path`����ֻ����URL��path���֣�url�еĲ���ʹ��`Query`��`QueryMap`���棬��֤�ӿڶ���ļ��
* **ע����** `Query`��`Field`��`Part`�����߶�֧��`����`��ʵ����`Iterable`�ӿڵ����ͣ���List��set�ȣ��������̨�������顣


##2. Gson��Converter

����**��Ĭ�������Retrofitֻ֧�ֽ�HTTP����Ӧ��ת��ΪResponseBody**�����Ƿ���ֵCall֧�ַ��ͣ��Ǿ�˵�����Ͳ����������������͵ġ�**��`Converter`����RetrofitΪ�û��ṩ�Ľ�`ResponseBody`ת������Ҫ�����͵�**��

��Ȼֻ�Ǹı䷺�͵Ĳ����ǲ��еģ�������Ҫ�ڴ���Retrofitʱ**��ȷ��֪**���ڽ�`ResponseBody`ת�������Ƿ����е�����ʱ��Ҫʹ�õ�`Converter`��

���磬�����Gson��֧�֣�
```
compile 'com.squareup.retrofit2:converter-gson:2.0.2'
```

ͨ��`GsonConverterFactory`ΪRetrofit���Gson֧�֣�
```
Gson gson = new GsonBuilder()
        .setDateFormat("yyyy-MM-dd hh:mm:ss")
        .create();
        
Retrofit retrofit = new Retrofit.Builder()
        .baseUrl("http://gank.io/api/")
        .addConverterFactory(GsonConverterFactory.create(gson))
        .build();
```

##3. ����

* **`Retrofit`**: ���������װ��
* **`okHttp`**: ��������client
* **`RxJava`**: �����첽���������԰���������ŵ����߳���ִ�У�Ȼ����������ŵ����߳���ȥ����
* `Retrofit`��`okHttp`�Ĺ�ϵ��: `Retrofit`��Ҫ������������ݺ�����Ľ����ʹ�ýӿڵ���ʽ�����֣�`okHttp`��Ҫ������������Ĺ��̣���ӡlog�����粻�ȶ���״̬�½��������ӣ����ó�ʱ�ȡ����仰˵��`Retrofit`������**ͷ��β**��**okHttp**�����м䲿�֡�



--

**�ο�����**
* [����Ļ���Retrofit2��?Retrofit2��ȫ�̳�](http://www.jianshu.com/p/308f3c54abdd)