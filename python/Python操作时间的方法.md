# python ����ʱ������ڵķ���

`python`

---


## 1. ����ʱ������ڵķ���

http://www.jb51.net/article/47957.htm

ʱ����صĶ�Ҫ�õ� `datetime` �� `time` ��������׼��ģ��

### 1. ���ַ�����ʱ��ת��ʱ���

```
>>> import time
>>> a = "2017-5-17 18:25:39"
>>> timeArray = time.strptime(a,"%Y-%m-%d %H:%M:%S")
>>> timeStamp = int(time.mktime(timeArray))
>>> timeStamp
1495016739
```

### 2. ���ַ���ת�� datetime ��ʽ

```
>>> import datetime
>>> t = "2017-5-18-14-34-24"
>>> datetime.datetime.strptime(t,"%Y-%m-%d-%H-%M-%S")
datetime.datetime(2017, 5, 18, 14, 34, 24)
```

### 3. ��ʽ����

�� a = "2017-5-17 18:25:39" �����Ϊ a = "2017/5/17 18:25:39"

**��ת��Ϊʱ�����飬Ȼ����ת��Ϊ������ʽ**

```
>>> import time
>>> a = "2017-5-17 18:25:39"
>>> timeArray = time.strptime(a,"%Y-%m-%d %H:%M:%S")
>>> otherStyle = time.strftime("%Y/%m/%d %H:%M:%S",timeArray)
>>> otherStyle
'2017/05/17 18:25:39'
```

### 4. ʱ���ת��Ϊָ����ʽ����

#### ����һ�� ����localtime()ת��Ϊʱ������,Ȼ���ʽ��Ϊ��Ҫ�ĸ�ʽ

```
>>> import time
>>> timeStamp = 1495016739
>>> timeArray = time.localtime(timeStamp)
>>> otherStyle = time.strftime("%Y/%m/%d %H:%M:%S",timeArray)
>>> otherStyle
'2017/05/17 18:25:39'
```

#### ��������ʹ�� datetime

```
>>> import datetime
>>> timeStamp = 1495016739
>>> dateArray = datetime.datetime.utcfromtimestamp(timeStamp)
>>> otherStyle = dataArray.strftime("%Y-%m-%d %H:%M:%S")
>>> otherStyle
'2017-05-17 10:25:39'
```

### 5. ��ȡ��ǰʱ�䲢ת��Ϊָ�����ڸ�ʽ

#### ����һ�� ʹ�� time

```
>>> import time
>>> now = int(time.time())
>>> timeArray = time.localtime(now)
>>> otherStyle = time.strftime("%Y-%m-%d %H:%M:%S",timeArray)
>>> otherStyle
'2017-05-18 10:55:28'
```

#### �������� ʹ�� datetime

```
>>> import datetime
>>> now = datetime.datetime.now()
>>> otherStyle = now.strftime("%Y-%m-%d %H:%M:%S")
>>> otherStyle
'2017-05-18 10:58:10'
```

### 6. ��ȡ����ǰ��ʱ��ķ���

```
>>> import time
>>> import datetime
>>> threeDayAgo = (datetime.datetime.now()-datetime.timedelta(days=3))
>>> otherStyle = threeDayAgo.strftime("%Y-%m-%d %H:%M:%S")
>>> otherStyle
'2017-05-15 11:07:11'
```
**ע�⣺**  `timedelta()` �����Ĳ����У� `days`,`hours`,`seconds`,`microseconds`

####  ��ʽת��

```
>>> import time
>>> import datetime
>>> now = datetime.datetime.now()  # ��ȡ��ǰʱ�䣬type Ϊ�� datetime.datetime
>>> now
datetime.datetime(2017, 5, 18, 11, 13, 25, 877000)
>>> type(now)
<type 'datetime.datetime'>


>>> now.timetuple()  # ��ȡ datetime.datetime �� timetuple()
time.struct_time(tm_year=2017, tm_mon=5, tm_mday=18, tm_hour=11, tm_min=13, tm_sec=25, tm_wday=3, tm_yday=138, tm_isdst=-1)
>>> timeStamp = int(time.mktime(now.timetuple()))  # ʹ�� time ת��Ϊʱ���
>>> timeStamp
1495077205

>>> nowTimetuple = time.localtime(timeStamp)  # ʹ�� time.localtime() �ֿ��Խ�ʱ���ת�� timetuple
>>> nowTimetuple
time.struct_time(tm_year=2017, tm_mon=5, tm_mday=18, tm_hour=11, tm_min=13, tm_sec=25, tm_wday=3, tm_yday=138, tm_isdst=0)
>>>
```

### 7. ����ʱ����������ʱ��ļ���ǰʱ��

��ת���� `datetime.datetime` ��ʽ��Ȼ����ʹ�� `timedelta()` ��������

```
>>> import time
>>> import datetime
>>> now = int(time.time())
>>> dateArray = datetime.datetime.utcfromtimestamp(now)
>>> dateArray
datetime.datetime(2017, 5, 18, 3, 24, 5)
>>> threeDayAgo = dateArray - datetime.timedelta(days=3)
>>> threeDayAgo
datetime.datetime(2017, 5, 15, 3, 24, 5)
```

### 8. �� Python ������������������

����ʹ�� `datetime.date.today()` ��ȡ����������ڣ�Ȼ��ʹ�� `datetime.datetime.timedelta()` ��������

```
>>> import datetime
>>> today = datetime.date.today()   # ��ȡ�����������
>>> today
datetime.date(2017, 5, 18)
>>> yesterday = today - datetime.timedelta(days=1)  # �������������
>>> yesterday
datetime.date(2017, 5, 17)
>>> tomorrow = today + datetime.timedelta(days=1)  # �������������
>>> tomorrow
datetime.date(2017, 5, 19)
```

### 9. ʹ�� Python ��ӡ��ǰʱ��

#### ����һ�� ʹ�� time
```
>>> import time
>>> time.strftime("%Y-%m-%d %H:%M:%S")
'2017-05-18 11:52:06'
```

#### �������� ʹ�� detetime

```
>>> import datetime
>>> datetime.datetime.now().timetuple()
time.struct_time(tm_year=2017, tm_mon=5, tm_mday=18, tm_hour=11, tm_min=53, tm_sec=9, tm_wday=3, tm_yday=138, tm_isdst=-1)
>>> datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
'2017-05-18 11:54:00'
```
### �������ں�ʱ��ĸ�ʽ������

```
%a ���ڼ��ļ�д
%A ���ڼ���ȫ��
%b �·ֵļ�д
%B �·ݵ�ȫ��
%c ��׼�����ڵ�ʱ�䴮
%C ��ݵĺ���λ����
%d ʮ���Ʊ�ʾ��ÿ�µĵڼ���
%D ��/��/��
%e �����ַ����У�ʮ���Ʊ�ʾ��ÿ�µĵڼ���
%F ��-��-��
%g ��ݵĺ���λ���֣�ʹ�û����ܵ���
%G ��֣�ʹ�û����ܵ���
%h ��д���·���
%H 24Сʱ�Ƶ�Сʱ
%I 12Сʱ�Ƶ�Сʱ
%j ʮ���Ʊ�ʾ��ÿ��ĵڼ���
%m ʮ���Ʊ�ʾ���·�
%M ʮʱ�Ʊ�ʾ�ķ�����
%n ���з�
%p ���ص�AM��PM�ĵȼ���ʾ
%r 12Сʱ��ʱ��
%R ��ʾСʱ�ͷ��ӣ�hh:mm
%S ʮ���Ƶ�����
%t ˮƽ�Ʊ��
%T ��ʾʱ���룺hh:mm:ss
%u ÿ�ܵĵڼ��죬����һΪ��һ�� ��ֵ��0��6������һΪ0��
%U ����ĵڼ��ܣ�����������Ϊ��һ�죨ֵ��0��53��
%V ÿ��ĵڼ��ܣ�ʹ�û����ܵ���
%w ʮ���Ʊ�ʾ�����ڼ���ֵ��0��6��������Ϊ0��
%W ÿ��ĵڼ��ܣ�������һ��Ϊ��һ�죨ֵ��0��53��
%x ��׼�����ڴ�
%X ��׼��ʱ�䴮
%y �������͵�ʮ������ݣ�ֵ��0��99��
%Y �����Ͳ��ֵ�ʮ�����
%z��%Z ʱ�����ƣ�������ܵõ�ʱ�������򷵻ؿ��ַ���
%% �ٷֺ�
```