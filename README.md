# hanaheshamm.github.io
# Fibonacci report

       Prepared by Hana Hesham, section 2, BN 45.

In this report, I am going to list many solutions to the Fibonacci sequence problem. "given an integer **n**, output the **n**th Fibonacci number" and I am going to explain the algorithm of each solution mentioning the space and time complexity.


In mathematics, the **Fibonacci numbers**, commonly denoted _Fn_, form a sequence, the **Fibonacci sequence**, in which each number is the sum of the two preceding ones.

The *Fibonacci Sequence* is the series of numbers:
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, ...


![fibonacci](https://encrypted-tbn0.gstatic.com/licensed-image?q=tbn:ANd9GcQMmZFV597hreUgTQd8o5u8z-nagQymJlnOV-erIrhMjOQoaFYzgH5_wyI&usqp=CAE&s=19)

You can also check this link for more information [Fibonacci numbers](https://en.wikipedia.org/wiki/Fibonacci_number).

 
## First solution

    #include <iostream>  
    using namespace std;  
      
    int main() {  
          
     // 0 1 1 2 3 5 8 
      int n;  
      cin >> n;  
      long long *arr = new long long(n+2);  
      for(int i=2 ; i<n+2 ; i++)  
        {  
            arr[0]=0;  
            arr[1]=1;  
            arr[i] = arr[i-1] + arr[i-2];  
         }  
        
      cout << arr[n];  
      //   delete [] arr;  
      
      return 0;  
    }

 - **Time complexity**: O(n) for given n
   
 - **Auxiliary space**: O(n)

*In this solution we used the property that **Fn  = F(n−1)  + F(n−2)*** 

## Second solution

    #include <iostream>  
    #include "bits/stdc++.h"  
    using namespace std;  
      
      
    int main() {  
      double n;  
      cin >> n;    
      double up =(( pow(1.618034 ,n) ) - (pow((1-1.618034) , n) ) ) ;  
      
      cout << ((up)/ sqrt(5)) ;  
      return 0;  
    }
    

 - **Time complexity**: O(1) 
   
 - **Auxiliary space**: O(1)

   *In this solution we used the golden rule method to get the Fibonacci number*

## Third solution

 

    #include <bits/stdc++.h>  
    using namespace std;  
      
    int fib(int n)  
    {  
       if (n <= 1)  
          return n;  
      return fib(n - 1) + fib(n - 2);  
    }  
      
    int main()  
    {  
      int n;  
      cin>>n;  
      cout << fib(n);  
      return 0;  
    }
        
      

 - **Time Complexity:** Exponential ( as every function calls two other functions.)
 - **Auxiliary space:** O(1)

   *In this solution, we used recursion to get the Fibonacci number*


## Fourth solution

    
    #include<bits/stdc++.h>
    using namespace std;
    
    int fib(int n)
    {
    	int a = 0, b = 1, c, i;
    	if( n == 0)
    		return a;
    	for(i = 2; i <= n; i++)
    	{
    	c = a + b;
    	a = b;
    	b = c;
    	}
    	return b;
    }
    
    // Driver code
    int main()
    {
    	int n;
    	cin>>n;
    	
    	cout << fib(n);
    	return 0;
    }
    

 - **Time Complexity:**  O(n)
 - **Auxiliary space:**  O(1)

   *In this solution, we can optimize the space used in the first solution by only storing the previous two numbers because that is all we need to get the next Fibonacci number in series.*

## Fifth solution

    #include<bits/stdc++.h>
    using namespace std;
    
    void multiply(int F[2][2], int M[2][2]);
    void power(int F[2][2], int n);
    
    int fib(int n)
    {
    	int F[2][2] = { { 1, 1 }, { 1, 0 } };
    	if (n == 0)
    		return 0;
    	power(F, n - 1);
    	return F[0][0];
    }
    
    void multiply(int F[2][2], int M[2][2])
    {
    	int x = F[0][0] * M[0][0] +
    			F[0][1] * M[1][0];
    	int y = F[0][0] * M[0][1] +
    			F[0][1] * M[1][1];
    	int z = F[1][0] * M[0][0] +
    			F[1][1] * M[1][0];
    	int w = F[1][0] * M[0][1] +
    			F[1][1] * M[1][1];
    	
    	F[0][0] = x;
    	F[0][1] = y;
    	F[1][0] = z;
    	F[1][1] = w;
    }
    
    void power(int F[2][2], int n)
    {
    	int i;
    	int M[2][2] = { { 1, 1 }, { 1, 0 } };
    	
    	// n - 1 times multiply the
    	// matrix to {{1,0},{0,1}}
    	for(i = 2; i <= n; i++)
    		multiply(F, M);
    }
    
    int main()
    {
    	int n;
    	cin>>n;
    	
    	cout << fib(n);
    	
    	return 0;
    }

 - **Time Complexity:** O(n)
 - **Auxiliary space:** O(1)

   *This solution relies on the fact that if we n times multiply the matrix M = {{1,1},{1,0}} to itself (in other words calculate power(M, n)), then we get the (n+1)th Fibonacci number as the element at row and column (0, 0) in the resultant matrix.*

## Sixth solution

    #include <bits/stdc++.h>
    using namespace std;
    
    void multiply(int F[2][2], int M[2][2]);
    void power(int F[2][2], int n);
    
    // Function that returns nth Fibonacci number
    int fib(int n)
    {
    	int F[2][2] = {{1, 1}, {1, 0}};
    	if (n == 0)
    		return 0;
    	power(F, n - 1);
    
    	return F[0][0];
    }
    
    void power(int F[2][2], int n)
    {
    	if(n == 0 || n == 1)
    	return;
    	int M[2][2] = {{1, 1}, {1, 0}};
    	
    	power(F, n / 2);
    	multiply(F, F);
    	
    	if (n % 2 != 0)
    		multiply(F, M);
    }
    
    void multiply(int F[2][2], int M[2][2])
    {
    	int x = F[0][0] * M[0][0] + F[0][1] * M[1][0];
    	int y = F[0][0] * M[0][1] + F[0][1] * M[1][1];
    	int z = F[1][0] * M[0][0] + F[1][1] * M[1][0];
    	int w = F[1][0] * M[0][1] + F[1][1] * M[1][1];
    	
    	F[0][0] = x;
    	F[0][1] = y;
    	F[1][0] = z;
    	F[1][1] = w;
    }
    
    int main()
    {
    	int n ;
    	cin >>n;
    	
    	cout << fib(9);
    	getchar();
    	
    	return 0;
    }
 

 - **Time Complexity:**  O(Log n)
 - **Extra Space:** O(Log n)
 
   *In this solution, we optimized the fifth solution to work in O(Log n) time complexity by doing recursive multiplication to get power(M, n)*
   
## Seventh solution

    #include<iostream>
    #include<cmath>
    using namespace std;
    
    int fib(int n) {
    double phi = (1 + sqrt(5)) / 2;
    return round(pow(phi, n) / sqrt(5));
    }
    
    int main ()
    {
    int n;
    cin >>n;
    cout << fib(n);
    return 0;
    }

 - **Time Complexity**_**:**_ O(logn), this is because calculating phi^n takes log n time

 - **Auxiliary Space**_**:**_ O(1)
 
   *In this solution, we directly implement the formula for the nth term in the Fibonacci series.  :  Fn = {[(√5 + 1)/2] ^ n} / √5*
   

## The following table compares between them:

|         | First | Second | Third | Forth | Fifth | Sixth | Seventh 
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Time Complexity | O(n) | O(1) | O(2^n) |O(n) | O(n) | O(logn) | O(logn) | 
|Auxiliary Space | O(n) | O(1) | O(1) | O(1) | O(1) | O(1) | O(1) |


 

 

 
