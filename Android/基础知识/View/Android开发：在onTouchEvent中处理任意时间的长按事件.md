#��onTouchEvent�д�������ʱ��ĳ����¼�

`Android`

--
##A. ����һ ���������ţ�
###1. ��ʵ�ֵ�Ч��

����Android�ṩ��GestureDetector��������һЩ���õ����Ʋ���������˵ onLongPress,onFling �ȡ������ﲻʹ��GestureDetector������ֱ�����Զ���View��д��onTouchEvent�н��д���

������ʵ�ֵ�Ч���ǣ����ֻ���ס��Ļʱ�������ָ����ʱ����û���ƶ�����500���룩,��ô���볤��ģʽ����ʱ��ָ����Ļ���ƶ�����������ģʽ������ֻ���ס��Ļ�������ƶ�����ô�������ƶ�ģʽ��


###2. ʹ�õķ���

����MotionEvent ���ṩ�˼�¼��ǰ����ĺ�����**getX()**,**getY()**���͵�ǰ�¼�������ʱ��ĺ�����**getEventTime()**���Լ�����ʱ�䣨**getDowntime()**����MotionEventͬʱҲ�ṩ�˵�ǰ�Ĳ������ͣ����£�ACTION_DOWN���� �ƶ� ��ACTION_MOVE�������� ��ACTION_UP����������Щ���������Ǳ�������׵�ʵ����Ҫ��Ч���ˡ�

###3. ʵ��˼·

�����ڰ���ʱ��¼x,y�����Լ�����ʱ�䣬����һ���ƶ���ʱ���ȡ�ƶ���ʱ�䣬�������ָ���ĳ���ʱ�䣬��ô���볤��ģʽ�����������ͨ���ƶ�ģʽ�������ף���ģ��������ʵ�������Ч�������ǵ��������������ʱ��ȴ�޷�ʵ��������Ч����ԭ��ģ���������ʱ���ܹ���֤�ڲ��ƶ���������²�����ACTION_MOVE���������ȴ�����У�������ACTION_DOWN��ļ�����֮�������ͣ��ACTION_MOVE�ˡ�����һ�£���ʵֻҪ��΢��ͨ�±�����������Ҳʵ����ͬ��Ч���ˡ��Ǿ����ж�ACTION_MOVE��������ACTION_DOWN�������ƫ��ֵ�Ƿ�С������ָ����ƫ�����أ������ָ��ֵ�ڣ���ô��Ϊû���ƶ������������������������

```java
/**
	 * * �ж��Ƿ��г����������� * @param lastX ����ʱX���� * @param lastY ����ʱY���� *
	 * 
	 * @param thisX
	 *            �ƶ�ʱX���� *
	 * @param thisY
	 *            �ƶ�ʱY���� *
	 * @param lastDownTime
	 *            ����ʱ�� *
	 * @param thisEventTime
	 *            �ƶ�ʱ�� *
	 * @param longPressTime
	 *            �жϳ���ʱ��ķ�ֵ
	 */
	static boolean isLongPressed(float lastX, float lastY, float thisX,
			float thisY, long lastDownTime, long thisEventTime,
			long longPressTime) {
		float offsetX = Math.abs(thisX - lastX);
		float offsetY = Math.abs(thisY - lastY);
		long intervalTime = thisEventTime - lastDownTime;
		if (offsetX <= 10 && offsetY <= 10 && intervalTime >= longPressTime) {
			return true;
		}
		return false;
	}
```

������ACTION_DOWN��ʱ�򣬼�¼��lastX��lastY��lastDownTime��ʹ��getEventTime()����ACTION_MOVE��ʱ���жϵ�ǰ�Ƿ�Ϊ����ģʽ(���־�����ķ�ʽ)��������ǣ���ô��ȡ��ǰ��thisX��thisY��thisEventTime���ú��������жϡ�����������ACTION_UP�ｫ������־ֵΪFALSE��ACTION_DOWN������������:

```java
//����Ƿ񳤰�,�ڷǳ���ʱ��� 
	if(!mIsLongPressed){ 
		mIsLongPressed = isLongPressed(mLastMotionX, mLastMotionY, x, y, lastDownTime,eventTime,500); 
		} 
	if(mIsLongPressed){  
		//����ģʽ�������� 
		}else{  
			//�ƶ�ģʽ��������
	}
}
```


##B. �����������ţ�

###1. ����һȱ��

������ʹ�÷���һʵ�ֳ�������Dialog�Ĺ����У����ǻ���ֵ������Dialog�����������Debugʱ��ȷ������ԭ�����һ��Ѱ�ҡ���������
###2. ʵ��˼·

�����÷�����ActionDown��ʱ��postDelayһ��Runnable��ȥ��delay��ʱ����ǳ�����ʱ�䣬Ȼ����move����һ���������up ��ʱ�򣬰����delay��runnable�Ƴ������Ϳ��Դﵽ������Ч����

###3. ʵ�ִ���

```java
@Override
    public boolean onTouchEvent(MotionEvent event) {
        switch (event.getAction()) {
            case MotionEvent.ACTION_DOWN:
                touchView = null;

                startX = (int) event.getX();
                startY = (int) event.getY();
                startTime = event.getDownTime();

                if (hasView(startX, startY)) {
                   
                    /* �������� */ 
                    mHandler.postDelayed(new Runnable() {
                        @Override
                        public void run() {
                            longPressedAlertDialog();
                        }
                    }, PRESSREANGE);
                } 
                break;
            case MotionEvent.ACTION_MOVE:
                int lastX = (int) event.getX();
                int lastY = (int) event.getY();
                //�ƶ�
                moveView(lastX, lastY);

                if (Math.abs(lastX - startX) > CLICKRANGE || Math.abs(lastY - startY) > CLICKRANGE) {
                    this.mHandler.removeCallbacksAndMessages(null);
                }

                break;
            case MotionEvent.ACTION_UP:
                this.mHandler.removeCallbacksAndMessages(null);
                break;
        }
        return true;
    }
```

--
**�ο�����**
* [Android��������onTouchEvent�д�������ʱ��ĳ����¼�](http://blog.csdn.net/eoeandroida/article/details/8308877)