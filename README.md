1. Using Keil software, observe the various Registers, Dump, CPSR, with a simple Assembly
Language Programs (ALP).
Module – 2
2. Develop and simulate ARM ALP for Data Transfer, Arithmetic and Logical operations
(Demonstrate with the help of a suitable program).
3. Develop an ALP to multiply two 16-bit binary numbers.
4. Develop an ALP to find the sum of first 10 integer numbers.
5. Develop an ALP to find the largest/smallest number in an array of 32 numbers.
6. Develop an ALP to count the number of ones and zeros in two consecutive memory locations.
Module – 3
7. Simulate a program in C for ARM microcontroller using KEIL to sort the numbers in
ascending/descending order using bubble sort.
8. Simulate a program in C for ARM microcontroller to find factorial of a number.
9. Simulate a program in C for ARM microcontroller to demonstrate case conversion of characters
from upper to lowercase and lower to uppercase.
Module – 4 and 5
10. Demonstrate enabling and disabling of Interrupts in ARM.
11. Demonstrate the handling of divide by zero, Invalid Operation and Overflow exceptions in ARM.

1.DATA TRANSFER

	AREA MOV,CODE,READONLY
START
	MOV R1,#0005
	MOV R2,#0002
	MOV R3,R1
	MOV R4,R2
STOP B STOP
	END

1B. ADDITION

	AREA MOV,CODE,READONLY
START
	MOV R7,#0005
	MOV R8,#0004
	ADD R3,R7,R8
	MOV R6,R3
STOP B STOP
	END


1C. SUBSTRACTION

	AREA MOV,CODE,READONLY
START
	MOV R4,#7
	MOV R6,#5
	SUB R5,R4,R6
	MOV R9,R5
STOP B STOP
	END

1D. ARITHEMATIC 

	AREA ADD,CODE,READONLY
START 
	MOV R1,#0005
	MOV R2,#0002
	ADD R3,R2,R1
	SUB R5,R1,R2
	MUL R6,R1,R2
	MOV R7,R6
	ADD R7,#2
	MOV R8,R7
	SUB R8,#3
	MOV R9,R8
STOP B STOP
	END

1E.LOGICAL

	AREA DIS,CODE,READONLY
START
	MOV R0,#5
	MOV R1,R0
	AND R1,#4
	MOV R2,R1
	LSR R2,#1
	MOV R3,R0
	AND R3,#3
	AND R1,R0
	ORR R2,R1
	LSR R2,#2
STOP B STOP
	END
	
2. TWO BINARY BIT NUMBERS

	AREA MOV,CODE,READONLY
START
	MOV R1,#6400;
	MOV R2,#3200;
	MUL R3,R1,R2;
STOP B STOP
	END

3.  SUM OF FIRST 10 NUMBERS

	AREA SUM5,CODE,READONLY
START
	MOV R0,#10
	MOV R1,#00
LOOP
	ADD R1,R1,R0
	SUBS R0,R0,#1
	BNE LOOP
STOP B STOP
	END

4. ARRAY OF 32 NUMBERS

	AREA LARGEST,CODE,READONLY
START
	LDR R0,=TABLE
	MOV R1,#8
	LDR R2,[R0],#4
LOOP
	LDR R3,[R0],#4
	CMP R2,R3
	MOVCC R2,R3;
	SUBS R1,R1,#1
	BNE LOOP
STOP B STOP
TABLE
	DCD 0X11111111,0X55555555,0X12345678,0X45673245,0X33333333,0X67543876,0Xa2345678,0Xbcd45432
	END

5. ONES & ZEROS

	AREA COUNT,CODE,READONLY
START
	LDR R0,=0X40000050
	LDRH R1,[R0]
	MOV R2,#16
LOOP
	MOVS R1,R1,LSR#1
	ADDCS R3,#1
	ADDCC R4,#1
	SUBS R2,#1
	BNE LOOP
STOP B STOP
	END

6. FACTORIAL 

#include<lpc214x.h>
int main()
{
unsigned long i,fact=1;
unsigned long m=4;
for(i=1;i<=m;i++)
{
fact=fact*i;
}
}

7. Bubble Ascending

#include<lpc214x.h>
int main()
{
unsigned long i,n=4,temp,j;
unsigned long arr[]={0Xaaaaaaaa,0X11111111,0X33333333,0X44444444,0X66666666};
for(i=0;i<n;i++)
{
for(j=0;j<n-i;j++)
	{
if(arr[j]>arr[j+1])
	{
temp=arr[j];
arr[j]=arr[j+1];
arr[j+1]=temp;
  }
}
while(1);
 }
}


8.Bubble Descending 

#include <lpc214x.h>

int main()
{
    unsigned long i, n = 5, temp, j;
    unsigned long arr[] = {0Xaaaaaaaa, 0X11111111, 0X33333333, 0X44444444, 0X66666666};
    
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n - i -1; j++)  
        {
            if (arr[j] < arr[j + 1])
            {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    while (1);
    return 0; 
}

9. Uppercase And Lowercase 

#include<lpc214x.h>
int main()
{
	char s[100]={"WELcome HOme\0"};
		int i;
		
		for(i=0;s[i]!='\0';i++)
		{
			if(s[i]>='a' && s[i]<='z')
			{
				s[i]=s[i] - 32;
			}
			else if (s[i] >= 'A' && s[i] <='Z')
			{
				s[i] = s[i] + 32 ;
			}
		}
}
	
