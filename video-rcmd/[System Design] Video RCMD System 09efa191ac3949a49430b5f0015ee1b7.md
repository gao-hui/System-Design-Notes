# [System Design] Video RCMD System

## High-Level Design

![Untitled](%5BSystem%20Design%5D%20Video%20RCMD%20System%2009efa191ac3949a49430b5f0015ee1b7/Untitled.png)

## Candidate Generation

![Untitled](%5BSystem%20Design%5D%20Video%20RCMD%20System%2009efa191ac3949a49430b5f0015ee1b7/Untitled%201.png)

## Scoring

Prioritize accuracy over efficiency

Use conten-based filtering and heavier models relying on video features.

![Untitled](%5BSystem%20Design%5D%20Video%20RCMD%20System%2009efa191ac3949a49430b5f0015ee1b7/Untitled%202.png)

## User Features

![Untitled](%5BSystem%20Design%5D%20Video%20RCMD%20System%2009efa191ac3949a49430b5f0015ee1b7/Untitled%203.png)

## User-Video Interaction Features

![Untitled](%5BSystem%20Design%5D%20Video%20RCMD%20System%2009efa191ac3949a49430b5f0015ee1b7/Untitled%204.png)

## Video Features

![Untitled](%5BSystem%20Design%5D%20Video%20RCMD%20System%2009efa191ac3949a49430b5f0015ee1b7/Untitled%205.png)

## Types of RCMD System

**Content-based filtering**: use video features to recommend videos similar to previous

Handle new videos, slower, need domain knowledge, cannot find new interest

**Collaborative filtering (CF)**: use user-user or video-video similarities

Cannot handle new videos, faster, no domain knowledge, discover new interest

**Hybrid filtering**: combine CF-based and content-based sequentially or in parallel

![Untitled](%5BSystem%20Design%5D%20Video%20RCMD%20System%2009efa191ac3949a49430b5f0015ee1b7/Untitled%206.png)

## Two-Tower Network (candidate generation)

![Untitled](%5BSystem%20Design%5D%20Video%20RCMD%20System%2009efa191ac3949a49430b5f0015ee1b7/Untitled%207.png)

## Re-Ranking

- Region-restricted videos
- Videos freshness
- Videos spreading misinformation
- Duplicated
- Fairness and bias

## Cold-Start Problem

**New users:**

- Use user basic features: age, gender…
- After the user interacts with more videos, can do better

**New videos:**

- Use baisc metadata and content
- Display videos to random users to collect interaction data

## Summary

![Untitled](%5BSystem%20Design%5D%20Video%20RCMD%20System%2009efa191ac3949a49430b5f0015ee1b7/Untitled%208.png)