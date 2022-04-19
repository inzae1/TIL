

# Django 소개

### **Django 란?** 

- 보안이 우수하고 유지보수가 편리한 웹사이트를 신속하게 개발하는 **Python Web Framework** 이다.

### **Django 설치하기**

```bash
python3 -m pip insatll Django
```
- 위 명령어를 실행하면 Django 를 설치할 수 있다.

```bash
python3 -m django --version
```
- 위 명령어를 실행하면 Django 의 설치유무와 설치된 버전을 알 수 있다.
- 설치가 제대로 되지 않았다면, `No module named django` 와 같은 에러가 발생합니다.


### **Django 프로젝트 만들기**

```bash
django-admin startproject project-name
```
- 위 명령어를 실행하면 `project-name` 이라는 디렉토리를 생성한다.

```bash
# 프로젝트 구조
project-name/
    manage.py
    project-name/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
```

- **manage.py** : Django 프로젝트와 다양한 방법으로 상호작용하는 커맨드라인의 유틸리티
- **project-name/\__init\__.py** : Python 으로 하여금 이 디렉토리를 패키지처럼 다루라고 알려주는 용도의 단순한 빈 파일
- **project-name/settings.py** : 현재 Django 프로젝트의 환경 및 구성을 저장
- **project-name/urls.py** : 현재 Django project 의 URL 선언을 저장, Django 로 작성된 사이트의 **목차**
- **project-name/asgi.py** : 현재 프로젝트를 서비스하기 위한 ASGI 호환 웹 서버의 진입점
- **project-name/wsgi.py** : 현재 프로젝트를 서비스하기 위한 WSGI 호환 웹 서버의 진입점

### **Django 프로젝트 실행하기**
```bash
./manage.py runserver
```
- 위 명령어를 실행하면 서버가 실행되면서 터미널에 아래와 같이 나온다.

```bash
Performing system checks...

System check identified no issues (0 silenced).

You have unapplied migrations; your app may not work properly until they are applied.
Run 'python manage.py migrate' to apply them.

1월 19, 2022 - 20:50:53
Django version 4.0, using settings 'mysite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```