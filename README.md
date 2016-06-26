JqueryTokyo.ElasticSearch
=========================

A Symfony project created on June 25, 2016, 11:43 pm.

DoctrineにSQLでデータ投入
```
php app/console doctrine:query:sql "INSERT INTO post(title, body, create_at, update_at) values('こんにちは', '本日は晴天なり', '2016-06-26 22:30:45', '2016-06-26 22:30:45'), ('テスト', 'テストです','2016-06-26 22:31:45', '2016-06-26 22:31:45');"
```

ElasticSearchに反映
```
php app/console fos:elastica:populate
 100/100 [============================] 100%
Populating symfony/postRefreshing symfony
Refreshing symfony
```

検索
```
php app/console fos:elastica:search post "テスト"
Found 1 results
[0.19] 2
```

直接
```
curl http://localhost:9200/symfony/_search\?pretty
```

戻り
```json
{
  "took" : 2,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "failed" : 0
  },
  "hits" : {
    "total" : 2,
    "max_score" : 1.0,
    "hits" : [ {
      "_index" : "symfony",
      "_type" : "post",
      "_id" : "1",
      "_score" : 1.0,
      "_source":{"id":1,"title":"こんにちは","body":"本日は晴天なり"}
    }, {
      "_index" : "symfony",
      "_type" : "post",
      "_id" : "2",
      "_score" : 1.0,
      "_source":{"id":2,"title":"テスト","body":"テストです"}
    } ]
  }
}
```

CRUDジェネレート
```
app/console doctrine:generate:crud AppBundle:Post
```
