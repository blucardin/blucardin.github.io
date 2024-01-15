---
title: "Christmas Lights Version 2"
date: 2024-01-04
draft: false
---

<iframe width="100%" height="475"src="https://www.youtube.com/embed/qRL0N3ooU7c?si=6yHi9NtoIwvrpivd" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

This project is a continuation of my [Christmas Lights](/projects/Christmas-Lights) project.

My Christmas tree lights project involved playing video on a set of addressable Christmas tree lights.

The program first determines the relative positions of the lights by turning on each light in sequence and using a camera to see where they are. This generates a list of coordinates which are stored on disk. Then for each frame of a video, the program resizes the frame to fit the light positions, then assigns each light the corresponding color at that point on the frame. Finally, it displays each frame on the light in sequence.

The lights were driven by a raspberry pi with low compute capacity. To increase speed, operations were split into different parts and run between my laptop and the pi. The pi would calculate the positions. Using the positions my laptop would calculate the colors for each frame. Using the colors for each frame, the pi would display the images. The laptop was connected to the pi via SSH over my home network allowing me to play video from anywhere in my home.
