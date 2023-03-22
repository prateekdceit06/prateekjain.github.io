---
layout: post
title:  "Operator placement on edge systems in stream processing"
date:   2023-02-28 13:25:13 -0400
categories: streaming flink raspberrypi
background: style-2
description: Working on a heterogeneity-aware operator placement project, our team utilized Raspberry Pi devices and Apache Flink to optimize edge offloading for stream processing systems, reducing latency and data traffic while maximizing resource efficiency in real-time data processing.
---
This article discusses a project that aims to enhance stream processing systems by offloading processing tasks to edge systems, specifically Raspberry Pi devices, to reduce data traffic and latency overhead caused by the limited bandwidth of Wide Area Networks (WANs). The proposed solution involves developing a cost model and modifying the Apache Flink scheduler to efficiently offload tasks to edge systems, ultimately improving latency problems over the WAN.

<h1>Introduction</h1>
Stream processing systems are crucial for handling real-time data, but they often face challenges related to limited resources and strict latency requirements. To address these issues, this project proposes a heterogeneity-aware operator placement algorithm for stream processing systems that offloads tasks to edge systems, specifically Raspberry Pi devices, to optimize resource utilization and minimize latency overhead.

<h1>Problem Statement</h1>
Traditional stream processing systems like Flink are designed for homogeneous data center servers, making them unsuitable for automatically offloading tasks to edge systems. This limitation results in high latency and inefficient resource utilization when streaming applications ingest data from multiple sources across different locations via a WAN with limited bandwidth and high latency.

<h1>Proposed Solution</h1>
The proposed solution involves preprocessing data streams at the edge to reduce data traffic and latency overhead over the WAN. This can be achieved by identifying tasks that can be offloaded to edge systems using performance metrics, and implementing a dynamic mechanism to automatically predict data stream flow, compute metrics, and decide which tasks can be offloaded to increase efficiency. The project will extract performance metrics like backPressureTimeMsPerSecond, idleTimeMsPerSecond, busyTimeMsPerSecond, and numRecordsOutPerSecond to calculate the maximum output rate an instance can sustain for every task. Using this information, the Flink scheduler will be modified to offload tasks to edge systems.

<h1>Expectations</h1>
The project aims to implement a prototype that can offload tasks to edge systems, reducing data traffic and latency overhead caused by limited WAN bandwidth. The system is expected to efficiently utilize edge resources, minimize server-side resource usage, and improve system efficiency without sacrificing performance.

<h1>Experimental Plan</h1>
The experimental setup for evaluating the solution will include a cloud server/local server, Raspberry Pi 4B, Apache Flink, Python, and Java. The scheduling algorithm will begin by running all tasks on the server side (except the source) and collecting performance metrics from Flink. Lightweight operators will then be placed on available edge slots. The initial prototype will be built using Flink and Raspberry Pi, with tests conducted on open-source datasets to identify suitable tasks for offloading to edge systems.

<h1>Success Indicators</h1>
The project will be considered successful if it can demonstrate improved performance compared to conventional approaches. Major milestones include making Flink compatible with heterogeneous resources, implementing a cost model to determine which operators can be offloaded to edge systems, and changing the placement configuration based on the cost model output.

<h1>Conclusion</h1>
The proposed heterogeneity-aware operator placement algorithm aims to improve the performance of stream processing systems by offloading tasks to edge systems, specifically Raspberry Pi devices. By doing so, it seeks to minimize latency overhead and resource utilization, providing a more efficient solution for processing real-time data streams.