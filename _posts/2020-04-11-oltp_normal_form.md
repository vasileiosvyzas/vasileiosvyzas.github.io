---
title: "Normal Form notes"
date: 2020-04-11
tags: [oltp, normal form, db]
---


# What is Normalization?
In database design, normalization is the process of separating and organizing the records in tables in a way that reduces redundancy and dependency of data. It basically, divides larger tables to smaller tables and links them using relationships. Edgar Codd defined normalization in the form of some rules:

![alt text](/images/oltp/normalisation.png)

## 1st Normal Form
![alt text](/images/oltp/normal_form1.png)

When a table is in its first normal form, searching, filtering and sorting information is easier. The rules to satisfy the 1st normal form are:
- When the data is in a database table.  The table stores information in rows and columns where one or more columns, called the primary key, uniquely identify each row.
- Each column contains atomic values, and should be not repeating groups of columns.

Tables cannot contain sub-columns in the first normal form. That is, you cannot list multiple cities in one column and separate them with a semi-colon. Questions that should be answered at this stage:
- Are there any repeating groups?
- Does each table cell have a single value?
- Is each record unique?

## 2nd Normal Form
![alt text](/images/oltp/normal_form2.png)

The goal is to break down each entity and narrow them to a single purpose that make it easier to describe and use a table.  In second normal form, each table should be a separate standalone entity where the primary key is the main focus point and the non-key columns depend on the primary key.

The second normal form is defined by two rules:
- The table should be in 1st normal form
- There must be a single column which is the primary key and the non-key columns are dependent on the table’s primary key.

Related to the second normal form is the foreign key. When we define the primary key for a single table we can then use it as a reference point on another table. This reference is called the foreign key and it helps connect your tables by having the values of the primary key. The principles for the foreign key are:
- A foreign key can have a different name from its primary key
- It ensures rows in one table have corresponding rows in another
- Unlike the primary key, they don’t have to be unique. Most often they aren’t
- Foreign keys can be null even though primary keys can not

Questions that should be answered when converting a table in 2nd normal form:
- Is each non-key attribute determined by the whole of the multi-part primary key, or only by some subset of it?  
- Does each column in the table serve to describe what the primary key identifies?

## 3rd Normal Form
![alt text](/images/oltp/normal_form3.png)

Once a table is in second normal form, we are guaranteed that every column is dependent on the primary key, or as I like to say, the table serves a single purpose.  But what about relationships among the columns?  Could there be dependencies between columns that could cause an inconsistency when updating and inserting new records?
The rules for 3rd normal form are:
    • Be in 2NF
    • It contains only columns that are non-transitively dependent on the primary key
To be non-transitively dependent on the primary key means that one and only one column in the table has to be dependent on the primary key. If a column’s value relies on another column through an intermediate column then that breaks 3rd NF. Examples of that could be:

<html>
<head>
	
	<meta http-equiv="content-type" content="text/html; charset=utf-8"/>
	<title></title>
	<meta name="generator" content="LibreOffice 6.1.6.3 (Linux)"/>
	<meta name="created" content="2020-04-11T15:41:05.912812284"/>
	<meta name="changed" content="2020-04-11T16:07:36.035571121"/>
	
	<style type="text/css">
		body,div,table,thead,tbody,tfoot,tr,th,td,p { font-family:"Liberation Sans"; font-size:x-small }
		a.comment-indicator:hover + comment { background:#ffd; position:absolute; display:block; border:1px solid black; padding:0.5em;  } 
		a.comment-indicator { background:red; display:inline-block; border:1px solid black; width:0.5em; height:0.5em;  } 
		comment { display:none;  } 
	</style>
	
</head>

<body>
<table cellspacing="0" border="0">
	<colgroup span="4" width="85"></colgroup>
	<tr>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" height="20" align="left"><b><font face="Calibri" size=3>Primary Key (PK)</font></b></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="left"><b><font face="Calibri" size=3>Column A</font></b></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="left"><b><font face="Calibri" size=3>Column B</font></b></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="left"><b><font face="Calibri" size=3>Transitive Dependence?</font></b></td>
	</tr>
	<tr>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" height="20" align="left"><font face="Calibri" size=3>PersonID</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="left"><font face="Calibri" size=3>FirstName</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="left"><font face="Calibri" size=3>LastName</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="left"><font face="Calibri" size=3>No, In Western cultures a person’s last name is based on their father’s LastName, whereas their FirstName is given to them.</font></td>
	</tr>
	<tr>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" height="20" align="left"><font face="Calibri" size=3>PersonID</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="left"><font face="Calibri" size=3>BodyMassIndex</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="left"><font face="Calibri" size=3>IsOverweight</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="left"><font face="Calibri" size=3>Yes, &nbsp;BMI over 25&nbsp;is considered overweight. It wouldn’t make sense to have the value IsOverweight be true when the BodyMassIndex was &lt; 25.</font></td>
	</tr>
	<tr>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" height="20" align="left"><font face="Calibri" size=3>PersonID</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="left"><font face="Calibri" size=3>Weight</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="left"><font face="Calibri" size=3>Sex</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="left"><font face="Calibri" size=3>No:There is no direct link between the weight of a person and their sex.</font></td>
	</tr>
	<tr>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" height="20" align="left"><font face="Calibri" size=3>VehicleID</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="left"><font face="Calibri" size=3>Model</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="left"><font face="Calibri" size=3>Manufacturer</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="left"><font face="Calibri" size=3>Yes:Manufacturers make specific models.&nbsp; For instance, Ford creates the Fiesta; whereas, Toyota manufacturers the Camry.</font></td>
	</tr>
</table>
<!-- ************************************************************************** -->
</body>

</html>

Questions to ask at this stage:
- Is each non-key attribute in a relation depended directly on the primary key? Does it depend on another non-key attribute in the relation?
- Is there a relationship among the columns?
- Could there be dependency between columns that could cause an inconsistency?

## Boyce-Codd Normal Form (BCNF) or 3.5 Normal Form
Boyce-Codd Normal Form is a stricter version of 3NF which also deals with anomalies in the data. A table is considered to be in BCNF if all redundancy based on functional dependency has been removed. BCNF acts differently from 3NF only when there are multiple overlapping candidate keys. For a table to satisfy the Boyce-Codd Normal Form, it should satisfy the following two conditions:
1. It should be in the Third Normal Form.
2. And, for any dependency A → B, A should be a super key. A super key is basically a set of columns such that the value of that set of columns is unique across various rows. This basically means that no two rows have the same set of values for those columns.

For example:
<html>
<head>
	
	<meta http-equiv="content-type" content="text/html; charset=utf-8"/>
	<title></title>
	<meta name="generator" content="LibreOffice 6.1.6.3 (Linux)"/>
	<meta name="created" content="2020-04-11T16:11:21.081094452"/>
	<meta name="changed" content="2020-04-11T16:11:40.834624901"/>
	
	<style type="text/css">
		body,div,table,thead,tbody,tfoot,tr,th,td,p { font-family:"Liberation Sans"; font-size:x-small }
		a.comment-indicator:hover + comment { background:#ffd; position:absolute; display:block; border:1px solid black; padding:0.5em;  } 
		a.comment-indicator { background:red; display:inline-block; border:1px solid black; width:0.5em; height:0.5em;  } 
		comment { display:none;  } 
	</style>
	
</head>

<body>
<table cellspacing="0" border="0">
	<colgroup span="3" width="85"></colgroup>
	<tr>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" height="20" align="center"><b><font face="Calibri" size=3>student_id</font></b></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="center"><b><font face="Calibri" size=3>subject</font></b></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="center"><b><font face="Calibri" size=3>professor</font></b></td>
	</tr>
	<tr>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" height="20" align="center" sdval="101" sdnum="1033;"><font face="Calibri" size=3>101</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="center"><font face="Calibri" size=3>Java</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="center"><font face="Calibri" size=3>P.Java</font></td>
	</tr>
	<tr>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" height="20" align="center" sdval="101" sdnum="1033;"><font face="Calibri" size=3>101</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="center"><font face="Calibri" size=3>C++</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="center"><font face="Calibri" size=3>P.Cpp</font></td>
	</tr>
	<tr>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" height="20" align="center" sdval="102" sdnum="1033;"><font face="Calibri" size=3>102</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="center"><font face="Calibri" size=3>Java</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="center"><font face="Calibri" size=3>P.Java2</font></td>
	</tr>
	<tr>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" height="20" align="center" sdval="103" sdnum="1033;"><font face="Calibri" size=3>103</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="center"><font face="Calibri" size=3>C#</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="center"><font face="Calibri" size=3>P.Chash</font></td>
	</tr>
	<tr>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" height="20" align="center" sdval="104" sdnum="1033;"><font face="Calibri" size=3>104</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="center"><font face="Calibri" size=3>Java</font></td>
		<td style="border-top: 1px solid #000000; border-bottom: 1px solid #000000; border-left: 1px solid #000000; border-right: 1px solid #000000" align="center"><font face="Calibri" size=3>P.Java</font></td>
	</tr>
</table>
<!-- ************************************************************************** -->
</body>

</html>


In the table above:
- One student can enrol for multiple subjects. For example, student with student_id 101, has opted for subjects: Java & C++
- For each subject, a professor is assigned to the student.
- And, there can be multiple professors teaching one subject like we have for Java.

In the table above student_id, subject together form the primary key, because using student_id and subject, we can find all the columns of the table. One more important point to note here is, one professor teaches only one subject, but one subject may have two different professors. Hence, there is a dependency between subject and professor here, where subject depends on the professor name.

student_id, subject form primary key, which means subject column is a prime attribute.
But, there is one more dependency, professor → subject.
And while subject is a prime attribute, professor is a non-prime attribute, which is not allowed by BCNF.

**Student Table**

|student_id| p_id|
|---|:---:|
|101 | 1|
|101|  2|


**Professor Table**

|p_id| professor| subject|
|---|:---:|:---|
|1 |P.Java| Java|
|2 |P.Cpp| C++|


## 4th Normal Form
The 4th normal form is the next level of normalisation after BCNF which deals with mutli-valued dependency.  The goal, like the other normal forms, is to organize the data and eliminate anomalies and redundancy. The conditions for the 4NF are:
- The table should be in BCNF
- There should be no Multi-valued dependency

Conditions for multivalued dependency:
1. There should be at least 3 columns in a table
2. For every dependency A->B, for every value of A multiple values of B exists then the dependency is referred to as multi-valued dependency.
3. In the relation of 3 columns R(XYZ), if there exists a multi-valued dependency between X and Y then the Y and Z should be independent of each other.

**Example**

|Student_Roll_No| Subject_Enrolled |Activity_Enrolled|
|---|:---:|:---|
|45| Economics| Painting|
|45| History| Hockey|
|33| Physics| Drawing|
|59| Chemistry| Singing|
|40| Python| Journalism|

Checking for multi-valued dependency in the table above:
1. There are at least 3 columns in the table. The dependencies are:
Student_Roll_No -> Subject_Enrolled
Student_Roll_No -> Activity_Enrolled
2. For every dependency A-> B, for every value of A multiple values of B exists then the dependency is referred to as multi-valued dependency. – – Roll no 45 has enrolled in Economics and History in terms of academics and Painting and Hockey as activities. Thus for a value of Student_Roll_No different values of Activity_Enrolled exist.
3. In the relation of 3 columns R(XYZ), if there exists a multi-valued dependency between X and Y then Y and Z should be independent of each other. – – Subject_Enrolled and Activity Enrolled are independent of each other.

Since it’s clear that there is a multi-valued dependency, the above table can be decomposed into:

|Student_Roll_No |Subject_Enrolled|
|---|:---:|
|45 |Economics|
|45 |History|
|33 |Physics|
|59 |Chemistry|
|40 |Python|


## Fifth Normal Form
A relation R is in 5NF if and only if every join dependency in R is implied by the candidate keys of R. A relation decomposed into two relations must have loss-less join property, which basically means that when you decompose a relation R into R1, R2 relations, then the union of those 2 (or more) decomposed relations should give you back your original relation.

The conditions for 5NF are:
- The table should be in 4NF
- It cannot be further non loss decomposed (join dependency)

**Example**

|AGENT| COMPANY| PRODUCT|
|---|:---:|:---|
|A1| PQR| Nut|
|A1| PQR |Bolt|
|A1| XYZ| Nut|
|A1| XYZ| Bolt|
|A2 |PQR |Nut|

The above relation can be decomposed into the following 3 relations where the result of Natural Join of R1 and R3 over ‘Company’ and then Natural Join of R1, R3 and R2 over ‘Agent’and ‘Product’ will be table ACP.

**Table R1**

|AGENT| COMPANY|
|---|:---:|
|A1| PQR|
|A1| XYZ|
|A2| PQR|

**Table R2**

|AGENT| Product|
|---|:---:|
|A1| Nut|
|A1| Bolt|
|A2| Nut|

**Table R3**

|COMPANY |PRODUCT|
|---|:---:|
|PQR |Nut|
|PQR |Bolt|
|XYZ |Nut|
|XYZ |Bolt|


