# python������ʽѧϰ�ʼ�

`python` `������ʽ`


---

## 1. ������ʽ�﷨

### 1.1 ������ʽ���÷���

http://www.cnblogs.com/huxi/archive/2010/07/04/1771073.html

|����|����|
|:--|:--|
|.|ƥ�������ַ������������з� \n |
|^|ƥ���ַ����Ŀ�ʼ|
|$|ƥ���ַ����Ľ��������ַ����Ľ�β�µ�һ�еĿ�ʼ|
|*|ƥ��ǰһ���ַ� 0 �λ��� ���޴�|
|+|ƥ��ǰһ���ַ� 1 �λ��� ���޴�|
|[]|ƥ���ַ���������ַ�|
|\||���ߣ�A|B ��ʾƥ�� A ���� B|
|?|ƥ��ǰһ���ַ� 0 �λ��� 1 ��|
|.*|̰���㷨|
|.*?|��̰���㷨|
|()|�����ڵ�������Ϊ�������|
|\A|ֻƥ���ַ����Ŀ�ʼ|
|\Z|ֻƥ���ַ����Ľ���|
|\b|ֻƥ������ڿ�ʼ�ͽ�β�Ŀ��ַ�|
|\B|ֻƥ�䲻�����ڿ�ʼ�ͽ���Ŀ��ַ�|
|\d|ֻƥ�����֣��൱��[0-9]|
|\D|ƥ������֣��൱��[^0-9]|
|\s|ƥ������Ŀ��ַ����൱��[\t\n\r\f\v]|
|\S|ƥ������ķǿ��ַ����൱��[^\t\n\r\f\v]|
|\w|ƥ��������ַ����൱��[a-zA-z0-9].����� rs.L ģʽ�����ƥ��[0-9]���ڵ�ǰ�������϶�Ϊ�ַ����ַ���|
|\W|ƥ�����з� \\w ƥ����ַ�|
|\\\|ƥ�䷴б�� \\|


### 1.2 ������ʽƥ��ģʽ

|ƥ��ģʽ|����|
|:--|:--|
|re.I|�����ִ�Сд����ƥ��|
|re.L|Make \w, \W, \b, \B, dependent on the current locale|
|re.M|����ƥ��ģʽ��^ ƥ������ַ����Ŀ�ʼ�� $ ƥ������ַ����Ľ���|
|re.S|"."ƥ�����е��ַ����������з� \n|
|re.X|���Կո��ע��|
|re.U|Make \w, \W, \b, \B, dependent on the Unicode locale|

### 1.3 ������ʽ���÷���

|������|����|
|:--|:--|
|findall|ƥ�����з��Ϲ��ɵ����ݣ����ذ���������б�|
|search|ƥ�䲢��ȡ��һ�����Ϲ��ɵ����ݣ�����һ��������ʽ����(object)|
|match|���ַ��Ŀ�ʼƥ��������ʽ|
|sub|�滻���Ϲ��ɵ����ݣ������滻���ֵ|
|subn|�滻���Ϲ��ɵ����ݣ������滻���ֵ���滻�ĸ���|
|split|ʹ��������ַ������зָ�|
|escape|���ڽ�string�е�������ʽԪ�ַ���*/+/?��֮ǰ����ת����ٷ��أ�����Ҫ����ƥ��Ԫ�ַ�ʱ����ôһ����|

## 2. ������ʽʵ��

### 2.1 match(string[, pos[, endpos]]) | re.match(pattern, string[, flags]): 

�����������`string`��`pos`�±괦����ƥ��pattern:
    
* ���`pattern`����ʱ�Կ�ƥ�䣬�򷵻�һ��`Match`����
* ���ƥ�������`pattern`�޷�ƥ�䣬����ƥ��δ�������ѵ���`endpos`���򷵻�`None`�� 

* `pos`��`endpos`��Ĭ��ֵ�ֱ�Ϊ 0 ��`len(string)`��`re.match()`�޷�ָ��������������
* ���� `flags` ���ڱ��� `pattern` ʱָ��ƥ��ģʽ�� 

ע�⣺���������������ȫƥ�䡣��`pattern`����ʱ��`string`����ʣ���ַ�����Ȼ��Ϊ�ɹ�����Ҫ��ȫƥ�䣬�����ڱ��ʽĩβ���ϱ߽�ƥ���`'$'`�� 

```
#!/usr/bin/python
# -*- coding: UTF-8 -*- 
 
import re
print(re.match('www', 'www.runoob.com').span())  # ����ʼλ��ƥ��
print(re.match('com', 'www.runoob.com'))         # ������ʼλ��ƥ��
```
����ʵ������������Ϊ��
```
(0, 3)
None
```


```
#!/usr/bin/python
import re
 
line = "Cats are smarter than dogs"
 
matchObj = re.match( r'(.*) are (.*?) .*', line, re.M|re.I)
 
if matchObj:
   print "matchObj.group() : ", matchObj.group()
   print "matchObj.group(1) : ", matchObj.group(1)
   print "matchObj.group(2) : ", matchObj.group(2)
else:
   print "No match!!"
```
����ʵ���Ľ��Ϊ��
```
matchObj.group() :  Cats are smarter than dogs
matchObj.group(1) :  Cats
matchObj.group(2) :  smarter
```


### 2.2 search(string[, pos[, endpos]]) | re.search(pattern, string[, flags]): 

����������ڲ����ַ����п���ƥ��ɹ����Ӵ�����`string`��`pos`�±괦����ƥ��`pattern`:
* ���`pattern`����ʱ�Կ�ƥ�䣬�򷵻�һ��`Match`����
* ����޷�ƥ�䣬��`pos`�� 1 �����³���ƥ�䣻ֱ��`pos=endpos` ʱ���޷�ƥ���򷵻�`None`�� 
* `pos`��`endpos`��Ĭ��ֵ�ֱ�Ϊ 0 ��`len(string)`,`re.search()`�޷�ָ��������������
* ���� `flags` ���ڱ��� `pattern` ʱָ��ƥ��ģʽ�� 

```
#!/usr/bin/python
# -*- coding: UTF-8 -*- 
 
import re
print(re.search('www', 'www.runoob.com').span())  # ����ʼλ��ƥ��
print(re.search('com', 'www.runoob.com').span())         # ������ʼλ��ƥ��
```
����ʵ������������Ϊ��

```
(0, 3)
(11, 14)
```


```
#!/usr/bin/python
import re
 
line = "Cats are smarter than dogs";
 
searchObj = re.search( r'(.*) are (.*?) .*', line, re.M|re.I)
 
if searchObj:
   print "searchObj.group() : ", searchObj.group()
   print "searchObj.group(1) : ", searchObj.group(1)
   print "searchObj.group(2) : ", searchObj.group(2)
else:
   print "Nothing found!!"
```
����ʵ��ִ�н�����£�
```
searchObj.group() :  Cats are smarter than dogs
searchObj.group(1) :  Cats
searchObj.group(2) :  smarter
```


### 2.3 findall(string[, pos[, endpos]]) | re.findall(pattern, string[, flags]): 

����string�����б���ʽ����ȫ����ƥ����Ӵ���

```
import re
 
p = re.compile(r'\d+')
print p.findall('one1two2three3four4')
 
### output ###
# ['1', '2', '3', '4']
```

### 2.4 re.sub(pattern, repl, string, count=0, flags=0)

������
* `pattern` : �����е�ģʽ�ַ�����
* `repl` : �滻���ַ�����Ҳ��Ϊһ��������
* `string` : Ҫ�������滻��ԭʼ�ַ�����
* `count` : ģʽƥ����滻����������Ĭ�� 0 ��ʾ�滻���е�ƥ�䡣


```
#!/usr/bin/python
# -*- coding: UTF-8 -*-
 
import re
 
phone = "2004-959-559 # ����һ������绰����"
 
# ɾ���ַ����е� Pythonע�� 
num = re.sub(r'#.*$', "", phone)
print "�绰������: ", num
 
# ɾ��������(-)���ַ��� 
num = re.sub(r'\D', "", phone)
print "�绰������ : ", num
```

����ʵ��ִ�н�����£�

```
�绰������:  2004-959-559 
�绰������ :  2004959559
```