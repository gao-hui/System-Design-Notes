# [System Design] Ads Click Prediction

## High-level Design

![Untitled](%5BSystem%20Design%5D%20Ads%20Click%20Prediction%201a28d29439f5484d98d2c4eb3d106243/Untitled.png)

## Ads Features

IDs, Image/Video, Category, Impression and click numbers

![Untitled](%5BSystem%20Design%5D%20Ads%20Click%20Prediction%201a28d29439f5484d98d2c4eb3d106243/Untitled%201.png)

## User Features

Demographics: age, gender, city, coutry…

Contextual information: device, time…

Interaction-related features: clicked ads, user’s historical engagenment statistics…

![Untitled](%5BSystem%20Design%5D%20Ads%20Click%20Prediction%201a28d29439f5484d98d2c4eb3d106243/Untitled%202.png)

## Model Selection

- Logistic regression
- Feature crossing + logistic regression
- Gradient boosted decision trees
- Gradient boosted decision trees + logistic regression
- Neural networks
- Deep & Cross networks
- Factorization Machines (FM); (→ FFM)
- Deep Factorization Machines (DeepFM); (→XDeepFM)
- Deep Interest Network (DIN); (→DIEN)

## Offline Metrics

- Cross-entropy
- Normalized cross-entropy

## Online Metrics

- CTR
- Conversion rate
- Revenue lift
- Hide rate

## Summary

![Untitled](%5BSystem%20Design%5D%20Ads%20Click%20Prediction%201a28d29439f5484d98d2c4eb3d106243/Untitled%203.png)