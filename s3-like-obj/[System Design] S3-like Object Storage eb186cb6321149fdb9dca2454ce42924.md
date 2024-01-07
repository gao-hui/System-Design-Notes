# [System Design] S3-like Object Storage

### Storage System

![Untitled](%5BSystem%20Design%5D%20S3-like%20Object%20Storage%20eb186cb6321149fdb9dca2454ce42924/Untitled.png)

### Storage System

- **Block Storage**
Common storage devices like HDD and SSD that are physically attached to servers. Also include those connected over a high-speed network or over industry-standard connectivity protocols (FC, iSCSI).

- **File storage**
Built on top of block storage, which provides a higher-level abstraction to make it easier to handle files and directories. Do not need to deal with the complexity of managing the blocks, formatting volume, etc.

- **Object storage**
Make a tradeoff to sacrifice performance for high durability, vast scale, and low cost. It targets “cold” data and is mainly used for archival and backup. It uses a flat structure and is relatively slow compared to other storage types.

### Bucket & Object

A bucket is a logical container for objects. An object is an individual piece of data we store in a bucket, which contains object data (payload) and metadata. 

Use **versioning** to keep multiple variants of an object in the same bucket. The object storage provides RESTful **APIs** to access its resources, which are uniquely identified by its **URI**.

The data store (payload) contains **immutable** data while the metadata store (metadata) contains **mutable** data.

![Untitled](%5BSystem%20Design%5D%20S3-like%20Object%20Storage%20eb186cb6321149fdb9dca2454ce42924/Untitled%201.png)

`

### High-level design

![Untitled](%5BSystem%20Design%5D%20S3-like%20Object%20Storage%20eb186cb6321149fdb9dca2454ce42924/Untitled%202.png)

### Data Store

![Untitled](%5BSystem%20Design%5D%20S3-like%20Object%20Storage%20eb186cb6321149fdb9dca2454ce42924/Untitled%203.png)

### Data Store

- Data routing service
Query the placement service to get the best data node to store data.
Read/write data from/to data nodes.

- Placement service
Determine which data nodes should be chosen. Continuously monitors all nodes through heartbeats. Should use 5 or 7 placement service nodes with a consensus protocol.

- Data node
A data service daemon continuously sends heartbeats, which include how many disk drivers and how much data is stored in it.

### Data organization for small objects

![Untitled](%5BSystem%20Design%5D%20S3-like%20Object%20Storage%20eb186cb6321149fdb9dca2454ce42924/Untitled%204.png)

Small files could waste data blocks (~4KB) and exceed the inode capacity.

When we save an object, it is appended to an existing read-write file. When the file reaches its capacity threshold (~GB), mark it as read-only and a new read-write file is created.

### Erasure coding

It chunks data into smaller pieces (placed on different servers) and creates parities for redundancy. 

In the event of failures, can use chunk data and parities to reconstruct. Use a more complex solution with a slower access speed, in exchange for higher durability and lower storage cost. 

![Untitled](%5BSystem%20Design%5D%20S3-like%20Object%20Storage%20eb186cb6321149fdb9dca2454ce42924/Untitled%205.png)

### Correctness verification

![Untitled](%5BSystem%20Design%5D%20S3-like%20Object%20Storage%20eb186cb6321149fdb9dca2454ce42924/Untitled%206.png)

![Untitled](%5BSystem%20Design%5D%20S3-like%20Object%20Storage%20eb186cb6321149fdb9dca2454ce42924/Untitled%207.png)