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

The `weighted average` metric is a multi-value metric aggregations that returns the weighted average value. Weighted average can be used when calculating grades for students, where various assignments and exams make-up the final grade of 100%. 


A weighted average has two fields, a value and a weight.

* `value`: value that the weight is applied to
  * `missing`: (optional) to apply a default value for any missing/null value fields
* `weight`: weight that the value is applied for
  * `missing`: (optional) to apply a default weight for any missing/null weight fields

Every value field is applied with the respective value in the weight field.

![Weighted average formula]({{site.url}}{{site.baseurl}}/images/aggregations/metric/weighted-average.png)

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

#### Example with optional `missing` field

```json
GET opensearch_dashboards_sample_data_ecommerce/_search
{
  "size": 0,
  "aggs": {
    "Weighted_average_response": {
      "weighted_avg": {
        "value": {
          "field": "taxless_total_price",
          "missing": 100
        },
        "weight": {
          "field": "total_quantity",
          "missing": 1
        }
      }
    }
  }
}
```
{% include copy-curl.html %}
