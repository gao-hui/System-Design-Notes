# [System Design] Nearby Friends

Compare to [Proximity Service], data is more dynamic.

High-level design

![Untitled](%5BSystem%20Design%5D%20Nearby%20Friends%200a694020e743424c878bff59ac1a352d/Untitled.png)

Workflow

![Untitled](%5BSystem%20Design%5D%20Nearby%20Friends%200a694020e743424c878bff59ac1a352d/Untitled%201.png)

## WebSocket servers scaling

Each client maintains a persistent conn to one of the WebSocket servers, which will forward the updated info. WebSocket connections handler for each active friend subscribes to the Pub/Sub. 

Stateful, must be taken when removing existing nodes. Mark a node as “draining” at LB, so that no new conns will be routed to it. Once all existing conns are closed, the server can be removed.

## Pub/Sub Servers

![Untitled](%5BSystem%20Design%5D%20Nearby%20Friends%200a694020e743424c878bff59ac1a352d/Untitled%202.png)

## Scaling consideration for Pub/Sub servers

- There will be a ton of re-subscription requests.
- During the re-subscription events. some location updates might be missed.
- Resizing should be done when usage is at its lowest.

## Nearby random person

![Untitled](%5BSystem%20Design%5D%20Nearby%20Friends%200a694020e743424c878bff59ac1a352d/Untitled%203.png)

## Adding/removing friends

Register a callback on a mobile client whenever a new friend is added, which sends messages to WebSocket Servers to subscribe to the new friend’s Pub/Sub channel.

## Alternative to Redis Pub/Sub

Erlang is a general programming language and runtime environment built for highly distributed and concurrent applications. It has Lightweight processes and is easy to distribute among many Erlang servers. We can implement the WebSocket service in Erlang and replace the cluster of Redis Pub/Sub with a distributed Erlang application. Subscription is native in Erlang/OTP.