---
layout: default
title: Weighted Average
parent: Metric aggregations
grand_parent: Aggregations
nav_order: 150
redirect_from:
  - /query-dsl/aggregations/metric/weighted-average/
---

# Weighted average aggregations

The `weighted average` metric is a multi-value metric aggregations that returns the weighted average value.


A script has four stages: the initial stage, the map stage, the combine stage, and the reduce stage.

* `value`: value of 
* `weight`: weight that the value is applied for


```json
GET opensearch_dashboards_sample_data_ecommerce/_search
{
  "size": 0,
  "aggs": {
    "Weighted_average_response": {
      "weighted_avg": {
        "value": {
          "field": "taxless_total_price"
        },
        "weight": {
          "field": "total_quantity"
        }
      }
    }
  }
}
```
{% include copy-curl.html %}

#### Example response

```json
{
  "took": 2,
  "timed_out": false,
  "_shards": {
    "total": 1,
    "successful": 1,
    "skipped": 0,
    "failed": 0
  },
  "hits": {
    "total": {
      "value": 4675,
      "relation": "eq"
    },
    "max_score": null,
    "hits": []
  },
  "aggregations": {
    "Weighted_average_response": {
      "value": 81.8645153323506
    }
  }
}
```
