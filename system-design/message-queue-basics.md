# Message Queue Basics

## Day 23

A message queue decouples a producer from background consumers.

For a video upload flow:

```text
Client upload
  -> Upload service stores file
  -> publish VIDEO_UPLOADED
  -> Message Queue
  -> thumbnail / transcoding / analytics workers
  -> notification or progress update
```

The user should normally wait for the upload to complete, not for every downstream processing step.

Chunked upload is an upload optimization; the message queue handles asynchronous background work after the upload event.

## Why Use a Queue?

- absorb traffic spikes
- protect downstream services from overload
- process jobs according to worker capacity
- decouple producers from consumers
- scale workers independently
- retry failed jobs

If 1000 videos arrive suddenly, the queue buffers the jobs instead of sending all 1000 processing requests directly to a transcoder.

## Acknowledgement

A worker acknowledges a message only after successful processing.

If the worker crashes before ACK, the queue can make the message available for another worker.

This often gives **at-least-once delivery**, so consumers should be idempotent when possible.

## Failure Handling

Repeated failures can be retried and eventually moved to a **Dead Letter Queue (DLQ)** for inspection or recovery.

## Common Technologies

- RabbitMQ
- Kafka
- AWS SQS
- Azure Service Bus
- Google Pub/Sub
