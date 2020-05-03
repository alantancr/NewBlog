---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: Python with Excel Workbook
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-05-03T16:07:41+08:00
lastmod: 2020-05-03T16:07:41+08:00
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

It's been hectic past one month, with circuit breaker , technical assessment and interviews. I would say I have learnt something in each assessment although some of them are really tough. In this post, I will be sharing on working on Python and Excel. 

Pandas has integrated the capability of reading Excel file is really convenient to use. One of the assessment which I have done requires me to perform EDA on Excel file and create charts report in Excel.

```python
#read excel file
df_policy = pd.read_excel('PREMIUM_POLICY_DATA.xlsb',sheet_name='POLICY', engine='pyxlsb')
df_premium = pd.read_excel('PREMIUM_POLICY_DATA.xlsb',sheet_name='PREMIUM', engine='pyxlsb')
```

Engine pyxlsb is used to support for binary Excel files. It was released in on the `1.0.0` release of pandas. 

In this exercise, I created a plot and pin in one worksheet and copy the output data into another sheet. Here is a sample visualisation that I have appended and below is a function I have wrote to append this chart into the sheet.



![](/post/3May/download.png)



**Steps to create a excelwork and worksheet and append image**

1. Import these libraries 

   - Import io

   	- import xlsxwriter

   - from openpyxl import load_workbook

2. You will need to use package xlsxwriter to create a workbook. Create the worksheets which are required. 

3. Instantiate an io for image data

4. Create a function/ run seperate codeline to create a plot and append the position you need

5. Close the workbook to save the image

   

```
#creating a workbook excel file
workbook = xlsxwriter.Workbook('report.xlsx')
wks2=workbook.add_worksheet('report_chart')
#wks1=workbook.add_worksheet('Overview_chart')


#create io for image data for inserting charts
imgdata=io.BytesIO()

```



```python
# function to load dataframe, plot, insert imagedata io into excel with position
def plot_m(df,imagedata,wk,a,b,title):
  	#matplotlib
    df.plot(kind='bar',x="MonthName")
    plt.legend()
    plt.xticks(rotation=0)
    plt.xlabel("Month")
    plt.ylabel("GWP($)")
    #set title
    plt.title(title)
    #set currentfigure size
    plt.gcf().set_size_inches(8, 7)
    #save image
    plt.savefig(imagedata, format='png')
    #insert image into workbook
    #a and b refers to position of the image in the worksheet
    wk.insert_image(a,b, '', {'image_data': imagedata})
   
```

In order to save the workbook images, you will need to remember to close the workbook.

```python
# close workbook to save the files
workbook.close()

```

**Steps to append data into workbook**

1. Load the workbook
2. Use pandas function to insert dataframe into worksheet 

```python
#load workbook to save the data into other worksheets
book = load_workbook('report.xlsx')
writer = pd.ExcelWriter('report.xlsx', engine='openpyxl')
writer.book = book

```

I have perform a try-except if the data is empty dataframe, I will pass to prevent throwing error if the dataframe is empty.

```python
try: 
  # writing the dataframe into excel and naming the worksheet "GWP_booking_thisyr"
    booked_ty_plt.to_excel(writer, "GWP_booking_thisyr")
except:
    pass
```

Last but not least remember to save the written data

```python
writer.save()
```

After this assessment, I understood that Python and Excel can work hand-in-hand and we could  be generating reports automatically with Python scripts like this. Anyway, there is more requirement needed for the technical assessment, I would share the second half of the assessment in another post.