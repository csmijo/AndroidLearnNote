# Appium python API ѧϰ

`Appium` `python API`

--

## 0. Appium server arguments

* [Appium server arguments](https://appium.io/slate/en/master/?ruby#appium-server-capabilities)
* [ѧϰ DesiredCapabilities](https://anikikun.gitbooks.io/appium-girls-tutorial/content/desired_caps.html)

## 1. find element

### 1.1 driver �ķ���

����**ע�⣺** �⼸������ֻ��ͨ�� `self.driver` ����
����

1. `find_element_by_android_uiautomator(self,uia_string)`
2. `find_elements_by_android_uiautomator(self,uia_string)`
3. `find_element_by_accessibility_id(self,id)`
4. `find_elements_by_accessibility_id(self,id)`

### 1.2 element �ķ��� 

����**ע�⣺** �⼸������ͨ�� `driver`��`element`�����Ե��á�`element` ����ʱ����������λ��Ԫ�ص���Ԫ��

1.  `find_element_by_id(self,id_)`
2. `find_elements_by_id(self,id_)`
3. ~~`find_element_by_name(self,name)`~~   **Appium 1.5�汾֮�����**
4. ~~`find_elements_by_name(self,name)`~~  **Appium 1.5�汾֮�����**
5. `find_element_by_link_text(self,link_text)`
6. `find_elements_by_link_text(self,link_text)`
* `find_element_by_partial_link_text(self, link_text)`
* `find_elements_by_partial_link_text(self, link_text)`
* `find_element_by_tag_name(self, name)`
* `find_elements_by_tag_name(self, name)`
* `find_element_by_xpath(self, xpath)`   **ͨ��Xpath��λԪ�أ���ϸ�����ɲ���`http://www.w3school.com.cn/xpath/`**
* `find_elements_by_xpath(self, xpath)`
* `find_element_by_class_name(self, name)`
* `find_elements_by_class_name(self, name)`


## 2. remote/webdriver

����**ע�⣺**��`selenium` ԭ�����������÷�����`self.driver.xxxx()`

1. `page_source(self)`
* `get_screenshot_as_file(self, filename)`
* `get_window_size(self, windowHandle='current')`
* `orientation(self)`   ��ȡ����
* `orientation(self, value)`  ���÷���
* `desired_capabilities(self)`   ���� �趨�����в���

## 3. appium/webdriver

���෽���ĵ��÷�ʽ��Ϊ `self.driver.xxxx()`

### 3.1 �������

#### 3.1.1 ���/��������

1. `scroll(self, origin_el, destination_el)`
* `drag_and_drop(self, origin_el, destination_el)`
* `tap(self, positions, duration=None)`  ģ����ָ�������������ָ���������ð�סʱ�䳤�ȣ����룩
* `swipe(self, start_x, start_y, end_x, end_y, duration=None)`    ��A�㻬����B�㣬����ʱ��Ϊ����
* `flick(self, start_x, start_y, end_x, end_y)`  ��סA�����ٻ�����B��
* `pinch(self, element=None, percent=200, steps=50)`   ��Ԫ����ִ��ģ��˫ָ����С������
* `zoom(self, element=None, percent=200, steps=50)`   ��Ԫ����ִ�зŴ������˫ָ�Ŵ�
* `open_notifications(self)`   ��ϵͳ֪ͨ����**��֧��API 18 ���ϵİ�׿ϵͳ**��
* `shake(self)`  ҡһҡ�ֻ�

#### 3.1.2 ���� 

1. `press_keycode(self, keycode, metastate=None)`   ���Ͱ����루��׿���У����������������ַ���ҵ�`http://developer.android.com/reference/android/view/KeyEvent.html`
* `long_press_keycode(self, keycode, metastate=None)`

#### 3.1.3 ���뷨


1. `hide_keyboard(self, key_name=None, key=None, strategy=None)`   ���ؼ���,iOSʹ��key_name���أ���׿��ʹ�ò���

* `available_ime_engines(self)`   **Android only**. ���ذ�׿�豸���õ����뷨
* `is_ime_active(self)`  **Android only**. ����豸�Ƿ������뷨������������/��
* `activate_ime_engine(self, engine)`   **Android only**.���׿�豸�е�ָ�����뷨���豸�������뷨���Դӡ�available_ime_engines����ȡ
* `deactivate_ime_engine(self)`    **Android only**.�رհ�׿�豸��ǰ�����뷨
* `active_ime_engine(self)`  **Android only**. ���ص�ǰ���뷨�İ���

### 3.2 app����
1.  `reset(self)`  ����Ӧ��(�൱��ж����װӦ��)
* `background_app(self, seconds)`  ��̨����app������
* `is_app_installed(self, bundle_id)`  ���app�Ƿ��а�װ
* `install_app(self, app_path)`   ��װapp,app_pathΪ��װ��·��
* `remove_app(self, app_id)`
* `launch_app(self)`        ���ݷ���ؼ��� (`desired capabilities`) �����Ự (`session`) ��**��ע��**��������趨 `autoLaunch=false` �ؼ���ʱ������Ч���ⲻ����������ָ���� `app/activities` �������������ʹ�� `start_activity` �������Ч��������������������������ʹ���� `autoLaunch=false` �ؼ���ʱ�ĳ�ʼ�� (`Launch`) ���̵ġ�
 
* `close_app(self)`


### 3.3 contexts/activity

1. `contexts(self)`  ���ص�ǰ�Ự�е������ģ�ʹ�ú����ʶ��H5ҳ��Ŀؼ�
* `current_context(self)`  ���ص�ǰ�Ự�ĵ�ǰ������
* `context(self)`  ���ص�ǰ�Ự�ĵ�ǰ�����ġ�
* `current_activity(self)`   ��ȡ��ǰ��activity
* `wait_activity(self, activity, timeout, interval=1)`  **Android only**.  �ȴ�ָ����`activity` ����ֱ����ʱ��`interval` Ϊɨ����1��
��ÿ�������ȡһ�ε�ǰ�� `activity` 
* `start_activity(self, app_package, app_activity, **opts)`  **Android only**.  �ڲ��Թ����д�����������������һ��Ӧ�ó��򣬸�Ӧ�ó���������ͻ����  

### 3.4 network

 
1. `network_connection(self)`  **Android only**.  ������������  ��ֵ
* `set_network_connection(self, connectionType)`  **Android only**. 

    |Value (Alias)      | Data | Wifi | Airplane Mode|
    |:--|:--|:--|:--|
    |0 (None)           | 0    | 0    | 0|
    |1 (Airplane Mode)  | 0    | 0    | 1|
    |2 (Wifi only)      | 0    | 1    | 0|
    |4 (Data only)      | 1    | 0    | 0|
    |6 (All network on) | 1    | 1    | 0|

### 3.5 λ�÷���

 
1. `toggle_location_services(self)`  �򿪰�׿�豸�ϵ�λ�ö�λ����
* `set_location(self, latitude, longitude, altitude)`   �����豸�ľ�γ��

### 3.6 �ļ� pull/push
 
1. `pull_file(self, path)`  ���豸��ָ��·����ȡ�ļ�
* `pull_folder(self, path)`
* `push_file(self, path, base64data)`

### 3.7 ����

1. `end_test_coverage(self, intent, path)`  **Android only**.���Ը�������أ�Ŀǰ�����ṩ����֧�֡� `https://github.com/appium/appium/blob/master/docs/en/android_coverage.md`
* `set_value(self, element, value)`   ����ĳԪ�ص�ֵ
* `create_web_element(self, element_id)`
* `app_strings(self, language=None, string_file=None)`  ��������app��strings.xml

## 4. remote/webelement

����ҳ��Ԫ�صķ��������÷�����`element.xxxx()`
 
1. `tag_name(self)`   ����Ԫ�ص�tagName����
* `text(self)`  ����Ԫ�ص��ı�ֵ
* `click(self)` 
* `submit(self)`   �ύ��
* `clear(self)`  ������������
* `get_attribute(self, name)`
* `is_selected(self)`
* `is_enabled(self)`
* `send_keys(self, *value)`  ��Ԫ����ģ�����루����appium�Դ������뷨��������appium���뷨�󣬿���������Ӣ�ģ�
* `size(self)`  ��ȡԪ�صĴ�С���ߺͿ�
* `location_once_scrolled_into_view(self)`  **���ȶ������Ƽ�ʹ��**
* `location(self)`   ��ȡԪ�����Ͻǵ�����
* `rect(self)`  Ԫ�صĴ�С��λ�õ��ֵ�


--
[�ο�����]

* [Appium python API �ܽ�](https://testerhome.com/topics/3711)
* [Appium Python API ���İ� By-HZJ](https://testerhome.com/topics/3711)
* [Appium �ͻ��˿�](http://appium.readthedocs.org/en/stable/cn/writing-running-appium/appium-bindings.cn/)