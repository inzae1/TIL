# Elasticsearch_Query

## 1. Full Text Query

- __match_all__ : 별다른 조건 없이 해당 인덱스의 모든 도큐먼트를 검색

```java
GET customer/_search
```

```java
GET customer/_search
{
  "query":{
    "match_all":{}
  }
}
```

두 예제의 결과는 동일함



- __match__ : 풀텍스트 검색에 사용되는 일반적인 쿼리

```java
GET customer/_search
{
  "query":{
    "match":{
      "person":"INZAE"
    }
  }
}
```

```java
GET customer/_search
{
  "query":{
    "match":{
      "person":"INZAE MIKE"
    }
  }
}
```

INZAE 와 MIKE 중 어떤 단어라도 포함된 도큐먼트를 검색

디폴트값이 __OR__

__AND__ 로 바꾸려면 

`<필드명>: { "query":<검색어>, "operator": "and"}`

를 사용하여야 한다.



- __match_phrase__ : 구문을 공백을 포함해 정확히 일치하는 내용을 검색



```java
GET customer/_search
{
  "query":{
    "match_phrase":{
      "person":"Amazing INZAE",
      "slop":1
    }
  }
}
```

__"Amazing INZAE"__ 를 검색 

`slop`을 1로 했기때문에 단어 사이의 한개의 값도 포함됨

__"Amazing mike INZAE"__ 도 검색됨





## 2. Bool Query

- __must__ : 쿼리가 참인 도큐먼트 검색
- __must_not__ : 쿼리가 거짓인 도큐먼트 검색
- __should__ : 검색 결과 중 이 쿼리에 해당하는 도큐먼트의 점수를 높임
- __filter__ : 쿼리가 참인 도큐먼트를 검색하지만 스코어를 계산하지 않음 (must 보다 속도가 빠름)



```java
'''Mike를 검색하고 food에 apple이 포함된 모든문서를 검색'''
  
GET my_index/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "person": "Mike"
          }
        },
        {
          "match_phrase": {
            "food": "apple"
          }
        }
      ]
    }
  }
}
```





## 3. 정확도 (Relevancy)

- Elasticsearch 는 이 정확도(Relevancy) 를 기반으로 가장 원하는 결과를 먼저 보여줌



### 1. score

- 이 점수는 검색된 결과가 얼마나 검색조건과 일치하는지를 나타내며 __score__ 가 높은 순으로 결과를 보여줌



### 2. TF (Term Frequency)

- 도큐먼트 내에 검색된 **텀(term)**이 더 많을수록 점수가 높아지는 것을 **Term Frequency** 라고 함



### 3. IDF (Inverse Document Frequency)

- 검색한 텀을 포함하고 있는 도큐먼트 개수가 많을수록 그 텀의 자신의 점수가 감소하는 것을 __Inverse Document Frequency__ 라고 함



## 4. Query DSL

###  size, from

- __size__ : 몇개의 value가 나오는 지 설정하는 옵션

  __size__가 지정되지 않으면 기본값은 10임

- __from__ : 어떤 색인에서 시작할지 설정하는 옵션

  __from__이 지정되지 않으면 기본값은 10임

```java
GET cuustomer/_search
{
  "query":{
    "match_all":{},
    "size": 1000,
    "from": 1000
  }
}
```



## 5. FIlter

