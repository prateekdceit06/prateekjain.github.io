---
layout: post
title:  "Breaking Boundaries: A Scalable Distributed MD5 Hash Matching System"
date:   2022-10-15 13:25:13 -0400
cover: post-image1.png
categories: distributed md5 networking
background: style-1
description: Distributed MD5 Hash Matching Scalable Password Cracking System is a project that designs a distributed system for cracking 5-character passwords using MD5 hash matching. The system employs a web interface, a management service, and multiple worker nodes to enable scalable brute-force attacks. Users can add or remove worker nodes, improving efficiency and adaptability.
---
This article delves into the design and implementation of a scalable distributed system for MD5 hash matching. With a user-friendly web interface and a robust management service, the system efficiently cracks passwords using a brute force approach. The project demonstrates the power of distributed systems, REST APIs, and real-world web applications, while also touching upon important concepts like SSH tunneling and client-server communication.

<h1>Introduction</h1>
In recent years, distributed systems have gained prominence in a variety of applications, offering improved performance, scalability, and fault tolerance. One such application involves matching MD5 hashes for password-cracking purposes. This article explores the design and implementation of a distributed system that can efficiently crack 5-character alphabetical passwords using a brute force approach, leveraging the power of multiple worker nodes.

<h1>Problem Statement and Learning Outcomes</h1>
The primary goal of the project is to create a scalable distributed system that cracks MD5 hashes for 5-character passwords. The system should be capable of distributing workload among multiple worker nodes and responding to the client with the appropriate outcome. In the process, the project aims to provide insights into the implementation of a distributed system, the significance of REST APIs, deployment of single-page applications, SSH tunneling, and maintaining client-server connections.

<h1>Design and Setup</h1>
The system's architecture consists of a server-client interaction model, utilizing resources from the GENI network for server and client nodes. A frontend developed in React is deployed on the world wide web to enable user input and communication with the password cracker server running on Geni.

<h1>Execution and Results</h1>
To reproduce the experiment, a slice on Geni with 1 server and 10 clients is created using a provided RSPEC file. Python 3.7, Flask 2.2.2, and Ngrok are used for setting up the environment, while the server and clients are configured using a series of SSH commands.

<h1>Metrics and Analysis</h1>
The experiment is run 50 times with varying bandwidth values and numbers of clients. Two key metrics are analyzed: the total time required to break the given hash and the total time required to process a file. Results indicate that the time required to crack a password decreases as more clients are added and as the bandwidth value increases.

<h1>Conclusion</h1>
This project demonstrates the power and flexibility of distributed systems in efficiently cracking MD5 hashes. Through a user-friendly web interface and an effective management service, the system enables the distribution of workload among multiple worker nodes, resulting in improved performance and scalability. The learnings from this project can be applied to other distributed system applications, further enhancing their capabilities and efficiency.


Check out more about the project through this [report.][projectpdf-link]

[projectpdf-link]: https://drive.google.com/file/d/1zp3tYJyh-yDjSKDW8yI3Et8wYyr6T-0R/view