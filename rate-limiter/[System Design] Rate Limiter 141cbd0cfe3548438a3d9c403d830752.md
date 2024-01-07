# [System Design] Rate Limiter

### High-Level Design

![Untitled](%5BSystem%20Design%5D%20Rate%20Limiter%20141cbd0cfe3548438a3d9c403d830752/Untitled.png)

Rate limiter middleware loads rules from the cache. It fetches counters and last request timestamp from Redis. 

### Token bucket algorithm

![Untitled](%5BSystem%20Design%5D%20Rate%20Limiter%20141cbd0cfe3548438a3d9c403d830752/Untitled%201.png)

**Bucket size**: the max number of tokens; **Refill rate**: number of tokens put into.

- Pros: memory efficient; allow a burst in short periods;
- Cons: hard to tune the two parameters.

### Leaking bucket algorithm

![Untitled](%5BSystem%20Design%5D%20Rate%20Limiter%20141cbd0cfe3548438a3d9c403d830752/Untitled%202.png)

**Bucket size**: equal to the queue size; **Outflow rate**: processing speed.

- Pros: memory efficient (limited queue size); process at a fixed rate.
- Cons: a burst of traffic will fill up the queue and limit the recent requests; hard to tune the 2 parameters.

### Sliding window log algorithm

![Untitled](%5BSystem%20Design%5D%20Rate%20Limiter%20141cbd0cfe3548438a3d9c403d830752/Untitled%203.png)

Keep track of request timestamps using Redis; Remove outdated timestamps when new requests come; limit according to the log size.

- Pros: accurate, not exceeding the limit.
- Cons: consume lots of memory; need to store timestamp even if a request is rejected.

### Sliding window counter algorithm

![Untitled](%5BSystem%20Design%5D%20Rate%20Limiter%20141cbd0cfe3548438a3d9c403d830752/Untitled%204.png)

requests in the rolling window = Requests in current window + requests in the previous window * overlap percentage of the rolling window and previous window.

- Pros: smooth out spikes through avg; memory efficient.
- Cons: assume the previous window are evenly distributed.