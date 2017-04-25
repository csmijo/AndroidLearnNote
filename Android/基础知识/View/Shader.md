# Shader

`Android` `Shader`

---

## 1. ���

[�ٷ�����](https://developer.android.google.cn/reference/android/graphics/Shader.html)��
```xml
Shader is the based class for objects that return horizontal spans of colors during drawing. A subclass of Shader is installed in a Paint calling
paint.setShader(shader). After that any object (other than a bitmap) that is drawn with that paint will get its color(s) from the shader.
```

Android �ж� Shader ���������͵ģ�
```
Shader ��һ�ֻ����������ͼ�λ��ƹ����з���һ�ζ���ɫֵ��ͨ������ Paint.setShader() ����������
���������లװ�����ʣ����� Paint �����ڻ��ƹ���������ȡ����ɫ�������� Shader ����
```

�����ᵽ��Shader�����࣬Shader ��5������ `BitmapShader`, `ComposeShader`, `LinearGradient`, `RadialGradient`,`SweepGradient`�� ���ĵ�Ŀ��Ҳ�Ƿֱ����ĸ������ࡣ

## 2. ͼƬ��Ⱦ�� BitmapShader

**BitmapShader** ��һ��ͼƬ��������������(�� `OpenGL` �У����������ͼ����˼���������Ϊһ��û����ɫ�������α�������һ��ͼƬ�������Ӿ�Ч������һ�������ε�ͼƬ)��������ͼƬ����ͨ������ `BitmapShader` �� `tiling mode` ���ﵽ������ظ���Ч����
```
BitmapShader(Bitmap bitmap, Shader.TileMode tileX, Shader.TileMode tileY)
```
������ `BitmapShader` �Ĺ��췽����

* bitmap ��ָ����ͼƬ
* tileX ��ָ��X������� `tiling mode`
* tileY ��ָ��Y������� `tiling mode`

�ܶ��˿��������ʣ���� `TileMode` ��ʲô��

### 1. ����Ī���TileMode

ʲô�� TileMode �أ� ��ʵ����ֻ��һ��ö�ٶ��ѡ�**��ֻ������ֵ**��

* **Shader.TileMode CLAMP**
* **Shader.TileMode MIRROR**
* **Shader.TileMode REPEAT**

#### 1. CLAMP

������˼��Ҫ���Ƶ��������ͼƬ�����������ʱ��������Ŀռ�λ�ý�������ͼƬ�ı�Ե��ɫ���

#### 2. MIRROR

���ģʽ�ܹ��������Ծ���ķ�ʽ��X��Y������

#### 3. REPEAT

���������ǽ�ͼƬ������XY����и��ơ�


---
[�ο�����]

* [��ͼCanvasʮ�˰�����֮Shader��⼰ʵս](http://mp.weixin.qq.com/s/3SX79GGZFoIPoxIRugAkoQ)
* [Android��ͼCanvasʮ�˰�����֮Shader��⼰ʵսƪ(��)](http://blog.csdn.net/briblue/article/details/53694042)
