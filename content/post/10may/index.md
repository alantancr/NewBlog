---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Automating Reports"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-05-10T18:12:15+08:00
lastmod: 2020-05-10T18:12:15+08:00
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

As I was sharing on the previous post about automating report, I have done some researched on automation. There are few methods to achieve this, we can use:

- Airflow
- Cron 
- Window Scheduler for Windows Users

In my submission, I have wrote a bash script which includes the dependicies (requirements.txt) and follow by my python script.

```nano
#!/bin/bash
requirements.txt
script.py
```

Click [here](https://www.hastac.org/blogs/joe-cutajar/2015/04/21/how-make-simple-bash-script-mac) if you wish to refer for some basic bash script guide.

 I have assumed in the scenario of using a virtual machine on linux. The scenario given was to automate the report every month end. Using Crontab, it is scheduled to run the script and check if the next day is 01, this is especially critical because we have February which has a lesser number of days. 

Below is the vi script save in crontab:

 

```nano
# For details see man 4 crontabs

# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name  command to be executed
```



```nano
 50 23 28-31 * * [ "$(date +%d -d tomorrow)" = "01" ] && {path of script}/bashscript
```

Airflow maybe a better option as it provides the power of scheduling the analytics workflow and Data warehouse also managed under a single roof so that a comprehensive view accessed to check the status.



