# tencentyun/image-python-sdk-v2.0
��Ѷ�� [������ͼ��Cloud Image v2.0��](https://www.qcloud.com/product/ci) SDK for PHP

## ��װ

### ʹ��pip
Python 2:

pip install tencentyun

Python 3:

pip3 install tencentyun

### ����Դ��
��github����Դ��װ�뵽���ĳ����У�������qcloud_image��
������ο�sample.py

### 1. ����Ѷ������ҵ�����Ȩ
��Ȩ������
		
	APP_ID 
	SECRET_ID
	SECRET_KEY
	BUCKET

### 2. ������Ӧ������Ķ���
���Ҫʹ��ͼƬ����Ҫ����ͼƬ���������

	from qcloud_image import Client
	from qcloud_image import CIUrl, CIFile, CIBuffer, CIUrls, CIFiles, CIBuffers

	appid = 'APP_ID'
	secret_id = 'SECRET_ID'
	secret_key = 'SECRET_KEY'
	bucket = 'BUCKET'

	client = Client(appid, secret_id, secret_key, bucket)
	client.use_http()
	client.set_timeout(30)

### 3. ���ö�Ӧ�ķ���
�ڴ��������󣬸���ʵ�����󣬵��ö�Ӧ�Ĳ��������Ϳ����ˡ�sdk�ṩ�ķ���������ͼƬʶ������ʶ����������ȡ�

#### 3.1 ͼƬʶ��
ͼƬʶ�������ͼƬ���ơ�ͼƬ��ǩ��OCR-���֤ʶ��OCR-��Ƭʶ��

##### ͼƬ����

```python
	#��������ͼƬUrl
	print (client.porn_detect(CIUrls(['http://jiangsu.china.com.cn/uploadfile/2015/1102/1446443026382534.jpg','http://n.sinaimg.cn/fashion/transform/20160704/flgG-fxtspsa6612705.jpg'])))
	#��������ͼƬFile
	print (client.porn_detect(CIFiles(['./test.jpg',])))
```

##### ͼƬ��ǩ

```python
	#����ͼƬurl
	print (client.tag_detect(CIUrl('http://img3.a0bi.com/upload/ttq/20160814/1471155260063.png')))
	#����ͼƬfile
	print (client.tag_detect(CIFile('./hot2.jpg')))
```

##### OCR-���֤ʶ��

```python
	#��������ͼƬUrl,ʶ�����֤����
	print (client.idcard_detect(CIUrls(['http://imgs.focus.cn/upload/sz/5876/a_58758051.jpg']), 0))
	#��������ͼƬfile,ʶ�����֤����
	print (client.idcard_detect(CIFiles(['./id4_zheng.jpg','./id1_zheng.jpg']), 0))
	#��������ͼƬUrl,ʶ�����֤����
	print (client.idcard_detect(CIUrls(['http://www.csx.gov.cn/cwfw/bszn/201403/W020121030349825312574.jpg', 'http://www.4009951551.com/upload/image/20151026/1445831136187479.png']), 1))
	#��������ͼƬfile,ʶ�����֤����
	print (client.idcard_detect(CIFiles(['./id5_fan.jpg']), 1))
```

##### OCR-��Ƭʶ��	
```python
	#��������ͼƬUrl
	print (client.namecard_detect(CIUrls(['http://pic1.nipic.com/2008-12-03/2008123181119306_2.jpg', 'http://pic.58pic.com/58pic/12/49/04/80k58PICzYP.jpg'])))
	#��������ͼƬfile
	print (client.namecard_detect(CIFiles(['./name1.jpg'])))
```

#### 3.2 ����ʶ��
����ʶ�������������⡢��ٶ�λ��������Ϣ����������֤�������Աȼ�����������

#### �������

```python
	#����ͼƬUrl, mode:1Ϊ����������� , 0Ϊ�����������
	print (client.face_detect(CIUrl('http://img3.a0bi.com/upload/ttq/20160814/1471155260063.png')))
	#����ͼƬfile,mode:1Ϊ����������� , 0Ϊ�����������
	print (client.face_detect(CIFile('./hot2.jpg')))
```

##### ��ٶ�λ

```python
	#����ͼƬUrl,mode:1Ϊ����������� , 0Ϊ�����������
	print (client.face_shape(CIUrl('http://img3.a0bi.com/upload/ttq/20160814/1471155260063.png'),1))
	#����ͼƬfile,mode:1Ϊ����������� , 0Ϊ�����������
	print (client.face_shape(CIFile('./hot2.jpg'),1))
```

##### ������Ϣ����
```python
    //���崴��,����һ��Person������Person���õ�group_idsָ�����鵱�У������ڵ�group_id���Զ�������
	#����һ��Person, ʹ��ͼƬurl
	print (client.face_newperson('person111', ['group2',], CIUrl('http://img3.a0bi.com/upload/ttq/20160814/1471155260063.png'), 'xiaoxin'))
	#����һ��Person, ʹ��ͼƬfile
	print (client.face_newperson('person211', ['group2',], CIFile('./hot2.jpg')))

	//��������,��һ��Face���뵽һ��Person�С�ע�⣬һ��Faceֻ�ܱ����뵽һ��Person�С� 
	#���������߶��Face��url���뵽һ��Person��
	print (client.face_addface('person111', CIUrls(['http://jiangsu.china.com.cn/uploadfile/2015/1102/1446443026382534.jpg','http://n.sinaimg.cn/fashion/transform/20160704/flgG-fxtspsa6612705.jpg'])))
	#���������߶��Face��file���뵽һ��Person��
	print (client.face_addface('person211', CIFiles(['./test.jpg',])))

	#ɾ������,ɾ��һ��person�µ�face
	print (client.face_delface('person111', ['person111',]))

	#������Ϣ
	print (client.face_setinfo('person111', 'hello'))

	#��ȡ��Ϣ
	print (client.face_getinfo('person111'))

	#��ȡ���б�
	print (client.face_getgroupids())

	#��ȡ���б�
	print (client.face_getpersonids('group2'))

	#��ȡ�����б�
	print (client.face_getfaceids('person211'))

	#��ȡ������Ϣ
	print (client.face_getfaceinfo('1820307972625034938'))

	#ɾ������
	print (client.face_delperson('person11'))
```

##### ������֤
����һ��Face��һ��Person�������Ƿ���ͬһ���˵��ж��Լ����Ŷ�

```python
	#������֤,����ͼƬUrl
	print (client.face_verify('person111', CIUrl('http://img3.a0bi.com/upload/ttq/20160814/1471155260063.png')))
	#������֤,����ͼƬfile
	print (client.face_verify('person111', CIFile('./test.jpg')))
```

##### ��������
����һ����ʶ�������ͼƬ����һ��Group��ʶ��������Ƶ�Top5 Person��Ϊ����ݷ��أ����ص�Top5�а������ƶȴӴ�С���С�

```python
	#��������,�����ļ�url
	print (client.face_identify('group1', CIUrl('http://www.5djiaren.com/uploads/2016-07/22-141354_227.jpg')))
	##��������,�����ļ�file
	print (client.face_identify('group2', CIFile('./test.jpg')))
```

##### �����Ա�

```python
	#�����Ա�ͼƬ���ļ�url
	print (client.face_compare(CIFile('./zhao1.jpg'), CIFile('./zhao2.jpg')))
	#�����Ա�ͼƬ���ļ�file
	print (client.face_compare(CIUrl('http://www.miexue.com/d/file/junshiyingshi/2016-12-05/60bce03aac7a57e4fc600ecee1591e1d.jpg'), CIUrl('http://img.mp.itc.cn/upload/20161118/ee6be67ec6fb4135b5d579ab05acd715_th.jpg')))
	#һ����ͼƬ���ļ�url�� һ���ǶԱ�ͼƬ���ļ�file
	print (client.face_compare(CIFile('./zhao1.jpg'), CIUrl('http://www.miexue.com/d/file/junshiyingshi/2016-12-05/60bce03aac7a57e4fc600ecee1591e1d.jpg')))
```
	
##### ���֤ʶ��Ա�

```python
	#���֤url
	print (client.face_idcardcompare('420822198804266119', '��ʱ��', CIUrl('http://docs.ebdoor.com/Image/CompanyCertificate/1/16844.jpg')))
	#���֤�ļ�file
	print (client.face_idcardcompare('420822198804266119', '��ʱ��', CIFile('./id4_zheng.jpg')))
```
		
#### 3.3 ��������

```python
	#�������һ������ȡ�����֤�룩
	obj = client.face_livegetfour()
	print (obj)
	#��֤��
	validate_data = obj['data']['validate_data']
	#������ڶ��������
	print (client.face_livedetectfour(validate_data, CIFile('../dn.qlv'), False, CIFile('../wxb.jpg')))
	#������ڶ��������--�Ա�ָ�������Ϣ
	print (client.face_idcardlivedetectfour(validate_data, CIFile('../dnn.qlv'), '330782198802084329', '��ʱ��'))
```