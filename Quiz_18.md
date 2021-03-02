Given a number as a String N. Multiply all of the digits of N, and repeat the same wSince it took us 3 steps to reach a number with only 1 digit, the output is 3.ith the product obtained till the product consists of only one digit. Output the number of steps taken to do so. 

Example: N = 39
Step 1: 3 * 9 = 27
Step 2: 2 * 7 = 14
Step 3: 1 * 4 = 4

Since it took us 3 steps to reach a number with only 1 digit, the output is 3.

```.py
class Solution:
    def __init__(self,N):
        self.N: str = self.N

    def single_digit(N:str):
        step = 0
        while len(N) > 1:
            product = 1
            for i in range(len(N)):
                product *= int(N[i])

            N = str(product)
            step += 1

        return step

print(Solution.single_digit("39"))
```
Test result:

![quiz18.png](https://github.com/cathymonkey/Unit_3/blob/main/Images/quiz18.png)

When step = 7, one of the numbers is 68898. I guess there's no number that needs 10 steps to multiply to become a single digit.
