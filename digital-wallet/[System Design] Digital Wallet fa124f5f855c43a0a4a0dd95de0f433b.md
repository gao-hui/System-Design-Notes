# [System Design] Digital Wallet

**Distributed transaction**

- **2PC**

![Untitled](%5BSystem%20Design%5D%20Digital%20Wallet%20fa124f5f855c43a0a4a0dd95de0f433b/Untitled.png)

the lock can be held for a long time; the coordinator can be a single point of failure.

- **Try-Confirm/Cancel (TC/C)**

![Untitled](%5BSystem%20Design%5D%20Digital%20Wallet%20fa124f5f855c43a0a4a0dd95de0f433b/Untitled%201.png)

1 Reserve resources. 2 The coordinator collects replies, if all yes, do try-confirm; else do try-cancel.

## Phase status table

![Untitled](%5BSystem%20Design%5D%20Digital%20Wallet%20fa124f5f855c43a0a4a0dd95de0f433b/Untitled%202.png)

The service maybe restarts in the middle of TC/C. Need to store the progress of a TC/C in a transactional database.

### Saga

![Untitled](%5BSystem%20Design%5D%20Digital%20Wallet%20fa124f5f855c43a0a4a0dd95de0f433b/Untitled%203.png)

1 Each operation is an independent transaction on its own DB. 2 When one operation is finished, the next operation is triggered. 3 If one failed, roll back from the current to the first in reverse.

Saga executes linearly, TC/C could in parallel.

### Event sourcing

![Untitled](%5BSystem%20Design%5D%20Digital%20Wallet%20fa124f5f855c43a0a4a0dd95de0f433b/Untitled%204.png)

State machine: 1 validate commands and generate events; 2 apply the event to update the state

### Command-query responsibility segregation (CQRS)

![Untitled](%5BSystem%20Design%5D%20Digital%20Wallet%20fa124f5f855c43a0a4a0dd95de0f433b/Untitled%205.png)

CRQS: Rather than publishing the state, event sourcing publishes all the events. The external world could rebuild the state by itself.

Independent scaling; Optimized data scheme…

### File-based command and event list

![Untitled](%5BSystem%20Design%5D%20Digital%20Wallet%20fa124f5f855c43a0a4a0dd95de0f433b/Untitled%206.png)

Append-only data structure; cache recent commands and events in memory; use mmap to write to a local disk and cache recent content in memory at the same time.

![Untitled](%5BSystem%20Design%5D%20Digital%20Wallet%20fa124f5f855c43a0a4a0dd95de0f433b/Untitled%207.png)