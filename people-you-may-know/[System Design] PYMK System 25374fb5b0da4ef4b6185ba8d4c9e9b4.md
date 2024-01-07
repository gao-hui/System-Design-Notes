# [System Design] PYMK System

## High-Level Design

![Untitled](%5BSystem%20Design%5D%20PYMK%20System%2025374fb5b0da4ef4b6185ba8d4c9e9b4/Untitled.png)

### Pointwise Learing to Rank (LTR)

Take 2 users as input, out the probability of forming a connection

not consider social context

### Graph-Based Prediction

- Graph-level prediction
    
    predict if a chemical compound is an enzyme
    
- Node-level-level prediction
    
    predict if a specific user (node) is a spammer
    
- Edge-level prediction
    
    predict if two users are likely to connect
    

## Edge Prediction

![Untitled](%5BSystem%20Design%5D%20PYMK%20System%2025374fb5b0da4ef4b6185ba8d4c9e9b4/Untitled%201.png)

### Features

- User: demographic, number of connections
- Interactions: connection req, accept, follow, search, view, like…
- User-User: connections, schools, major, Companies in common
- Social: profile visits, number of connections, time discounted mutual connections

### GNN

e.g., GCN, GraphSAGE, GAT, GIT

Nodes store info like age, gender… 

Edges store user-user info like common schools, connections…

GNN produces node embeddings for each node. Then perform similarity measures like dot product to predict if there is an edge between two users

## GNN Training Labels

![Untitled](%5BSystem%20Design%5D%20PYMK%20System%2025374fb5b0da4ef4b6185ba8d4c9e9b4/Untitled%202.png)

### GNN Predicting

![Untitled](%5BSystem%20Design%5D%20PYMK%20System%2025374fb5b0da4ef4b6185ba8d4c9e9b4/Untitled%203.png)

## Scoring Service

![Untitled](%5BSystem%20Design%5D%20PYMK%20System%2025374fb5b0da4ef4b6185ba8d4c9e9b4/Untitled%204.png)

## Summary

![Untitled](%5BSystem%20Design%5D%20PYMK%20System%2025374fb5b0da4ef4b6185ba8d4c9e9b4/Untitled%205.png)