ElasticSearch

# 1. 基础概念

- 索引 类型 文档

# 2. 查询条件

## 2.1  子查询

- 模糊查询（会对keyword进行分词后再进行模糊查询，返回结果包含_score）

```json
{
    "query":{
        "match":{
            "author":"ElasticSearch入门"
        }
    }
}
```

- 模糊查询-习语匹配

```json
{
    "query":{
        "match_phrase":{
            "author":"ElasticSearch入门"
        }
    }
}
```

- 多字段查询

```json
{
    "query":{
        "multi_match":{
            "query":"zxl",
            "fields":["title","author"]
        }
    }
}
```

- 语法查询(查询fields中包含abc或123的文档)

```json
{
    "query":{
        "match_string":{
            "query":"abc OR 123",
            "fields":["title","author"]
        }
    }
}
```

- 字段查询

```json
{
    "query":{
        "term":{
            "auth":"ZXL"
        }
    }
}
```

- 范围查询

```json
{
    "query":{
        "range":{
            "publish_date":{
                "gte":"2017-01-01",
                "lte":"now"
            }
        }
    }
}
```

- filter查询

```json
{
    "query":{
        "bool":{
            "filter":{
                "term":{
                    "word_count":1000
                }
            }
        }
    }
}
```

## 2.2  复合查询

- 固定分数查询(boost指定查询出结果的_score值)

```json
{
    "query":{
        "constant_score":{
            "filter":{
                "match":{
                    "author":"zxl"
                }
            },
            boost:2
        }
    }
}
```

- 布尔查询
  - must： 子条件是与
  - should：子条件是或
  - must_not

```json
{
    "query":{
        "bool":{
            "must":[
             	{
                    "author":"zxl"
                },
                {
                    "word_count":1000
                }
            ]
        }
    }
}
```

