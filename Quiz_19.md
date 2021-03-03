Reverse Mode: Given the input/outputs shown, create the program that produces the output. 

```.py
# Create class solution to solve the question
class solution():
# initialize the input as a string
    def __init__(self,input):
        self.input: str = input

# Create a function reverse to convert the input string to the number in decimal
    def reverse(self):
        input = self.input
        # by spliting the string input, we can get a list of three number strings 
        newList = input.split("!")
        # loop in each string in the newList  
        for i in range(len(newList)):
        
            print(str(int(newList[i],2)),end="")

        return

solution("100!000!111").reverse()

```

Test result:

![Quiz19.png](https://github.com/cathymonkey/Unit_3/blob/main/Images/Quiz19.png)
