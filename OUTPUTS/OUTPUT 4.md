
Question 1 
 

```c
#include‹stdio.h›
int main()
{
    struct site
    {
        char name[] = "GeeksforGeeks";
        int no_of_pages = 200;
    };
    struct site *ptr;
    printf("%d",ptr->no_of_pages);
    printf("%s",ptr->name); 
    getchar();
    return 0;
}

```
Output: 
Compiler error
Explanation: 
Note the difference between structure/union declaration and variable declaration. When you declare a structure, you actually declare a new data type suitable for your purpose. So you cannot initialize values as it is not a variable declaration but a data type declaration.
Reference: 
http://www.lix.polytechnique.fr/~liberti/public/computing/prog/c/C/SYNTAX/struct.html
Question 2 
 

```c
int main()
{
    char a[2][3][3] = {'g','e','e','k','s','f','o',
                           'r','g','e','e','k','s'};
    printf("%s ", **a);
    getchar();
    return 0;
}

```
Output: 
geeksforgeeks
Explanation: 
We have created a 3D array that should have 2*3*3 (= 18) elements, but we are initializing only 13 of them. In C when we initialize less no of elements in an array all uninitialized elements become ‘\0’ in case of char and 0 in case of integers. 
Question 3 
 

```c
int main()
{
   char str[]= "geeks\nforgeeks";
   char *ptr1, *ptr2;
      
   ptr1 = &str[3];
   ptr2 = str + 5;
   printf("%c", ++*str - --*ptr1 + *ptr2 + 2); 
   printf("%s", str); 
  
   getchar();
   return 0;
}

```
Output: 
heejs 
forgeeks
Explanation: 
Initially ptr1 points to ‘k’ and ptr2 points to ‘\n’ in “geeks\nforgeeks”. In print statement value at str is incremented by 1 and value at ptr1 is decremented by 1. So string becomes “heejs\nforgeeks” . 
First print statement becomes 
printf(“%c”, ‘h’ – ‘j’ + ‘\n’ + 2)
‘h’ – ‘j’ + ‘\n’ + 2 = -2 + ‘\n’ + 2 = ‘\n’
First print statements newline character. and next print statement prints “heejs\nforgeeks”. 
Question 4 
 

```c
#include <stdio.h>
int fun(int n)
{
    int i, j, sum = 0;
    for(i = 1;i<=n;i++)
        for(j=i;j<=i;j++)
            sum=sum+j;
    return(sum);
}
 
int main()
{
    printf("%d", fun(15));
    getchar();
    return 0;
}

```
Output: 120 
Explanation: fun(n) calculates sum of first n integers or we can say it returns n(n+1)/2.
Question 5 
 

```c
#include <stdio.h> 
int main()
{
    int c = 5, no = 1000;
    do {
        no /= c;
    } while(c--);
 
    printf ("%d\n", no);
    return 0;
}

```
Output: Exception – Divide by zero
Explanation: There is a bug in the above program. It goes inside the do-while loop for c = 0 also. Be careful when you are using do-while loop like this!!