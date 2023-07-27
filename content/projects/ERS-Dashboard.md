---
title: "ERS Dashboard"
date: 2023-06-25
draft: false
---

A business partner asked my father for assistance in creating a dashboard system for his online business. The company provides tests to job agencies that they can give to their clients to determine if the client is ready to enter the workforce or to indicate areas that need improvement (https://ersscale.com/). 

My father asked my opinion after realizing that the commercial solution (Power BI by Microsoft) was too expensive and inflexible. After some investagation, I created a website that would solve the problem. Over the next few months, in collabouration with the senior developer at ERS Scale, I made revisions to the site. 

I used python with flask to build a web server then hosted it on Google Cloud Platform for automated scaleability and performance. When a user went to the website, it would read the http variables in their request to determine the agency and timeframe requested, then send another request to ERS Scale’s API for the data. After receiving the data, it would unpack and aggregate the json, then embed it in the response to the client using jinja. Once the client receives the response, custom javascript would display the data as graphs and charts. 

This system allows administrators from any testing location to dynamically see the statistics for that location. I currently maintain the dashboard for his company and make routine bug-fixes and updates using git/gihub for version control. 

The ERS-dashboard project demonstrates my programming, collaboration, and code-maintenance skills. I managed the project from infancy to production, and am very proud of the result. 