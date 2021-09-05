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

- __Query Context__
  - __Query Context__ 에서 사용되는 query 절은 "해당 도큐먼트가 query 절과 얼마나 잘 일치하는가?" 라는 질문에 응답하는데 도큐먼트가 얼마나 잘 일치하는지를 _score로 표현함
- __Filter Context__
  - __Filter Context__에서 가용되는 query 절은 "해당 도큐먼트가 query 절과 일치합니까?" 라는 질문에 응답하는데 그 대답은 true 또는 false이며 점수는 계산하지 않음

###  1. size, from

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



### 2. sort

- __sort__ 
  - 쿼리로 특정 필드마다 하나 이상의 정렬을 추가 할 수 있음
  - __sort__ 쿼리를 사용하지 않을 경우, 기본정렬은 _score 내림차순(desc)이며, 다른 항목으로 정렬할 경우 오름차순(asc)으로 기본 설정됨



```java
{
  "sort":[
    {"age":"desc"},
    {"balance": "desc"},
    "_score"
  ],
  "query":{
    "match_all":0
  }
}
```



### 3. source filtering

- ___source__ 필드를 통해 검색된 데이터에서 특정 필드들만 반환하도록 할수 있음
- SQL 에서 SELECT 쿼리를 날릴 떄 특정 컬럼들을 명시하는 것과 유사함



```java
{
  "_source":false,
  "query":{
    "match_all":{}
  }
}
```

검색된 도큐먼트들에 대해 모든 필드들을 응답받지 않는 예제



```java
{
  "_source"["firstname","lastname"],
  "query":{
    "match_all":{}
  }
}
```

검색된 도큐먼트들에 대해 firstname, lastname 필드만 응답받는 예제

그밖에 `*`를 사용하여 필드명을 명시할 수 있고 `includes/excludes`를 사용하여 필드를 포함 제외할 수 있음



### 4. aggregations

- __aggregations__ 는 집계를 의미하며 aggs 필드를 통해 도큐먼트 개수를 통계낼 수 있음
- SQL에서 GROUP BY 와 유사함



```java
{
  "query":{
    "item":{
      "address":"street"
    }
  },
  "aggs":{
    "avg.balance_test":{
      "avg":{
        "field":balance
      }
    }
  }
}
```

address에 street 문자열이 포함된 도큐먼트들의 balance 필드 값들을 평균내는 예제

