Microsoft Excel OR LibreOffice Calc are excellent tools for data cleaning. For small to moderate level tasks, I always use LibreOffice Calc but very time I use Calc functions, I have to search for functions as I cannot remember functions names or parameters. Thus this blog

Some interesting functions 

### 1. Relplace/Remove unwanted characters
Ctrl+H is for find and replace, I use it all the time to remove special characters (end of line chearacter), spaces etc


### 2. Multiple data fields in one column.
Multiple fields in one column and I want them to be separated in multiple column

Example:
I have test "Alex 30years" in column A1 and as you can see these should be in two columns Name and age .I want any thing after first space to be in B1.

Now, will go to column B1 and paste the following

~~~
=MID( A1,FIND(" ",A1)+1,100)
~~~

> Explanation:

> * FIND("character",cell_number) will find and return the location of given cheracter.

> * MID(cell_number) will extract substring from cell A1 and the substring will start from the location returned by FIND() function till 100th character (yes we can use lenth function instead of static number like 100)


### 3. sting concatenation
Have you seen a case where you have two or more columns and you want to generate a new column based on available columns. The colution is CONCATINATE() function. Here how it works

Example:
There are four columns with data

![Alt](https://scriptndebug.files.wordpress.com/2016/12/concatinate.png "CONCATINATE")

Now you want to column E to appear like "abc to z". Click on cell/column D1 and use the following command

~~~
=CONCATENATE(A1,B1,C1," to ", D1)
~~~

I think its self explanatory :). This Example is not very interting so lets look at an interesting exmaple.

Suppose you have four pairs of latitudes/longitudes (a bounding box, see the image below) in columns and you want to make a csv which can be imported into qGIS in such a way that the columns becomes geometry.

![Alt](https://scriptndebug.files.wordpress.com/2016/12/concatinate_2.png "CONCATINATE 2")
We can generate a geometry column containing Well Known Text (WKT) by concatinating pairs of lat/long. Any GIS software that supports WKT will generate shapes based on this column.


![Alt](https://scriptndebug.files.wordpress.com/2016/12/concatinate_3.png "CONCATINATE 3")
and the code to generate wkt column is

~~~
=CONCATENATE("POLYGON ((",A2," ", B2,",",A2," ",C2,",",C2," ",D2,",",D2," ",B2,",",B2," ", A2,"))")
~~~

Save this exel sheet as csv and import in qGIS (by using layer - csv option). If every thing goes well, you will see a bolygon layer (like the one below)

![Alt](https://scriptndebug.files.wordpress.com/2016/12/concatinate_4.png "CONCATINATE 4")

Now if you have many rows, you can replicate the formula (by dragging it) on other columns.
