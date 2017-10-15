# Django

create:
	django-admin startproject guest #创建guest项目
	py -3 manage.py startapp sign #创建sign项目

run:
	py -3 manage.py runserver（默认8000端口）
	或 py -3 manage.py runserver 127.0.0.1:8001