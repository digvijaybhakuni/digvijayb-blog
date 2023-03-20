---
layout: post
title: How Data Streams work in elasticsearch?
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
Elasticsearch Data Streams is a feature introduced in Elasticsearch 7.11 that provides a simpler and more efficient way to handle time-series data.

Data Streams are a logical grouping of indices that are created based on a timestamp field, allowing data to be automatically and transparently moved to new indices as time progresses. This simplifies index management and makes it easier to manage large amounts of time-series data.

<!--more-->

In a Data Stream, the current active index is called the "write index", and all other indices in the stream are called "rollover indices". When a new document is added to the Data Stream, Elasticsearch automatically routes it to the write index. Once the write index reaches a certain size or age threshold, Elasticsearch automatically rolls over to a new index in the stream and begins writing to the new index.

This process is completely transparent to the user and requires no manual intervention. Data Streams also support automatic deletion of older indices in the stream, which helps to manage storage space and maintain optimal performance.

Data Streams are especially useful for managing large volumes of time-series data, such as log files or sensor data. They provide a streamlined way to manage and query time-series data, without the need for complex index management and maintenance.

To use Data Streams in Elasticsearch, you need to create a Data Stream by defining the index pattern for the stream, which includes the timestamp field and a name for the stream. Once the Data Stream is created, you can use it like any other index in Elasticsearch, but with the added benefits of automatic rollover and deletion of older data.

### The basic steps to set up a Data Stream in Elasticsearch

1. Define the index pattern: The first step is to define the index pattern for the Data Stream, which includes the timestamp field and a name for the stream. For example, to create a Data Stream for log files with a timestamp field called "timestamp", you could define the index pattern as:

    ```bash
    PUT _index_template/logs
    {
        "index_patterns": ["logs-*"],
        "template": {
            "settings": {
            "number_of_shards": 1,
            "number_of_replicas": 1
            },
            "mappings": {
            "_source": {
                "enabled": true
            },
            "properties": {
                "timestamp": {
                "type": "date"
                }
            }
            },
            "data_stream": {}
        },
        "priority": 200
    }
    ```
    In this example, the Data Stream is defined using the "data_stream": {} property within the index template.

1. Create the Data Stream: Once the index pattern is defined, you can create the Data Stream by sending a PUT request to Elasticsearch with the stream name and the index template name. For example:

    ```bash
    PUT /_data_stream/logs
    {
        "template": {
            "name": "logs"
        }
    }
    ```
    This will create a Data Stream called "logs" using the index template defined in step 1.

1. Write data to the Data Stream: Now that the Data Stream is created, you can write data to it using the write index. For example, to write a log message to the Data Stream:

    ```bash
    POST /logs/_doc
    {
        "timestamp": "2022-03-20T12:00:00Z",
        "message": "This is a log message"
    }
    ```
    Elasticsearch will automatically route the log message to the write index for the Data Stream based on the timestamp field.

That's it! You now have a Data Stream set up in Elasticsearch and can write data to it using the write index. As time progresses and the write index reaches the rollover threshold, Elasticsearch will automatically create a new index in the stream and begin writing to it, without any manual intervention required.





