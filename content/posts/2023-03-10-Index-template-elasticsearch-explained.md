---
layout: post
title: Index Template in Elasticsearch, Explained?
author: digvijayb
tags:
  - elasticsearch
  - elasticstack
  - index
  - web
  - search
date: 2023-03-20T09:59:42.780Z
description: The index template in Elasticsearch is used to define a set of rules that are applied to new indices created in Elasticsearch. These rules can be used to automatically set default values for fields, define mappings for new fields, and apply settings to new indices.
thumbnail: /images/uploads/featured.png
---
The index template in Elasticsearch is used to define a set of rules that are applied to new indices created in Elasticsearch. These rules can be used to automatically set default values for fields, define mappings for new fields, and apply settings to new indices.

The index template is a JSON file that contains a set of rules that are applied to new indices. When a new index is created in Elasticsearch, the index template is evaluated and any rules that match the new index are applied.

<!--more-->

The index template can contain a variety of settings, including:

- Index settings: These settings define the behavior of the index, such as the number of shards and replicas.

- Mapping definitions: These definitions define the structure of the data in the index, including the field types, analyzers, and other properties.

- Field templates: These templates define default values for fields in the index, such as the default value for a timestamp field.

- Dynamic mapping rules: These rules define how new fields are mapped when they are added to the index.

Overall, the index template is a powerful tool for automating the creation and management of Elasticsearch indices, allowing you to quickly and easily define the structure and behavior of new indices as they are created.

## Let take a look as Example 

Elasticsearch index template that includes an index pattern, index settings, mapping, field template, and dynamic mapping. 

```json
{
  "index_patterns": ["my-index-*"],
  "settings": {
    "number_of_shards": 3,
    "number_of_replicas": 2
  },
  "mappings": {
    "_doc": {
      "properties": {
        "message": {
          "type": "text",
          "analyzer": "english"
        },
        "timestamp": {
          "type": "date"
        }
      }
    }
  },
  "field_templates": [
    {
      "field": "user_id",
      "mapping": {
        "type": "keyword"
      }
    }
  ],
  "dynamic_templates": [
    {
      "strings": {
        "match_mapping_type": "string",
        "mapping": {
          "type": "text",
          "analyzer": "english"
        }
      }
    },
    {
      "dates": {
        "match_mapping_type": "date",
        "mapping": {
          "type": "date"
        }
      }
    }
  ]
}

```

In this example:

- The `index_patterns` field specifies the index pattern for which this template will be applied.
- The `settings` field sets the number of shards and replicas for new indices that match the pattern.
- The `mappings` field defines the structure of the data in the index, including a `message` field of type `text` with an English analyzer, and a timestamp field of type `date`.
- The `field_templates` field defines a template for a `user_id` field that will be mapped as a `keyword` type.
- The `dynamic_templates` field defines two dynamic mapping templates. One for `string` fields that will be mapped as a `text` type with an English analyzer, and another for `date` fields that will be mapped as a `date` type.

> This index template will be applied to any new indices that match the `my-index-*` pattern and will automatically set the index settings, mappings, and dynamic mapping templates.