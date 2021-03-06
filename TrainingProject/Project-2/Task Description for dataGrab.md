Task Description for Project dataGrab
========================================================

*October 15, 2014*

The main task of this project is to grab data from websites. To be more specific, we have already known 4 data sources containing the historical data of Chinese future market, and we need to grab the data and write all of them to a database using R. 

The information needed for this task will be given firstly. Then the latter part will be about the detailed requirements of this task. Some additional hints are given in the last part. In the future, more hints will be given if they are needed. These hints will be more and more specific but also lower the difficuilty level of this task. Try to use less hints and try to develop the ability to solve the problems by yourself.

# Given Information

## Data Source

Four data sources have already been explored and ready to be used. You can explore them and get a good idea about the data structure. 

### SHFE(������):

http://www.shfe.com.cn/statements/delaymarket_all.html

http://www.shfe.com.cn/data/dailydata/kx/kx20140924.dat

### DCE(������):

http://quote.dce.com.cn/data/quoteAll.xml

http://www.dce.com.cn/PublicWeb/MainServlet?action=Pu00012_download&Pu00011_Input.trade_date=20140923&Pu00011_Input.variety=all&Pu00011_Input.trade_type=0&Submit2=%CF%C2%D4%D8%CE%C4%B1%BE%B8%F1%CA%BD

http://quote.dce.com.cn/quote/index_blue4.html

*��Ӣת����ϵ�� var keys = new Array("a","b","m","y","c","p","jd","fb","bb","l","v","j","jm","i","pp");*

*var values = new Array("��һ","����","����","����","����","�����","����","��ά��","���ϰ�","����ϩ","������ϩ","��̿","��ú","����ʯ","�۱�ϩ")*

### CZCE(֣����)��

http://www.czce.com.cn/portal/exchange/2014/quotation/20140930.htm

http://www.czce.com.cn/portal/exchange/2014/datadaily/20140930.txt

### CFFEX(�н���):

http://www.cffex.com.cn/fzjy/mrhq/201409/30/index.xml

## Solutions for Reading Data

Notice the data from SHFE and CFFEX might be hard to be read directly, since their file types are not usual data file types (like .txt and .csv). The solutions are provided for these two data sources, and we can use direct ways like readLines() and read.csv() to read in the other two data sources.

### SHFE:


```r
dat <- readLines(con = "http://www.shfe.com.cn/data/dailydata/kx/kx20140930.dat",encoding = "UTF-8") 

js <- jsonlite::fromJSON(dat) 
```

### CFFEX:


```r
xml <- XML::xmlParse("http://www.cffex.com.cn/fzjy/mrhq/201409/30/index.xml",isURL = T) 

dt <- XML::xmlToDataFrame(xml,stringsAsFactors = F)
```

# Tasks

As has mentioned, the main task of this project is to grab the data and write them into a database. You are asked to do the following jobs to finish the task:

## Functions for Getting Data:

Functions should be written to grab the data and transform them to a proper format. You can write four functions to do this, one data source with one function. The argument of each function should be a date, and the return should be the cleared data.

## Write the Grabbed Data into A Database:

Call the functions written in the first step, and write the cleared data into a database. 

You have two choices to do so. The first is do not overly transform the data in order to avoid mistakes and information loss, and write the data into four tables. The second is transform four data sets in a standard way, and write them into a single table.

## Data Accumulation Function

A function used to grab today's data. That is, when we run this function, we can obtain today's data from four data sources, and write them into the existed database.
