# Load Balancer Fundamentals

## Day 20 — Load Balancer Fundamentals

A load balancer distributes incoming client traffic across multiple backend servers, supporting availability and scaling.

### Health Checks

Check backend health, exclude unhealthy instances from new traffic, and return recovered instances to rotation after they pass the health checks.

### L4 vs L7

| Layer | Routing information | Example |
|---|---|---|
| L4 — Transport | IP addresses and TCP/UDP ports | Route a connection to a backend. |
| L7 — Application | HTTP host, path, headers, or cookies | Route `/api/*` and `/images/*` to different pools. |

### Round-robin vs Least-connections

- Round-robin cycles through eligible servers in order. It does not account for how busy or slow each server currently is.
- Least-connections chooses a server with fewer active connections. This can help when connection durations vary; connection count is a proxy for load, not a direct measurement of CPU usage.

The Day 20 explanation correctly identified round-robin's limitation with busy/slow servers. Coverage was conceptual; no load balancer implementation was completed.
