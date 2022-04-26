

# Django Migrate

## **Django Project 등록**
```python
# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'rest_framework',
    'corsheaders',
    'first_app',
]
```
- django-project-name/settings.py 로 이동하여 `INSTALLED_APPS` 에 앱 이름을 추가한다.
- 앱이 추가될 때마다 `INSTALLED_APPS` 에 앱 이름을 등록해야 한다.
- 설치된 앱은 `app.py` 의 경로 설정을 따라간다.

## **Django migrate**

```bash
python manage.py migrate
```
- 일반적으로 `model` 클래스의 설계가 완료된 후 모델에 대응되는 테이블을 DB에서 생성한다.
- 먼저 위에 명령어를 실행하면 기본적인 구조가 적용된다.

```python
python manage.py showmigrations
```
- 위 명령어로 마이그레이션이 잘 되었는지 확인 할 수 있다.