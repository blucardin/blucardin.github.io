---
title: "Video to Ascii Art"
date: 2023-07-22T02:03:27-07:00
draft: false
---

I was bored one weekend so I decided to create some code to convert videos to ascii art. Everyone in my ICS class was trying to get slightly higher marks by including ascii gifs in their console projects and I wanted to show off a bit.  
 
I used python with the pillow image library to read in video/image files, convert each frame to ascii art, and stitch everything back together. The final code was quite simple but worked really well.  

The pseudocode for the algorithm I used to determine the ascii representation of each image is as follows: 

    Resize the image to be about ½ the resolution.
    Convert the image to grayscale. 
    For every pixel in the new image:
        Map the brightness to a value between 0 and 23
        Use that map to index this “.'-~|/+<?vcrenXuOAQ8d$”
        Write the letter with the original color and brightness of the pixel onto the image 

I enjoyed the project, and got some cool videos to show for it. 

All code and video samples can be found here: https://github.com/blucardin/image-to-Ascii
