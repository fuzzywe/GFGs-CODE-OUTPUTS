Question 1 



```
#include <stdio.h>
int main()
{
  printf("%p", main);
  getchar();
  return 0;
}
Output: Address of function main. 
Explanation: Name of the function is actually a pointer variable to the function and prints the address of the function. Symbol table is implemented like this. 

struct 
{
   char *name;
   int (*funcptr)();
}
symtab[] = {
   "func", func,
   "anotherfunc", anotherfunc,
};
```
Question 2  



```c
#include <stdio.h>
int main()
{
   printf("\new_c_question\by");
   printf("\rgeeksforgeeks");
 
   getchar();
   return 0;
}
```
Output: geeksforgeeks 
Explanation: First printf prints “ew_c_questioy”. Second printf has \r in it so it goes back to start of the line and starts printing characters.
Now try to print following without using any of the escape characters. 

new c questions by
geeksforgeeks
Question 3  


```c

# include<stdio.h>
# include<stdlib.h>
 
void fun(int *a)
{
    a = (int*)malloc(sizeof(int));
}
 
int main()
{
    int *p;
    fun(p);
    *p = 6;
    printf("%d\n",*p);
    
    getchar();
    return(0);
}
```
It does not work. Try replacing “int *p;” with “int *p = NULL;” and it will try to dereference a null pointer.
This is because fun() makes a copy of the pointer, so when malloc() is called, it is setting the copied pointer to the memory location, not p. p is pointing to random memory before and after the call to fun(), and when you dereference it, it will crash.
If you want to add memory to a pointer from a function, you need to pass the address of the pointer (ie. double pointer).
Thanks to John Doe for providing the correct solution. For better understanding please go through the following link: https://stackoverflow.com/questions/1398307/how-can-i-allocate-memory-and-return-it-via-a-pointer-parameter-to-the-calling
Question 4 


```c

#include <stdio.h>
int main()
{
    int i;
    i = 1, 2, 3;         
    printf("i = %d\n", i);
 
    getchar();
    return 0;
}
```
Output: 1 
The above program prints 1. Associativity of comma operator is from left to right, but = operator has higher precedence than comma operator. 
Therefore the statement i = 1, 2, 3 is treated as (i = 1), 2, 3 by the compiler.
Now it should be easy to tell output of below program.


```c

#include <stdio.h>
int main()
{
    int i;
    i = (1, 2, 3);         
    printf("i  = %d\n", i);
 
    getchar();
     return 0;
}
```
Question 5 




```c
#include <stdio.h>
int main()
{
    int first = 50, second = 60, third;
    third = first /* Will this comment work? */ + second;
    printf("%d /* And this? */ \n", third);
      
    getchar();
    return 0;
}
```
Output: 110 /* And this? */ 
Explanation: Compiler removes everything between “/*” and “*/” if they are not present inside double quotes (“”).
