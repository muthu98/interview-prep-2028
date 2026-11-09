# Rate Limiting

## Day 22

A rate limiter controls how many requests a client can make within a defined time window.

Benefits include:

- protecting APIs from overload and abuse
- controlling infrastructure cost
- improving fairness and stability
- reducing brute-force or spam traffic

A rejected request commonly receives **HTTP 429 Too Many Requests**.

## Distributed Rate Limiting

In a multi-server system, local counters can become inconsistent because a load balancer may route the same client to different servers.

A shared store such as Redis can keep one logical rate-limit state for all application instances.

The key can be based on:

- user ID
- API key
- IP address
- tenant
- endpoint
- combinations such as user + endpoint

## Algorithms

### Fixed Window

Simple and cheap, but it can allow a burst around a boundary.

Example: 10 requests at 12:00:59 and another 10 at 12:01:01 can both fit into separate one-minute windows.

### Sliding Window

For each incoming request:

```text
end = current request time
start = current request time - window duration
```

The limiter counts requests whose timestamps are still inside that rolling range.

There is no global reset time.

A Redis sorted set can store recent request timestamps per client key, remove expired timestamps, count the remaining entries, and add the new request atomically.

### Token Bucket

A logical token counter refills over time. Each accepted request consumes a token.

The tokens are rate-limiter state, not authentication tokens sent by the client.

Token Bucket is a useful default for APIs because it permits controlled bursts.

### Leaky Bucket

Requests enter a queue/bucket and leave at a controlled steady rate. It is useful for smoothing traffic toward downstream services.

## Rate Limit vs Concurrency Limit

Rate limit asks:

> How many requests happened in the configured time range?

Concurrency limit asks:

> How many requests are actively executing at the same time?

They solve different problems and can be used together.
