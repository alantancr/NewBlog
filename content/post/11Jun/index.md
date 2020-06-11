---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Docker and deploying on Heroku"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-06-11T15:53:06+08:00
lastmod: 2020-06-11T15:53:06+08:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

What is Docker and why it is used?

Docker is a tool designed to make it easier to create, deploy, and run applications by using containers. Containers allow a developer to package up an application with all of the parts it needs, such as libraries and other dependencies, and deploy it as one package. 

[Here's](https://docker-demo-app.herokuapp.com/) a simple Docker app which runs on Flask and deployed on Heroku.

In the file directory, these are the few files which you required to have them.

- app.py (where your code should be written)
- Dockerfile (Docker builds images automatically by reading the instructions from a `Dockerfile` -- a text file that contains all commands, in order, needed to build a given image. A `Dockerfile` refers to a specific format and set of instructions.)
- requirements.txt



**First**:

As a demonstration purpose, my Flask app returns me when I run app.py on localhost. 

> Hello, this is a test for Docker image hosting on Heroku.

**Second**:

In your virtual environment, freeze the dependencies into requirements.txt

Run this in cmd:

```
pip freeze > requirements.txt

```

Since this app is relatively simple, there are only two dependencies that you should need which are mainly:

- Flask
- gunicorn

 **Third**:

The third file is the Dockerfile. There are a set of rules in writing Dockerfile, refer [here](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/).

To generate a Dockerfile, in the working directory on command terminal:

```
touch Dockerfile
```

Once Dockerfile is created, edit the content in Dockerfile with vi or you can use Nano editor. 

```
vi Dockerfile
```

In vi, edit the file and save the content. In this instance, I have choosen a python environment:

```
FROM python:3.7.3-slim

COPY requirements.txt /
RUN pip3 install -r /requirements.txt

COPY . /app
WORKDIR /app

CMD gunicorn app:app --bind 0.0.0.0:$PORT --reload
```

Do remember to save this Dockerfile in vi editor.

Now we are ready to build our Docker image, perform these commands on terminal:

- Build the image with `docker build -t your-app-name .`
- Run the container with `docker run -d -p 5000:5000 -e PORT=5000 --name your-app-server-name your-app-name`
- Check whether the container is running
- Go to `localhost:5000`. You should see  `Hello, this is a test for Docker image hosting on Heroku.`

**<u>Deployment</u>**

Heroku supports container deployment and below are the steps to deploy it on Heroku.

Perform these on terminal:

- Login to Heroku container. It would open the browser and prompt you to login with your Heroku credentials if you are not logged in already. If you are logged in, you will see "Login Succeeded"

  `heroku container:login`

- Creating the application name on Heroku. Make sure you have the 3 files in the same folder.

  `heroku create your-app-name`

- Creating the Heroku container on the app

  `heroku container:push web --app your-app-name`

- Releasing the container on app

  `heroku container:release web --app your-app-name`

- Open your application, You should see `Hello, this is a test for Docker image hosting on Heroku.`

[Here](https://github.com/alantancr/docker-demo) is the demo code. 

![alternative text for search engines](/post/11June/dockerimage.png)

