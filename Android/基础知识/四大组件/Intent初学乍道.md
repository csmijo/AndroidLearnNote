#Intent��ѧէ��

`Android` `Intent`

--

##1. Intent���ݼ���

###1) `List<�����������ͻ���String>`

**д�뼯�ϣ�**

```java
intent.putStringArrayListExtra(name, value)
intent.putIntegerArrayListExtra(name, value)
```

**��ȡ���ϣ�**

```java
intent.getStringArrayListExtra(name)
intent.getIntegerArrayListExtra(name)
```

###2) `List<Object>`

��listǿ��ת����Serializable���ͣ�Ȼ����(ʹ��Bundle��ý��)

**ע�⣺**Object����Ҫʵ��Serializable�ӿ�

**д�뼯�ϣ�**

```java
putExtras(key, (Serializable)list)
```

**��ȡ���ϣ�**

```java
(List<Object>) getIntent().getSerializable(key)
```

###3) `Map<String,Object>,������ӵ�`
**���������** ���Ƕ��List

```java
//���ݸ���Щ�Ĳ��� 
Map<String, Object> map1 = new HashMap<String, Object>();  
map1.put("key1", "value1");  
map1.put("key2", "value2");  
List<Map<String, Object>> list = new ArrayList<Map<String, Object>>();  
list.add(map1);  

Intent intent = new Intent();  
intent.setClass(MainActivity.this,ComplexActivity.class);  
Bundle bundle = new Bundle();  

//�붨��һ��list������budnle�д�����Ҫ���ݵ�ArrayList<Object>,����Ǳ���Ҫ��  
ArrayList bundlelist = new ArrayList();   
bundlelist.add(list);   
bundle.putParcelableArrayList("list",bundlelist);  
intent.putExtras(bundle);                
startActivity(intent); 
```

##2. Intent���ݶ���

�������ݶ���ķ�ʽ�����֣�**������ת��ΪJson�ַ���**����**ͨ��Serializable,Parcelable���л�**��

###1. ������ת��Json�ַ�������

����������ʹ��Android���õĿٽ�Json����������ʹ��fastjson����Gson�������⣡

**д������**

```java
Book book=new Book();
book.setTitle("Java���˼��");
Author author=new Author();
author.setId(1);
author.setName("Bruce Eckel");
book.setAuthor(author);
Intent intent=new Intent(this,SecondActivity.class);
intent.putExtra("book",new Gson().toJson(book));
startActivity(intent);
```

**��ȡ����**

```java
String bookJson=getIntent().getStringExtra("book");
Book book=new Gson().fromJson(bookJson,Book.class);
Log.d(TAG,"book title->"+book.getTitle());
Log.d(TAG,"book author name->"+book.getAuthor().getName());
```

###2. ʹ��Serializable��Parcelable���л�����

####1) Serializableʵ�֣�

* ҵ��`Bean`ʵ��`Serializable`�ӿڣ�д�ϱ�����`getter()`��`setter()`����;
* Intentͨ������`putExtra(String name, Serializable value)`�������ʵ������Ȼ�����ж���Ļ�����Ļ�,����Ҳ������`Bundle.putSerializable(x,x)`����`Intent.putExtras()`����;
* ��`Activity`����`getSerializableExtra()`������ö���ʵ��:
```java
Product pd = (Product) getIntent().getSerializableExtra("Product");
```
* ���ö���get���������Ӧ����

####2) Parcelableʵ�֣�

**a. һ�����̣�**

* ҵ��`Bean`�̳�`Parcelable`�ӿ�,��д`writeToParcel`����,����Ķ������л�Ϊһ��`Parcel`����;
* `��дdescribeContents`���������ݽӿ�������Ĭ�Ϸ���`0`�Ϳ���
* ʵ������̬�ڲ�����`CREATOR`ʵ�ֽӿ�`Parcelable.Creator`
* ͬ��ʽͨ��`Intent`��`putExtra()`�����������ʵ��,��Ȼ�������Ļ�,���ǿ����ȷŵ�`Bundle`��`Bundle.putParcelable(x,x)`,��`Intent.putExtras()`����

**b. һЩ���ͣ�**

����ͨ��`writeToParcel`����Ķ���ӳ���`Parcel`������ͨ��`createFromParcel`��`Parcel`����ӳ�� ����Ķ���Ҳ���Խ�`Parcel`������һ������ͨ��`writeToParcel`�Ѷ���д�������棬 ��ͨ��`createFromParcel`�������ȡ����ֻ�������������Ҫ����ʵ�֣����**д��˳��Ͷ���˳�����һ��**��

**c. ʵ��Parcelable�ӿڵĴ���ʾ����**

```java
//Internal Description Interface,You do not need to manage  
@Override  
public int describeContents() {  
     return 0;  
}  
       
      
 
@Override  
public void writeToParcel(Parcel parcel, int flags){  
    parcel.writeString(bookName);  
    parcel.writeString(author);  
    parcel.writeInt(publishTime);  
}  
      

public static final Parcelable.Creator<Book> CREATOR = new Creator<Book>() {  
    @Override  
    public Book[] newArray(int size) {  
        return new Book[size];  
    }  
          
    @Override  
    public Book createFromParcel(Parcel source) {  
        Book mBook = new Book();    
        mBook.bookName = source.readString();   
        mBook.author = source.readString();    
        mBook.publishTime = source.readInt();   
        return mBook;  
    }  
};
```
####3) �������л���ʽ�ıȽ�

���ߵıȽ�:
* **��ʹ���ڴ��ʱ��`Parcelable`��`Serializable`���ܸ�**�������Ƽ�ʹ��`Parcelable`
* `Serializable`�����л���ʱ��������������ʱ�������Ӷ�����Ƶ����GC��
* `Parcelable`**����ʹ����Ҫ�����ݴ洢�ڴ����ϵ����**����Ϊ������б仯�������`Parcelable`���ܺܺõı�֤���ݵĳ����ԡ�����`Serializable`Ч�ʵ͵㣬����ʱ���ǽ���ʹ��Serializable��

##3. Intent����Bitmap

bitmapĬ��ʵ��Parcelable�ӿڣ�ֱ�Ӵ��ݼ��ɡ�

```java
Bitmap bitmap = null;
Intent intent = new Intent();
Bundle bundle = new Bundle();
bundle.putParcelable("bitmap", bitmap);
intent.putExtra("bundle", bundle);
```

##4. ����ȫ������

��������Ǵ��ݼ򵥵����ݣ�������������`Activity1` -> `Activity2` -> `Activity3` -> `Activity4`�� ������`Activity`�д���ĳ�����ݵ�`Activity4`�У���ô�ƣ�һ����ҳ�洫ô��

������Ȼ����ѧ�ǰɣ��������ĳ�����ݿ������κεط����ܻ�ȡ������Ϳ��Կ���ʹ�� `Application`ȫ�ֶ����ˣ�

����**Androidϵͳ��ÿ���������е�ʱ�򴴽�һ��`Application`���󣬶���ֻ�ᴴ��һ��**������`Application`�ǵ���(singleton)ģʽ��һ���࣬����`Application`���������������������������ģ�**�����������ڵ�������������������**��

���������洢һЩ�Ⱦ�̬��ֵ(�̶����ı�ģ�Ҳ���Ա�)���������ʹ�� `Application`����Ҫ�Զ�����ʵ��`Application��`�����Ҹ���ϵͳʵ�������������Զ����`Application`����ϵͳĬ�ϵģ�����һ����������`AndroidManifest.xml`��Ϊ���ǵ�`application`��ǩ���`:name`���ԣ�

**ע�����**

����`Application`�����Ǵ������ڴ��еģ�Ҳ���������ܻᱻϵͳɱ�������������ĳ�����

����������`Activity1`����`application`�д洢���û��˺ţ�Ȼ����`Activity2`�л�ȡ���û��˺ţ�������ʾ��

����������ǵ��`home`����Ȼ�����N�ú�ϵͳΪ�˻����ڴ�kill�������ǵ�app�����ʱ���������� �����app�����ʱ�������ģ��ص���`Activity2`��ҳ�棬����������ʱ������ȥ��ȡ`Application`����û��˺ţ�����ͻᱨ`NullPointerException`��Ȼ��crash��~

����֮���Իᷢ������`crash`��**����Ϊ���`Application`������ȫ�´�����**����������ΪApp�����������ģ� ��ʵ�����ǣ������Ǵ���һ���µ�`Application`��Ȼ�������ϴ��û��뿪ʱ��`Activity`���Ӷ�����`App`��û�б�ɱ���ļ���**��������ǱȽ���Ҫ�����ݵĻ��������㻹�ǽ��б��ػ���������ʹ�����ݵ�ʱ�� Ҫ�Ա�����ֵ���зǿռ�飡**

��������һ����ǣ�**��ֹ��`Application`���������������������Լ�������̬����**Ҳ������~

--
**�ο����ף�**
* [Intent֮�������ݵĴ���](http://www.runoob.com/w3cnote/android-tutorial-intent-pass-data.html "")
