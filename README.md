# Processor - teraslice_kafka_sender

To install from the root of your teraslice instance.

```
npm install terascope/teraslice_kafka_sender
```

# Description

Teraslice processor to send data to a Kafka topic.

# Expected Inputs

Array of JSON format records.

# Output

The input Array is returned as Output.

# Parameters

| Name | Description | Default | Required |
| ---- | ----------- | ------- | -------- |
| topic | Name of the Kafka topic to send data to | | Y |
| id_field | Field in the incoming record that contains keys | | N |
| timestamp_field | Field in the incoming record that contains a timestamp to set on the record | | N |
| timestamp_now | Set to true to have a timestamp generated as records are added to the topic | | N |
| connection | The kafka producer connection to use | | N |
| compression | Type of compression to use on the data. Options: gzip, snappy, lz4 and none | gzip | N |

# Job configuration example

This job generates some data and stores it to a Kafka topic named `testing-topic`. The field `created` in the incoming record contains a time that will be used to set the timestamp on the Kafka record and the field 'url' in the incoming record will be used as the key.

```
{
  "name": "Data Generator",
  "lifecycle": "persistent",
  "workers": 1,
  "operations": [
    {
      "_op": "elasticsearch_data_generator",
      "size": 500
    },
    {
      "_op": "teraslice_kafka_sender",
      "topic": "testing-topic",
      "timestamp_field": "created",
      "id_field": "url"
    }
  ]
}
```
