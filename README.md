# Decision-Support-System-Project
This project is about formulating a Business Problem and a Decision Support liner model to solve it.
The use case in this project describes a hypothetical car engine manufacturing company 
called CompanyX. CompanyX manufactures 5 types of cars engines with each having 
different characteristics and qualities. The following are the 5 engines, CompanyX makes.

1. Car Engine Model S1
2. Car Engine Model S44
3. Car Engine Model S46 
4. Car Engine Model S100
5. Car Engine Model S200

### **Problem at CompanyX**
This project focuses on maximizing the company profit from sales while considering the 
market fluctuating demands. To put it simply, we developed a linear mathematical model 
that tells CompanyX managers how much of each engine model they should manufacture 
each week to fill the market demands with the highest profit. The following tables show the 
5 models profit per 1 ton and CompanyX manufacturing capacity for each model.

|     | Car Engine Model S1 | Car Engine Model S44| Car Engine Model S46 | Car Engine Model S100 | Car Engine Model S200 | MAX |
| :---         |     :---:      |          ---: |          ---: |          ---: |          ---: |          ---:|
| Average profit of in 1 ton  | 10 mil$| 8 mil$| 9 mil$| 7.5 mil$| 8.3 mil$| 42.8 mil$|
| Number of tons produced in an hour   | 2 | 1 | 2 | 1 | 1 | 7 |

### **The Mathematical Model:**

**Variable** 
X1= Number of Car Engine Model S1 manufactured in a week in tons.
X2= Number of Car Engine Model S44 manufactured in a week in tons.
X3= Number of Car Engine Model S46 manufactured in a week in tons.
X4= Number of Car Engine Model S100 manufactured in a week in tons.
X5= Number of Car Engine Model S200 manufactured in a week in tons.

**Objective Function** 
MAX Z= (10) X1+(8)X2+(9) X3+(7.5) X4+(8.3) X5

**Constraint** 
1. Number of tons made in an hour <= 7 tons/hour.
2. Number of work hours in a week <= 40
3. How much per ton of products requested in a week >= 0 
4. How much is manufactured in tons in a week >=0 && <= how much is requested in a week.
5. The time it takes to manufacture the engines in a week must not exceed the time 
available for work which is 40 hours a week.
6. X1, X2, X3, X4, X5 >=0

### AMPL code:

`set PROD ;# products

param rate {PROD} >= 0, <=7 ;

param avail >=0,<=40;

param profit {PROD};

param market {PROD} >= 0 ;

var Make {p in PROD} >= 0, <= market[p];

maximize Z: sum {p in PROD} profit[p] * Make[p] ;

subject to Time: sum {p in PROD} (1/rate[p]) * Make[p] <= avail ;

 

data;

set PROD := X1 X2 X3 X4 X5;

param: rate profit market :=

X1 2 10 44

X2 1 8 46

X3 2 9 33

X4 1 7 45

X5 1 8 59;


param avail := 40;`

It is important to note that the rate of manufacturing and the profit for each engine is taken 
from the above table. However, the market demand for each type of engine changes from one week 
to another. For this example, we gave every one of the 5 engines the following market 
demand values in tons: x1=44, x2=46, x3=33, x4=45, and finally x5=59.

**The optimum solution after running the code:**
![image](https://user-images.githubusercontent.com/63616896/144734582-83bc2bb5-3c5b-435f-bc10-f4b2e5913509.png)
we concluded from the model that to get the maximum profit this week we only need to manufacture engines model S1, S46, and S200.

