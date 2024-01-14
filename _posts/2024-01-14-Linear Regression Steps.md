Suppose we have data number of correct answers and the attitude mark like this

(Reference and credit goes to: [Eugene O'Loughlin](https://www.youtube.com/watch?v=GhrxgbQnEEU))

| # Correct (x) | Attiitude (y) |
| --- | --- |
| 17 | 94 |
| 13 | 73 |
| 12 | 59 |
| 15 | 80 |
| 16 | 93 |
| 14 | 85 |
| 16 | 66 |
| 16 | 79 |
| 18 | 77 |
| 19 | 91 |  

Using linear regression, find the Attitude mark if the correct answer is 15  

Steps:  

(1) Find the a, which is Y-Intercept of Regression Line.

a = mean(y) - b * mean(x)  

Y-intercept is where you draw the lines between the point of slope to the y-axis 

x is an independent variable.  

the mean average of x is 17 + 13 + 12 + 15 + 16 + 14 + 16 + 16 + 18 + 19 = 156 / 10 = **15.6**  

the mean average of y ix 94 + 73 + 59 + 80 + 93 + 85 + 66 + 79 + 77 + 91 = 797 / 10 = **79.7**  

but hold on, you need to find the b value first.  
  
(2) Find the b, which isi slope of regression line  

b = r * Sy / Sx

r is Pearson correlation coefficient  
Sy is the standard deviation of y  
Sx is the standard deviation of x  

(3) Find the r, Pearson correlation coefficient  

![Pearson correlation coefficient](https://www.gstatic.com/education/formulas2/553212783/en/correlation_coefficient_formula.svg)

r = sumOf((x-mean(x)) * (y-mean(y))) / squareRootOf(sumOf((x-mean(x))^2) * sumOf((y-mean(y))^2))  

based on that, we have to find the  
(1) (x-mean(x))    
(2) (y-mean(y))  
(3) (x-mean(x)) * (y-mean(y))  and sum of all that    
(4) (x-mean(x))^2 and sum of all that  
(5) (y-mean(y))^2 and sum of all that   

for start, the first row   
17 - 15.6 = 1.4 that is (x-mean(x))  
94-79.7 = 14.3 that is (y-mean(y))  
1.4 * 14.3 = 20.02 that is (x-mean(x)) * (y-mean(y))  
1.4^2 = 1.96 that is (x-mean(x))^2  
14.3^2 = 204.49 that is (y-mean(y))^2  

and so on so forth for the rest of rows  

now we have the data like these  

| # Correct (x) | Attiitude (y) | (x-mean(x)) | (y-mean(y)) | (x-mean(x)) * (y-mean(y)) | (x-mean(x))^2 | (y-mean(y))^2 |
| --- | --- | --- | --- | --- | --- | --- |
| 17 | 94 | 1.4 | 14.3 | 20.02 | 1.96 | 204.49
| 13 | 73 | -2.6 | -6.7 | 17.42 | 6.76 | 44.89  
| 12 | 59 | -3.6 | -20.7 | 74.52 | 12.96 | 428.49  
| 15 | 80 | -0.6 | 0.3 | -0.18 | 0.36 | 0.09 
| 16 | 93 | 0.4 | 13.3 | 5.32 | 0.16 | 176.89  
| 14 | 85 | -1.6 | 5.3 | -8.48 | 2.56 | 28.09  
| 16 | 66 | 0.4 | -13.7 | -5.48 | 0.16 | 187.69
| 16 | 79 | 0.4 | -0.7 | -0.28 | 0.16 | 0.49  
| 18 | 77 | 2.4 | -2.7 | -6.48 | 5.76 | 7.29  
| 19 | 91 | 3.4 | 11.3 | 38.42 | 11.56 | 127.69   

sum or ∑ of (x-mean(x)) * (y-mean(y)) = 134.8  
sum or ∑ of (x-mean(x))^2 = 42.4  
sum or ∑ of (y-mean(y))^2 = 1206.1  

now because of. 

r = sumOf((x-mean(x)) * (y-mean(y))) / squareRootOf(sumOf((x-mean(x))^2) * sumOf((y-mean(y))^2))  

r = 134.8 / squareRootOf(42.4 * 1206.1)  

**r = 0.596**  

now we already have the r value.  Next is the standard deviations of y and x.  

the standard deviation formula is squareRootOf(sumOf((x-mean(x))^2) / m-1). 

where m is the amount of dataset we have, which is 10. 10 - 1 = 9. 

(1) Find the Sy  
squareRootOf(sumOf((y-mean(y))^2) / m-1)
= squareRootOf(1206.1 / 9)
= **11.576**  

(2) Find the Sx  
squareRootOf(sumOf((x-mean(x))^2) / m-1) 
= squareRootOf(42.4/9). 
= **2.171 ** 

Alright, we are now ready to put it to the formula b = r * Sy / Sx  

b = 0.596 * 11.576 / 2.171  
b = 0.596 * 5.332  
b = **3.178**  

ok, now we can go back to formula of y-intercept  

a = mean(y) - b * mean(x)  
a = 79.7 - 3.178 * 15.6  
a = 79.7 - 49.577  
a = **30.123**

(3) Work with the Linear Regression Function

y = a + bx
y = 30.123 + 3.178 * x

the x is 15.  
so  
y = 30.123 + 3.178 * 15.  
y = 30.123 + 47.67  
**y = 77.803**
