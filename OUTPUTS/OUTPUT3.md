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

Your code has a potential issue related to the handling of pointers, specifically in the fun() function, and this can lead to undefined behavior.

Explanation of Code:

#include<stdio.h>
#include<stdlib.h>

void fun(int *a)
{
    a = (int*)malloc(sizeof(int));  // Allocating memory for a new integer
}

int main()
{
    int *p;
    fun(p);  // Passing the pointer to the function
    *p = 6;  // Dereferencing the pointer and assigning a value
    printf("%d\n", *p);  // Printing the value of the dereferenced pointer
    
    getchar();
    return 0;
}

Problems in the Code:

1. Uninitialized Pointer p: In the main() function, you declare the pointer p but do not initialize it:

int *p;

Since p is not initialized, it points to some random memory address (a garbage value). Dereferencing an uninitialized pointer leads to undefined behavior.


2. The fun() Function Doesn't Modify the Original Pointer: In the function fun(), you're passing the pointer p by value:

void fun(int *a)

Inside fun(), you're allocating memory for a using malloc, but this change only affects the local copy of the pointer a. The original pointer p in the main() function is not modified. Therefore, after fun() is called, p in main() still points to the garbage value (uninitialized memory).

a = (int*)malloc(sizeof(int));  // Allocating new memory, but it won't affect 'p' in main


3. Dereferencing p after fun() Call: After the fun() call, p still points to invalid memory. Dereferencing p with:

*p = 6;

leads to undefined behavior, as p hasn't been properly initialized or modified to point to valid, allocated memory.



How to Fix the Code:

1. Initialize p Properly in main():
You should either allocate memory for p before passing it to fun(), or pass a pointer to pointer (int **) to modify the original pointer in main().


2. Fix the fun() Function:
Modify fun() to either return a pointer or use a pointer-to-pointer to directly modify the memory location of p in main().



Corrected Code:

Option 1: Using malloc in main():

#include<stdio.h>
#include<stdlib.h>

void fun(int *a)
{
    // You can assign to 'a' here, but it won't affect 'p' in main
    // a = (int*)malloc(sizeof(int));  // This won't modify 'p' in main.
}

int main()
{
    int *p = (int*)malloc(sizeof(int));  // Properly allocate memory for 'p'
    if (p == NULL) {
        printf("Memory allocation failed.\n");
        return 1;
    }
    fun(p);  // Pass 'p' to 'fun'
    *p = 6;  // Now this is valid since 'p' points to allocated memory
    printf("%d\n", *p);  // Prints 6
    
    free(p);  // Don't forget to free the memory
    getchar();
    return 0;
}

Option 2: Using Pointer to Pointer in fun():

#include<stdio.h>
#include<stdlib.h>

void fun(int **a)
{
    *a = (int*)malloc(sizeof(int));  // Allocate memory for the pointer that 'a' points to
}

int main()
{
    int *p = NULL;  // Initialize 'p' to NULL
    fun(&p);  // Pass the address of 'p' to 'fun'
    *p = 6;  // Now 'p' points to valid memory
    printf("%d\n", *p);  // Prints 6
    
    free(p);  // Don't forget to free the memory
    getchar();
    return 0;
}

Summary:

The problem in your code is that p was uninitialized, and fun() was not modifying the original pointer p due to passing it by value.

Properly initialize p in main() and either pass it to fun() in a way that allows modification (such as by pointer-to-pointer or direct memory allocation in main()).

Don't forget to free any dynamically allocated memory to avoid memory leaks.










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
