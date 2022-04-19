

# Django 환경설정

## **Django setting.py 설정**

### **기본 디렉토리 경로**
```python
BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
```
- 기본 디렉토리 경로는 `BASE_DIR` 로 나타낸다.
- `BASE_DIR` 은 임의적으로 디렉토리 경로를 수정한 경우가 아니라면 수정하지 않는다.

<br>

### **비밀 키**
```python
SECRET_KEY = '비밀 키'
```
- `SECRET_KEY` 는 무작위의 50글자로 구성되어 있으며, 쿠키데이터 해시, 암호화 서명, 일회성 비밀 URL 생성 등에 사용된다.
- `SECRET_KEY` 는 노출되어서는 안되며, 노출되었을 때는 보안기능이 상실되므로 새로운 `SECRET_KEY` 를 사용해야 한다.
- `SECRET_KEY` 의 값은 분리해서 사용하며, 크게 환경 변수에 등록하거나 비밀 파일로 저장해 사용한다.

<br>

### **디버그**
```python
DEBUG = True
```
- `True` 일 때는 디버그 모드로 들어갈 수 있다.

<br>

### **허용 가능한 호스트**
```python
ALLOWED_HOSTS = []
```
- 허용 가능한 호스트는 운영 서버 등에 배포하여, 서비스할 때 호스트로 사용 가능한 호스트 또는 도메인 목록이다.
- 해당 기능은 CSRF(Cross-site request forgery) 와 HTTP 웹 서버 헤더 공격을 막기 위한 조치이다.
- `DEBUG = True` 일 때 동작하며, 기본적으로 `localhost`, `127.0.0.1` 는 등록해 사용한다.

<br>

```python
ALLOWED_HOSTS = ['localhost', '127.0.0.1', '168.92.0.381']
```
- 모든 호스트를 허용한다면 `ALLOWED_HOSTS = ['*']` 으로 설정한다.

<br>

### **설치된 애플리케이션**
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'rest_framework',
    'corsheaders',
    '앞으로 추가할 애플리케이션',
]
```
- 현재 Django project 에 설치된 애플리케이션의 목록을 의미한다.
- 애플리케이션을 등록하지 않는다면 서비스에서 사용할 수 없다.

<br>

### **CORS 허용**
```python
CORS_ORIGIN_ALLOW_ALL = False
CORS_ALLOW_CREDENTIALS = False
 
CORS_ALLOW_HEADERS = [
    'accept',
    'accept-encoding',
    'authorization',
    'content-type',
    'dnt',
    'origin',
    'user-agent',
    'x-csrftoken',
    'x-requested-with',
]
 
CORS_ALLOW_METHODS = (
    'DELETE',
    'GET',
    'OPTIONS',
    'PATCH',
    'POST',
    'PUT',
    '허용할 메서드',
)
     
CORS_ORIGIN_WHITELIST = (
    '허용할 URL',
)
```
- CORS 를 설정 했다면 위와 같은 내용을 추가한다.
- `CORS_ORIGIN_ALLOW_ALL` 은 모든 사이트들의 HTTP 요청을 가능하게한다. 개발 중에는 `True` 로 사용한다.
- 서비스 중인 서버에서는 `False` 로 사용하고, `CORS_ORIGIN_WHITELIST` 를 설정한다.
- `CORS_ALLOW_CREDENTIALS` 은 쿠키가 사이트 간 HTTP 요청에 포함 허용 여부를 설정한다.
- `CORS_ALLOW_HEADERS` 는 Access-Control-Allow-Headers 를 포함하는 예비 요청(preflight request) 응답에 사용되는 헤더를 설정한다.
- `CORS_ALLOW_METHODS` 는 사용 가능한 HTTP 메서드를 설정한다.
- `CORS_ORIGIN_WHITELIST` 는 사이트 간 요청을 허용하는 호스트 목록을 의미한다.

<br>

### **미들웨어**
```python
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```
- 미들웨어(middleware)란 운영 체제와 응용 소프트웨어 중간에서 조정과 중개의 역할을 수행하는 소프트웨어이다.
- 데이터, 애플리케이션 서비스, 인증, API 를 관리한다.
- Django 의 미들웨어는 Django 에서 발생하는 요청 및 응답 처리에 연결되는 프레임워크이다.

```python
MIDDLEWARE = [
    'corsheaders.middleware.CorsMiddleware',
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```
- Django 에서 CORS 를 허용하기 위해서는 목록의 가장 최상단에 CORS 미들웨어를 등록해야 한다.
- 추가적으로 등록되는 미들웨어는 하단에 등록해도 무방하다.

<br>

### **루트 URL**

```python
ROOT_URLCONF = 'project-name.urls'
```
- 루트 URL 설정에 대한 Python 경로를 나타내는 문자열이다.
- 루트 URL 경로 설정으로 Django project 의 URL 설정값을 가져와 등록한다.

<br>

### **템플릿**

```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```
- Django 는 웹사이트에서 활용할 수 있으므로 html 코드 등과 연동하여 사용할 수 있다.
- `BACKEND` 는 사용할 템플릿 백엔드를 설정한다. 아래와 같이 템플릿을 변경 해 사용할 수 있다.
```python
‘BACKEND’: ‘django.template.backends.django.DjangoTemplates’
or
‘BACKEND’: ‘django.template.backends.jinja2.Jinja2’
```
- `DIRS` 는 Django가 템플릿 소스 파일을 찾아야 하는 디렉터리 경로이다.
- `APP_DIRS` 은 Django 가 설치된 애플리케이션에서 템플릿 소스 파일을 찾는 여부이다.
- `OPTION` 는 템플릿 백엔드에 전달할 추가 매개 변수이다. 사용 가능한 매개 변수는 템플릿 백엔드에 따라 달라진다.

<br>

### **WSGI 배포**
```python
WSGI_APPLICATION = 'daehee.wsgi.application'
```
- 현재 프로젝트를 서비스하기 위해 WSGI(Web Server Gateway Interface) 의 경로를 의미한다.
- 환경변수가 설정되지 않으면 프로젝트를 생성할 때 제공되는 wsgi.py 의 설정값을 사용한다.

<br>

### **데이터베이스 설정**
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```
- 기본값으로 SQLite 가 설정되어 있으며, 특정 데이터베이스를 연동할 때 `DATABASES` 설정값을 변경한다.
- `ENGINE` 은 데이터베이스의 엔진을 의미하며, MySQL 이나 PostgreSQL 등을 연동할 수 있다.


#### 로컬 데이터베이스 연동
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'HOST': db_host,
        'PORT': db_port,
        'NAME': db_name,
        'USER': db_user,
        'PASSWORD': db_password,
    }
}
```

#### 클라우드 데이터베이스 연동
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'HOST': aws.076923.ap-northeast-2.rds.amazonaws.com,
        'PORT': 5432,
        'NAME': db_name,
        'USER': db_user,
        'PASSWORD': db_password,
    }
}
```

<br>

### **비밀번호 유효성 검사**
```python
AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
]
```



