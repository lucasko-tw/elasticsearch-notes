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
