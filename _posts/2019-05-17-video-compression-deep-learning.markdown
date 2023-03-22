---
layout: post
title:  "Video Compression & Deep Learning"
date:   2019-10-30 13:25:13 -0400
categories: video-compression AI deep-learning
background: style-2
description: In today’s world, video consumption has become an indispensable part of people’s life. Artificial Intelligence and Deep Learning models might be able to help us in compressing videos and save huge amounts of storage space.
---
In today’s world, video consumption has become an indispensable part of people’s life. The most popular way to consume content in this format is through the internet. More than 60% of the world’s internet data consumption is consumed by video streaming and it is still considered growing. More and more players are getting into this field including big names like Disney and Apple while existing players like Netflix and Amazon continue to grow. Platforms like YouTube also play an important role in this field. It is undeniably extremely important that the video we serve on the internet should be most optimized and compressed to save massive amounts of data as well as money for both users as well as corporates investing in this business. While the compressed video will not only save data consumption costs for consumers and ISPs but would also help in delivering higher resolution and quality videos with the existing internet speeds. Slower internet connections result in low-resolution video streaming, which has been a concern for many companies in this field because this leads to lower quality of experience to the end-users than the quality standards and benchmarks set by these companies to ensure optimal viewing experience.

<h1>How does this work?</h1>
The process of compressing video files is called video encoding. There are many popular ways to compress video files (the most popular being H.264). Encoding method H.264 compression has since become standard across the industry due to its advantages in efficiency as well as extend to which it compresses video files. Though there are few better standards available like H.265 which is better in many ways, these are still not widely used on the internet. HTML standards have provided video players with pretty wide decoding formats.

Ideally, the best compression should have an accompanying decoder written on language written for the internet and browsers, like Javascript. Therefore the best possible compressed video files should be tailor-made for streaming, for which decoder should be written on Javascript.

For implementing Deep learning-based video compression for the internet, the main challenge is implementing a decoder in Javascript for that compression model.

<h1>Implementation</h1>
A deep learning model that uses motion estimation and techniques like entropy coding should provide good compression. Compression time should not really be a big concern, the quality and bitrate should be important while designing this model because compression is a one-time process for videos. Decoding should be done on the client-side with a decoder written in Javascript so that it can be widely used on the web.

<h1>Proposed idea</h1>
The idea is to create a full-stack web application, which functions similar to Youtube, users are allowed to upload video as well as stream. For demo purposes, the following tech stack is used -
1. Tensorflow, PyTorch, or Keras — For Video Encoding
2. Django REST or NestJS - For Backend
3. MongoDB - Used as Database
4. ReactJS — For frontend
5. Tensorflow JS or Keras JS — For Video Decoding

The Encoding is done using a deep learning model which uses techniques like motion estimation, entropy encoding, and vector decomposition to compress video file and pack it into binaries. More processing is done to compress the video further by using reference frames and providing the changed pixel information as well as dividing the video into chunks and packing necessary reference frames with those chunks. These will ensure video to be compressed as well as split into chunks ready to be sent to the frontend for decoding.

The Flask or Django REST-based backend would help in the usual token-based authentication as well as would carry out many features for the web application. This API would also be responsible for sending video chunks for the frontend to decode. Flask with SQLAlchemy as well as Django has pretty good ORM (Object Relational Mapping), which would also us to build and maintain a database easily. The MySQL-based database would contain useful information as well as video metadata. For the sake of the demo, the fuzzy search should be enough for the video search feature which would again be implemented in our backend service.

Building frontend on a modular framework like Angular should be pretty good and simple, as it provides faster development benefits as well as the component system which should help make beautiful user interfaces with less effort. There is a lot of online support available for this framework due to its popularity as well as it is based on TypeScript which should help write our decoder on it.
The decoder should be pretty straightforward once the encoding is fixed. The main problem would be rendering speed as complex compression algorithms would result in slow decoding which would lead to slow and heavy decoding speeds. A very efficient decoder is the biggest challenge, as well as the decoder, should be light to be widely compatible. Although taking the faster computing speed in modern devices into account, one could aim for targeting those high-speed devices and make this compression for modern and future devices.

<h1>Compression using Deep Learning</h1>
There are a lot of research papers and techniques available online, but most of them are not implemented yet. The idea here is to read them and gather the best practices from them and implement them. Decoding becomes one for the biggest problem as most of the model encodes using Deep Learning and then the decoder is also trained as model in Python, but for writing the same decoding in JavaScript is simply not possible. The decoder model could be exported and somehow be used through JavaScript to be used on the web, but that won’t exactly be an efficient solution. As well as heavy compression algorithms would require matrix multiplications on the frontend to decode, which would again be a bit heavy for clients. Finding a good balance and writing in the most efficient possible way should be the main concern here for this work successfully.

Check out this [report][report-link] for more info on data consumption trends of the internet.

[report-link]: https://www.sandvine.com/phenomena