Reverse Mode: Given the input/outputs shown, create the program that produces the output. 

```.py
# Create a class solution to solve the question
class solution():
# initialize the input as a string
    def __init__(self,input):
        self.input: str = input
# Create a function reverse to find the input in decimal
    def reverse(self):
        input = self.input
        # split the input string and make a list with three number strings
        newList = input.split("!")
        # loop the strings in the newList
        for i in range(len(newList)):
        # convert each string from binary to decimal and print them in one line
            print(str(int(newList[i],2)),end="")

        return

solution("100!000!111").reverse()

```

Test result:

![Quiz19.png](https://github.com/cathymonkey/Unit_3/blob/main/Images/Quiz19.png)
