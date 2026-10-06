# Caching Fundamentals

## Day 21 — Concepts Covered

A cache keeps a reusable copy of data to reduce repeated computation, latency, or database load. The source of truth can change while a cached copy remains old: this is stale data or cache inconsistency.

## Cache-aside

1. Application checks the cache for a key.
2. On a hit, return the cached value.
3. On a miss, read the database, populate the cache with a TTL, and return the value.
4. After a successful write, invalidate or update the affected cached value.

Cache-aside is application-managed; it does not automatically guarantee consistency. Concurrent requests and writes can still race, so invalidation and acceptable staleness need deliberate treatment.

## TTL Trade-offs

TTL is the time until a cache entry expires. A shorter TTL generally reduces the stale-data window but increases misses and source load. A longer TTL improves reuse but can serve old data longer. Choose based on freshness requirements and update frequency; TTL alone is not a strict consistency guarantee.

## Redis vs Local In-memory Cache

| Choice | Useful when | Trade-off |
|---|---|---|
| Local process memory | Small, frequently reused data; per-instance reuse is sufficient | Very fast, no network hop; each instance has its own copy, memory use, and invalidation state |
| Redis | Multiple application instances need a shared cache | Shared entries and expiration; adds network latency and an external service to operate |

Local caches are appropriate for small reference data when per-instance differences are acceptable. Redis is appropriate for shared cached query results across a scaled application. Neither choice removes the need for expiry, invalidation, or a plan for cache misses.

## Revision

Explain cache-aside for a task lookup, what happens after a task update, and how freshness requirements change the TTL decision. This day covered fundamentals, not a deployed caching implementation.

