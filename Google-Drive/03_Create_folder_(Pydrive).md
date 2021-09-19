

# Pydrive를 통한 구글드라이브에 폴더만들기

### 1. CreateFile 를 통해 폴더만들기

- 다음은 폴더를 만드는 함수이다.

```python
def create_folder(folder_name, parents_folder_id):
    folder_metadata = {
        'title': folder_name,
        'mimeType': 'application/vnd.google-apps.folder',
        'parents': [{'id': parents_folder_id}]
    }
    folder_upload = drive.CreateFile(folder_metadata)
    folder_upload.Upload()
    print(folder_name, 'FOLDER CREATE COMPLETE')
```

- `folder_name`에 생성할 폴더의 이름을 입력한다.

- `parents_folder_id`에 생성할 폴더의 부모폴더 id 를 입력한다.

  

