### Aggs with not analyzed
PUT /myIndexName
```JSON
{
  "mappings": {
    "myTypeName": {
      "properties": {
        "src_ip": {
          "type": "string",
          "fields": {
            "raw": {
              "type": "string",
              "index": "not_analyzed"
            }
          }
        },
        "dst_ip": {
          "type": "string",
          "fields": {
            "raw": {
              "type": "string",
              "index": "not_analyzed"
            }
          }
        }
      }
    }
  }
}

```
POST /myIndexName/_search
```JSON
{
  "query": {
    "bool": {
      "must": [
        {
          "range": {
            "startTime": {
              "gte": "2017-02-20T08:00:00",
              "lte": "2017-02-20T08:05:00"
            }
          }
        }
      ]
    }
  },
  "aggs": {
    "src_ip": {
      "terms": {
        "field": "src_ip.raw",
        "size": 1000
      },
      "aggs": {
        "dst_ip": {
          "terms": {
            "field": "dst_ip.raw",
            "size": 1000
          }
        }
      }
    }
  }
}
```

python code

```python
class ElasticsearchConnector ():
    client = None

    def __init__(self , host , port):
        url = "%s:%s" % (host , port)
        self.client = Elasticsearch( [url] , send_get_body_as="POST")

    def putMapping(self , esIndex , esType):

        response = self.client.indices.create(
                index=esIndex,
                body={
                            "mappings": {
                                esType : {
                                    "properties": {
                                        "src_ip": {
                                            "type": "string",
                                            "fields": {
                                                "raw": {
                                                    "type": "string",
                                                    "index": "not_analyzed"
                                                }
                                            }
                                        },
                                        "dst_ip": {
                                            "type": "string",
                                            "fields": {
                                                "raw": {
                                                    "type": "string",
                                                    "index": "not_analyzed"
                                                }
                                            }
                                        }
                                    }
                                }
                            }
                        }
        )
        print "put res=",response

```

