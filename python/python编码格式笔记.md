# Python2 �����ʽ�ʼ�

`python`

---

## 1. Python2 �� encode �� decode

Python �У�����ʹ�� `decode()` �� `encode()` �������н���ͱ��룬���Ǿ��������ļ���ȡ�ı����ָ��ִ���ʮ�ֵı����ġ�����Ҫ�Ƕ� Python �ı����ʽ���Ĳ��㵼�µġ�

�� Python ��ʹ�� `Unicode` ������Ϊ����Ļ�����Ҳ����˵��

```
    decode         encode
  str ---> unicode ---> str 
```

ͨ���м��� `unicode` �����ʽ���������ĸ��ָ�ʽ֮���ת��

#### 1.1 �ļ���ȡʵ��

�Դ��ļ���ȡ����Ϊ����������ļ������ʽΪ `UCS-2 little Endian`(Fiddler �����ļ����ļ��ı����ʽ�����˺þ�)�� ϣ����ȡ�ļ������ݲ����н�һ���Ĵ���

���ճ���ķ�ʽ��
```
f = open('test.txt','r')
s = f.readline()
print s
```

������ֿ���̨�����һЩ���ݣ����Ǹ�ʽ��ȫ����ȷ����

��һ�뷨�;������ļ���������⣬�޸����ļ���Ĭ�ϱ��뷽ʽΪ `UTF-8` ���ٴ���������Ľű���û�����⣬��ô�ͽ���ת��ඡ�

ʹ�� `chardet` ��⵽�ļ��ı���Ϊ `UTF-16`�����Ծͳ��Խ��������µĲ������������ `chardet`.

```
f = open('test.txt','r')
str = f.readline()
ss = str.decode('utf-16').encode('utf-8')
print ss
```

��������������Ĵ���
```
Traceback (most recent call last):
  ss = str.decode('utf-16').encode('utf-8')
  File "D:\program\python2.7.10\lib\encodings\utf_16.py", line 16, in decode
    return codecs.utf_16_decode(input, errors, True)
UnicodeDecodeError: 'utf16' codec can't decode byte 0x0a in position 1580: truncated data
```

���Ǿ�����һ���ܴ��Ȧ�ӣ���ôת `UCS-2` �� `UTF-8` �ȵȣ������ʹ�� Python �ṩ�� `codecs` �����ļ��Ķ�ȡ��������� `open()` ��������ָ����������ͣ����£�
```
import codecs

f = codecs.open('text.txt','r',"UTF-16")
str = f.readline()
print str
print type(str)
```

����̨��ӡ��ϢΪ��
```
test

<type 'unicode'>
```

ok ��ת�� `unicode` �ͺð��ˣ�Ȼ��Ϳ���ʹ�� `encode()` �������������ʽ��ת���ˡ�

## 2 chardet ʹ��

`chardet` ģ����Լ���ַ����룬Ӧ��˵������������ռ������

### 2.1 ��װ `chardet`
 
1. ����һ������ʹ�� `pip install chardet` �����а�װ
2. ��������
    * �����ڹ��� https://pypi.python.org/pypi/chardet ���� `chardet_3.0.3.tar.gz` ��
    * ��ѹ�� `Python` ��װĿ¼�� `site-packages` Ŀ¼��
    * ���뵽 `chardet_3.0.3.tar.gz` �Ľ�ѹĿ¼������ `python setup.py install` �������а�װ
3. �����Ŀӣ�
    
��ʹ���������ַ�����װ��ʱ�򣬶������������Ĵ���
```
pip install fails with ��connection error: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed ��
```

Ӧ���� `https` ֤����֤�����⣬������ `stackoverflow` ���ҵ��������Ľ��������

```
pip install --index-url=http://pypi.python.org/simple/ --trusted-host pypi.python.org  chardet
```

���Ժ�װ�ɹ�

### 2.2 ʹ�� chardet ����ļ��ı����ʽ

�������£�
```
import chardet

with open(path) as f:
    str = f.read()
    print chardet.detect(str)
```

����̨������£�

```
{'confidence': 1.0, 'language': '', 'encoding': 'UTF-16'}
```

����һ���ֵ䣬���Կ�����ǰ�ļ��ı��뷽ʽΪ `UTF-16`�������Ϳ����� `codecs.open()` ������ʹ���ˡ�


---

[�ο�����]

* [Python�����ʽ˵����ת�뺯��encode��decode��ʹ��](http://blog.csdn.net/mfcing/article/details/43058591)
* [pip install fails with ��connection error: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed (_ssl.c:598)��](http://stackoverflow.com/questions/25981703/pip-install-fails-with-connection-error-ssl-certificate-verify-failed-certi)
* [Python | ���ֱ����ļ������ģ�����������](http://jingyan.baidu.com/article/425e69e6e111a1be15fc1609.html)
* [Python_�����޸��ļ��ı����ʽ](http://blog.csdn.net/vagerant/article/details/50350171)
