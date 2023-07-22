---
title: "Candy Canes"
date: 2023-07-22T02:03:26-07:00
draft: false
---

My school has an annual candy cane sale where any student can buy a candy cane for any other student. 

One day, I had some spare time after school and went to help with the packaging of candy canes. What I saw shocked me. Due to the pandemic, candy canes had moved to online google form registration, away from physical handwritten notes. The poor organizer was manually copy-pasting information from the google form submissions into canva to be printed!

In most cases, this would be completely fine, however, there were 1000+ submissions with 5 fields each. The organizer was staying up all night trying to move over 5000 values before the scheduled distribution deadline. If there were any mistakes, the candy cane would be misdelivered, and people would be sad. 

I requested the spreadsheet from her and when I got home that night I got to work. After researching the best methods, I wrote custom google apps-script javascript code to automatically fill in a google slides presentation with the values in under 5 minutes. 

The organizer was overjoyed, and the event was a giant success. 

The next year, I reached out to the new leaders of the event, because I knew they were going to make the same mistake as the first person. After more research, I found the most efficient way to do it was to convert the spreadsheet to an excel document, mail merge it onto a template, export as png images, then use python to compile them into one large pdf for mass printing. 

The code to do this is below. I would attach a sample output, however it contains sensitive candy-cane information (names, personal notes, etc.).

<script src="https://gist.github.com/blucardin/8d8460bf651970863ae64fcfffa0f9a0.js"></script>