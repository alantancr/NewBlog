---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Capstone Project"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-03-30T10:23:06+08:00
lastmod: 2020-03-30T10:23:06+08:00
featured: true
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: "Center"
  placement: 2
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

# Hotel Pal: A Content-based recommender

I will be sharing my thoughts  about the project, challenges I have faced and after thoughts of the project. 

## Objective

As part of GA curriculum, I built a end-to-end content based recommender engine, deployment on Heroku via Flask. The objective is to transform implicit information provided by users into explicit features for hotel recommendation system engine. There are two parts to this recommender engine using hotel attributes and reviews by users respectively to build two separate recommendation engine. 



## Executive Summary

In a very general way, recommender systems are algorithms aimed at suggesting relevant items to users (items being movies to watch, text to read, products to buy or anything else depending on industries).

**There are two main data selection methods:**

Collaborative-filtering: In collaborative-filtering items are recommended, for example hotels, based on how similar your user profile is to other users’, finds the users that are most similar to you and then recommends items that they have shown a preference for. This method suffers from the so-called cold-start problem: If there is a new hotel, no-one else would’ve yet liked or watched it, so you’re not going to have this in your list of recommended hotels, even if you’d love it.

Content-based filtering: This method uses attributes of the content to recommend similar content. It doesn’t have a cold-start problem because it works through attributes or tags of the content, such as views, Wi-Fi or room types, so that new hotels can be recommended right away.

The point of content-based is that we have to know the content of both user and item. Usually you construct user-profile and item-profile using the content of shared attribute space. For example, for a movie, you represent it with the movie stars in it and the genres (using a binary coding for example).

**There are a number of popular encoding schemes but the main ones are:**

- One-hot encoding
- Term frequency–inverse document frequency (TF-IDF) encoding
- Word embeddings

In this project, we will be discussing content-based filtering of recommender engine, turning implicit attributes into explicit features for hotel recommender engine.

Details can be found on my github [repo](https://github.com/alantancr/Hotel-Recommender).



## My thought process

I would like to share my experience in terms of the  process of this capstone. As a beginner in data science project, the first challenge I have faced was selecting the appropriate topic to work on and capturing the end goal of the project.  

1. Being objective and selecting a digestible topic within timeline

   With given about 4-5 weeks timeline, I took consideration of choosing a topic which I could complete on time.  Since I was always interested about how Netflix throws us recomendations of movies/shows we might like, I zoomed into looking at recommender systems. The recommender was introduced as part of unsupervised machine learning techniques in the course around week 7-8, so I have sufficient time to read up and do my research on building recommender engine. It took me around 2-3 weeks to settle in on a topic which I want to work on and how my project demostration will look like. The  difficult part is to conceptualise how the demostration will look like, what information to use and illustrate on.

   

2. Goals of  project

   I also took consideration of building a demo as part of my consideration for the project. Because with the aid of demo, it will be helpful for my audience to understand what I am trying to deliver. From project managment perspective, I inked down the various timeline I need to meet in order the final deadline. I also evaluated the difficulty of each task, giving more time for deployment since it was my first time deploying on Flask and using Heroku. Base on my experience on deployment when i was doing my Graduate Diploma, the deployment is the phase where I did a lot of self reading and debugging. 

   

3. Technical perspect of the project

   One of the key issues which I faced initially when I was writing the code to compile a sparse matrix and tabulating a cosine-similar matrix was computation power. My current MacBook has only 8gb Ram and some codes takes a bit of computation power. I explored Google Colab and Sagemaker, and as recommended by TA, AWS Sagemaker is so much efficient and easy to use. It has exactly the same user interface as jupyter notebook. Moreover, the better computation specifications is not really costly as  long as you remember to turn off the instance after usage.  3-4 hours of a ml.t2.2xlarge (32gb ram) cost me about 3-4 USD. 

   

   In the deployment phase, there are guides available online and it is really useful. One of the website which i followed diligently is this [article](https://stackabuse.com/deploying-a-flask-application-to-heroku/). I felt that the most challenging part was the http protocols, GET and POST requests and how information are passed through these requests. Fortunately, I have tapped on my past experience in software development to build the site. I have considered using a docker and host in AWS but utlimately my application is not intensive. I felt Heroku works for me now and it's free anyway.

   

   # Looking back

   This journey was really interesting. I learnt to look at problems in a different perspective and building an end-to end solution needs to go through a lot more thought process. I tried different technology and see how it work or did not work for me.

   





