# 🏗️ System Design Preparation

Track system design concepts and interview revision. Detailed explanations live in topic files.

## 📊 Current Progress

- ✅ Topic units covered: **4** — load balancing, caching, rate limiting, and message queues.
- 📅 Latest study day: **Day 23**.
- Coverage is conceptual; no load balancer implementation is marked complete.

## ✅ Completed Topics

| Day | Topic | Status |
|---|---|---|
| Day 20 | [Load balancer fundamentals](load-balancer.md) | ✅ Fundamentals covered |

| Day 21 | [Caching fundamentals](caching-fundamentals.md) | ✅ Basics covered |
| Day 22 | [Rate limiting](rate-limiting.md) | ✅ Fundamentals covered |
| Day 23 | [Message queue basics](message-queue-basics.md) | ✅ Fundamentals covered |

## 📚 Learning Roadmap

- [x] Distribute client traffic across backend servers.
- [x] Health checks and removal/recovery of unhealthy instances.
- [x] L4 vs L7 routing.
- [x] Round-robin vs least-connections.

- [x] Stale cache, TTL trade-offs, cache-aside, Redis vs local cache.
- [x] Fixed/sliding window, token bucket, leaky bucket, Redis-backed rate-limit state.
- [x] Producer/consumer queues, traffic buffering, ACK/retry, at-least-once delivery, DLQ.

## 🔁 Revision

- [ ] Explain how health checks affect traffic routing.
- [ ] Compare transport-level and application-level routing with examples.
- [ ] Explain round-robin's limitation with busy/slow servers.
- [ ] Explain why active connection count is a proxy for load.

## 📂 Topic Notes

- [Load balancer fundamentals](load-balancer.md)

- [Caching fundamentals](caching-fundamentals.md)
- [Rate limiting](rate-limiting.md)
- [Message queue basics](message-queue-basics.md)

