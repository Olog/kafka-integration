# Phoebus Olog Kafka Integration

This is an optional module for the Phoebus Olog electronic logbook service, see https://github.com/Olog/phoebus-olog. Its purpose is to broadcast a message whenever
a new log entry is created, using a Kafka message broker instance. Clients subscribing to the message topic - named "olog-notify" - will then be able to take 
appropriate action when new log entries are created.

## Prerequisites

In order for this module to act as a Kafka producer, a Kafka message broker must be available on the endpoint address defined in the runtime property 
"kafka.bootstrap.servers", e.g. localhost:9092.

## Message structure

The Kafka message payload that subscribers will receive is a JSON-formatted object like so:

```json
{
  "url":"http://localhost:8080/Olog/12345",
  "logbooks":["logbook1", "logbook2"],
  "title":"Log Entry Title",
  "author":"John Doe",
  "body":"Log entry body"
}
```

The url field is useful only if a Phoebus Olog web client has been deployed, see https://github.com/Olog/phoebus-olog-web-client. A subscriber client can use this 
url to present a direct link to the created log entry. 

The actual address and port of the Phoebus Olog web client is configured in the runtime property "olog.web.rootURL".

