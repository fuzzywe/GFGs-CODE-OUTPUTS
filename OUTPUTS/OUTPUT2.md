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
0 0 0 0 

=== Code Execution Successful ===
