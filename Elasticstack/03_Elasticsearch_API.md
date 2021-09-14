# Elasticsearch_search_API

### 1. URI 검색

- _search 뒤에 `q` 파라미터를 이용하여 검색하는 방식을 __URI__ 이라고 함

  

```java
GET customer/_search?q=value
```

__value__ 라는 값을 검색하기 위한 로직, 가장 정확도 (relevancy) 가 높은 문서 10개가 나타남



```java
GET customer/_search?q=value AND person
```

__value__  와 __three__를 모두 포함한 도큐먼트만 리턴



```java
GET customer/_search?q=field:value
```

검색어 __value__ 을 __field__ 에서 찾고싶을때 검색 방법





### 2. 멀티네넌시 (Multitenancy)

- 날짜별로 지정된 인덱스들이 있다면 모두 `log-*/_search`명령으로 검색 가능
- 여러 인덱스를 검색할때에는 `,`로 나열하거나 `*`로 묶을 수 있음

```java
GET log-2021-*/_search
```





### 3. Data Body 검색

- 데이터 본문(Data Body) 검색은 검색쿼리를 데이터 본문으로 입력하는 방식
- 쿼리 입력은 항상 `query` 로 시작함

```java
GET costumer/_search
{
  "query": {
    "match": {
      "field": "value"
    }
  }
}
```

`match`쿼리를 지정하여`field` 필드에서 `value` 검색
