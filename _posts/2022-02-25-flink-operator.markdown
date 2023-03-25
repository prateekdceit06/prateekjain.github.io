---
layout: post
title:  "Heterogeneity-Aware Operator Placement for Stream Processing Systems at the Edge
Optimizing Edge Resources"
date:   2022-02-25 13:25:13 -0400
cover: post-image1.png
categories: flink raspberry streaming
description: Our team has been working on a heterogeneity-aware system for operator placement in stream processing systems at the edge to optimize edge resources. We implemented a cost model, a scheduler for offloading operators, and identified parameters impacting operator placement. Our solution utilizes edge computing clusters and improved efficiency while reducing latency. Though we faced some challenges in implementing the system, we believe our work has the potential to revolutionize the use of edge resources.
---

# Introduction

As part of our work in the field of edge computing, my team and I have been working on developing a solution to optimize edge resources for stream processing systems at the edge. Our work has been driven by the rapid growth of edge computing applications and the need to efficiently utilize edge resources such as Raspberry Pi devices.

To address this need, we developed a heterogeneity-aware system for operator placement in stream processing systems at the edge. Our solution utilizes edge computing clusters to efficiently use resources and improve latency and throughput. We identified parameters that impact the decision of which operators to offload, such as complexity, selectivity, bandwidth, round-trip time, and data rate.

# Cost Model
We developed a cost model to decide which operators to offload and implemented a scheduler for offloading operators to Raspberry Pi devices. Our filter operator was selectively designed to forward certain data to the downstream operator, making the process highly efficient. We offloaded operators based on selectivity and complexity, and the results were impressive, improving the efficiency and reducing the latency of edge computing applications.

# Benchmark
To benchmark our model, we modified the Nexmark query and collected metrics such as selectivity rate and true output processing rate. We identified other metric parameters to consider and ran experiments to vary bandwidth, data rate, and round-trip time. Our results were highly technical, and we were able to gain valuable insights into the efficient use of edge resources.

# Challenges
We faced some challenges in implementing our system, including the lack of documentation for collecting metrics inside the Flink environment using REST APIs. We also had to configure our system heterogeneously, requiring deployment scripts and a custom Flink build to work on Raspberry Pi devices. Additionally, we faced challenges in modifying Nexmark queries to benchmark the model and debugging the custom scheduler to pick up the correct configuration.

# Conclusion
Overall, we are proud of the work we have done to develop a heterogeneity-aware system for operator placement in stream processing systems at the edge. We believe that our solution has the potential to revolutionize the way we use edge resources, and we are excited to continue developing and experimenting with our system to improve the efficiency and reduce the latency of edge computing applications.