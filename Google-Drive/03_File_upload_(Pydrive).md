

# Pydrive를 통한 File Upload



## 1. Pydrive 설치 및 가져오기

### 1. Pydrive 모듈을 설치

- 터미널에 다음과 같이 작성

```bash
python -m pip intall pydrive
```



### 2. 라이브러리 가져오기

- Google API 콘솔에서 __client_secrets.json__ 다운로드 하면 __OAuth2.0__ 이 두줄로 완료됨
- __setting.yaml__ 에서 __OAuth2.0__ 의 동작을 사용자 정의할 수 있음

```python
from pydrive.auth import GoogleAuth
from pydrive.drive import GoogleDrive
gauth = GoogleAuth()           
drive = GoogleDrive(gauth)  
```



### 3. Google Drive 에 파일 업로드

- `'id'`에는 구글드라이브 url의  https://drive.google.com/drive/u/0/folders/ <id> 값을 넣어준다

```python
upload_file_list = ['1.jpg', '2.jpg']
for upload_file in upload_file_list:
	gfile = drive.CreateFile({'parents': [{'id': '1pzschX3uMbxU0lB5WZ6IlEEeAUE8MZ-t'}]})
	# Read file and set it as the content of this instance.
	gfile.SetContentFile(upload_file)
	gfile.Upload() # Upload the file.
```

- 출력결과

![google-drive1](/Users/inzae/Documents/TIL-inzae/img/googledrive1.jpeg)

