---
layout: post
title:  "Building a Scalable Distributed System for MD5 Hash Matching"
date:   2022-11-15 13:25:13 -0400
cover: post-image5.png
categories: distributed md5 networking
description: Distributed MD5 Hash Matching Scalable Password Cracking System is a project that designs a distributed system for cracking 5-character passwords using MD5 hash matching. The system employs a web interface, a management service, and multiple worker nodes to enable scalable brute-force attacks. Users can add or remove worker nodes, improving efficiency and adaptability.
---
# Introduction

Distributed systems are an essential part of modern-day applications that require high performance, scalability, and fault tolerance. One of the most common use cases for distributed systems is password cracking, which involves matching MD5 hashes for password-cracking purposes. This article explores the design and implementation of a distributed system that can efficiently crack 5-character alphabetical passwords using a brute force approach, leveraging the power of multiple worker nodes.

# Problem
The primary goal of this project is to create a scalable distributed system that cracks MD5 hashes for 5-character passwords. The system should be capable of distributing workload among multiple worker nodes and responding to the client with the appropriate outcome. In the process, the project aims to provide insights into the implementation of a distributed system, the significance of REST APIs, deployment of single-page applications, SSH tunneling, and maintaining client-server connections.

# Design and Setup

The system's architecture consists of a server-client interaction model, utilizing resources from the GENI network for server and client nodes. The client-facing web interface is built using React, while the password-cracking server is built using Python's Flask framework. The communication between the client and server is established through a REST API, and SSH tunneling is used to ensure secure communication between the nodes.

# Execution and Results
To reproduce the experiment, a slice on GENI with 1 server and 10 clients is created using a provided RSPEC file. Python 3.7, Flask 2.2.2, and Ngrok are used for setting up the environment, while the server and clients are configured using a series of SSH commands. Once the setup is complete, the password-cracking experiment is run 50 times with varying bandwidth values and numbers of clients. The two key metrics analyzed are the total time required to break the given hash and the total time required to process a file. Results indicate that the time required to crack a password decreases as more clients are added and as the bandwidth value increases.

# Analysis
The analysis of the experiment's results shows that the system's performance is directly proportional to the number of clients and the available bandwidth. The average time required to crack a password is reduced from 5 minutes to under a minute as more clients are added, making the system more scalable and efficient. Moreover, the analysis shows that the total time required to process a file is directly proportional to the size of the file and the available bandwidth, highlighting the importance of considering these factors while designing and implementing distributed systems.

# Conclusion
This project demonstrates the power and flexibility of distributed systems in efficiently cracking MD5 hashes. Through a user-friendly web interface and an effective management service, the system enables the distribution of workload among multiple worker nodes, resulting in improved performance and scalability. The learnings from this project can be applied to other distributed system applications, further enhancing their capabilities and efficiency. Overall, this project provides valuable insights into the design and implementation of distributed systems, REST APIs, SSH tunneling, and client-server communication.

Check out more about the project through this [report.][projectpdf-link]

[projectpdf-link]: https://drive.google.com/file/d/1C6D0ipEkrFN-qYyeWHmeqATqYVZ9CFnj/view