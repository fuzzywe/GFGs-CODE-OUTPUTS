```c
#include<stdio.h>
int main()
{
	static int i=5;
	if(--i){
		main();
		printf("%d ",i);
	} 
}
```

Let me explain it even more clearly with a detailed visual step-by-step walkthrough, showing the call stack, the value of `i` at each step, and how the recursive calls are made and unwound.

### Initial Understanding:
- The program uses **recursion** to call the `main()` function multiple times.
- **Static Variable `i`** retains its value across all function calls, which is critical to understand the output.
- The variable `i` starts with the value `5`, and it's decremented in each call until it reaches `0`.

---

### Initial Setup:
```c
int main() {
    static int i = 5;  // Step 1: 'i' is initialized to 5 (once due to 'static').
    if (--i) {         // Step 2: Decrement 'i' by 1, then check if 'i' is non-zero.
        main();        // Step 3: Recursively call 'main()' if 'i' is non-zero.
        printf("%d ", i);  // Step 4: Print the value of 'i'.
    }
}
```

---

### **Step-by-Step Execution**:

1. **First Call to `main()`** (Initial `i = 5`):
   - `static int i = 5;` → This is the first time `i` is initialized. 
   - `--i;` → `i` is decremented from `5` to `4`.
   - Since `i = 4` (non-zero), the program **calls `main()` recursively**.

   **Call Stack**:
   ```
   main() [i = 4]
   ```

---

2. **Second Call to `main()`** (Now `i = 4`):
   - `static int i;` → `i` remains `4` from the first call because it's static.
   - `--i;` → `i` is decremented from `4` to `3`.
   - Since `i = 3` (non-zero), the program **calls `main()` recursively** again.

   **Call Stack**:
   ```
   main() [i = 3]  <--- Second call
   main() [i = 4]  <--- First call
   ```

---

3. **Third Call to `main()`** (Now `i = 3`):
   - `static int i;` → `i` remains `3`.
   - `--i;` → `i` is decremented from `3` to `2`.
   - Since `i = 2` (non-zero), the program **calls `main()` recursively** again.

   **Call Stack**:
   ```
   main() [i = 2]  <--- Third call
   main() [i = 3]  <--- Second call
   main() [i = 4]  <--- First call
   ```

---

4. **Fourth Call to `main()`** (Now `i = 2`):
   - `static int i;` → `i` remains `2`.
   - `--i;` → `i` is decremented from `2` to `1`.
   - Since `i = 1` (non-zero), the program **calls `main()` recursively** again.

   **Call Stack**:
   ```
   main() [i = 1]  <--- Fourth call
   main() [i = 2]  <--- Third call
   main() [i = 3]  <--- Second call
   main() [i = 4]  <--- First call
   ```

---

5. **Fifth Call to `main()`** (Now `i = 1`):
   - `static int i;` → `i` remains `1`.
   - `--i;` → `i` is decremented from `1` to `0`.
   - Since `i = 0`, the condition `if (--i)` becomes `false`, so the program does **not** call `main()` again.
   - No recursive call happens, and the recursion stops here.

   **Call Stack**:
   ```
   main() [i = 0]  <--- Fifth call (no more recursion)
   main() [i = 1]  <--- Fourth call
   main() [i = 2]  <--- Third call
   main() [i = 3]  <--- Second call
   main() [i = 4]  <--- First call
   ```

---

### **Recursion Stops – Now Unwinding Begins**:
At this point, the recursion has stopped. Now, the program will **unwind** the recursive calls, printing the value of `i` in **reverse order**.

1. **Fifth Call Unwinds (i = 0)**:
   - After recursion stops, the `printf("%d ", i);` statement in the fifth call executes.
   - `i = 0` (since `i` was decremented to `0` in the last step).
   - The program prints:
     ```
     0
     ```

   **Call Stack** (after printing):
   ```
   main() [i = 1]  <--- Fourth call
   main() [i = 2]  <--- Third call
   main() [i = 3]  <--- Second call
   main() [i = 4]  <--- First call
   ```

---

2. **Fourth Call Unwinds (i = 0)**:
   - Control returns to the fourth call, where `i` was `1` before the recursion.
   - Now, `i = 0` (since `i` is static and retains its value from the previous call).
   - The program prints:
     ```
     0
     ```

   **Call Stack** (after printing):
   ```
   main() [i = 2]  <--- Third call
   main() [i = 3]  <--- Second call
   main() [i = 4]  <--- First call
   ```

---

3. **Third Call Unwinds (i = 0)**:
   - Control returns to the third call, where `i` was `2` before the recursion.
   - Now, `i = 0`.
   - The program prints:
     ```
     0
     ```

   **Call Stack** (after printing):
   ```
   main() [i = 3]  <--- Second call
   main() [i = 4]  <--- First call
   ```

---

4. **Second Call Unwinds (i = 0)**:
   - Control returns to the second call, where `i` was `3` before the recursion.
   - Now, `i = 0`.
   - The program prints:
     ```
     0
     ```

   **Call Stack** (after printing):
   ```
   main() [i = 4]  <--- First call
   ```

---

5. **First Call Unwinds (i = 0)**:
   - Control returns to the first call, where `i` was `4` before the recursion.
   - Now, `i = 0`.
   - The program prints:
     ```
     0
     ```

---

### **Final Output**:
After all recursive calls unwind, the final output is:
```
0 0 0 0
```

### Key Points:
- The variable `i` is **static**, so it retains its value across recursive calls.
- After recursion stops at `i = 0`, all previous recursive calls print `0` during the unwinding process because `i` remains `0`.
- Each function call prints the value of `i` after it finishes the recursion, which explains why we see four `0`s in the output.

---

Does this detailed explanation with visuals and a step-by-step call stack make it clearer now? Let me know if you need further clarification!

0 0 0 0 

=== Code Execution Successful ===

```c
#include<stdio.h>
int main()
{
	static int var = 5;
	printf("%d ",var--);
	if(var)
		main();				 
}
```
Output
5 4 3 2 1 
 
Explanation: Same as previous question. The only difference here is, sequence of calling main and printf is changed, therefore different output.
Question 4 
  ```c
#include<stdio.h>
int main()
{
    int x;
    printf("%d",scanf("%d",&x)); 
    /* Suppose that input value given 
        for above scanf is 20 */
    return 1;
} 
Output
1
scanf returns the no. of inputs it has successfully read.
```
The `%d` format specifier in C is crucial for several reasons, particularly when working with functions like `printf` and `scanf`. Let’s break down its significance in the context of both functions:

### 1. **Purpose of `%d` in `scanf`**

- **Input Specification**: When you use `scanf` with the format specifier `%d`, you are telling the function to expect an integer input from the user. This informs `scanf` to interpret the input characters as a decimal integer.
  
  ```c
  scanf("%d", &x);
  ```

- **Memory Storage**: The `%d` format specifier indicates that the function should convert the input to an integer and store it at the memory location pointed to by `&x`. Without `%d`, `scanf` wouldn’t know how to interpret the user’s input.

- **Error Handling**: If the input provided by the user cannot be converted to an integer, `scanf` will not successfully read a value, returning `0`. This allows you to implement error handling based on the return value of `scanf`.

### 2. **Purpose of `%d` in `printf`**

- **Output Formatting**: When you use `printf` with `%d`, you specify that you want to print an integer value. This tells `printf` to format the variable you are passing as a decimal integer in the output.

  ```c
  printf("%d", x);
  ```

- **Data Representation**: The `%d` specifier ensures that the integer is printed in the correct format. If you were to use a different format specifier (like `%f` for floats or `%s` for strings), it would lead to undefined behavior or incorrect output.

### Example Breakdown

Here’s a complete example illustrating both uses of `%d`:

```c
#include <stdio.h>

int main() {
    int x;

    // Using scanf to read an integer
    printf("Enter an integer: ");
    int result = scanf("%d", &x); // %d tells scanf to expect an integer
    printf("scanf returned: %d\n", result); // Print how many values were read

    // Using printf to output the integer
    printf("You entered: %d\n", x); // %d tells printf to print x as an integer

    return 0;
}
```

### Explanation of the Example

1. **Input Phase**:
   - The user is prompted to enter an integer.
   - The `scanf("%d", &x);` function call waits for user input.
   - If the user enters `10`, `scanf` reads `10`, converts it to an integer, and stores it in `x`. It returns `1` (since one value was successfully read).

2. **Output Phase**:
   - The program then prints `scanf returned: 1`, indicating successful input.
   - Finally, `printf("You entered: %d\n", x);` prints the value of `x`, formatted as an integer. Here, `%d` ensures that `10` is displayed correctly as `10`.

### Summary

- **Why Use `%d`?**
  - It specifies that an integer is expected (in `scanf`).
  - It ensures proper formatting when printing integers (in `printf`).
  - It is essential for correctly interpreting and displaying numeric values.

Using the correct format specifier is vital in C programming, as it dictates how data is read from or written to the console, ensuring that the program behaves as expected and reduces errors.

```c
Question 5 
 




# include <stdio.h>
int main()
{
   int i=0;
   for(i=0; i<20; i++)
   {
     switch(i)
     {
       case 0:
         i+=5;
       case 1:
         i+=2;
       case 5:
         i+=5;
       default:               
         i+=4;
         break;
     }
     printf("%d  ", i);
   }
 
   getchar();
   return 0;
}   
Output
16  21  
Explanation: 
Initially i = 0. Since case 0 is true i becomes 5, and since there is no break statement till last statement of switch block, i becomes 16. Before starting the next iteration, i becomes 17 due to i++. Now in next iteration no case is true, so execution goes to default and i becomes 21.
In C, if one case is true switch block is executed until it finds break statement. If no break statement is present all cases are executed after the true case. If you want to know why switch is implemented like this, well this implementation is useful for situations like below.
```
