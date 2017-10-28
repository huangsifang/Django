# Django

create:
	django-admin startproject guest #创建guest项目
	py -3 manage.py startapp sign #创建sign项目

run:
	py -3 manage.py runserver（默认8000端口）
	或 py -3 manage.py runserver 127.0.0.1:8001

创建django_session表:
	py -3 manage.py migrate

创建登录Admin后台的管理员账号:
	py -3 manage.py createsuperuser

登录admin管理后台:
	http://127.0.0.1:8000/admin/

数据库迁移：
	py -3 manage.py makemigrations sign
	py -3 manage.py migrate

manage.py提供的shell命令：
	>>> python3 manage.py shell

	>>> from sign.models import Event, Guest # 导入sign应用下的models.py中的Event表和Guest表
	>>> table.objects.all() # 获得table（Event、Gues 表）中的所有对象

	# 插入数据

	>>> from datetime import datetime
	>>> e1 = Event(id=2,name='红米Pro 发布会',limit=2000,status=True,address='北京水立方',start_time=datetime(2016,8,10,14,0,0))
	# 由于UTC，在.../settings.py 文件中设置：USE_TZ = False
	>>> e1.save()

	# 或者
	>>> Event.objects.create(id=3,name='红米MAX 发布会',limit=2000,status=True,address='北京会展中心',start_time=datetime(2016,9,22,14,0,0))
	>>> Guest.objects.create(realname='andy',phone=13611001101,email='andy@mail.com',sign=False,event_id=3)

	# 查询数据

	>>> e1 = Event.objects.get(name='红米MAX 发布会')
	>>> e2 = Event.objects.filter(name__contains='发布会') # 模糊查询，返回一个对象列表，如果记录不存在的话，它会返回[]

	# 删除数据

	>>> g2 = Guest.objects.get(phone='13611001101')
	>>> g2.delete()

	# 更新数据

	>>> g3=Guest.objects.get(phone='13611001101')
	>>> g3.realname='andy2'
	>>> g3.save()

	# 或者
	>>> Guest.objects.select_for_update().filter(phone='13611001101').update(realname='andy')