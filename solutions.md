## Part 1: Create a Function to Check if a Number Is Prime
You can find the complete code of the solution in the attached file. Please review the code and try to understand it in the notebook. If you encounter any aspects that appear unclear, return here to consult the solution.

Your first task was to write a function that will return True if the provided number is a prime number and False otherwise.

The most basic form of this function consists of three parts:

Evaluating special cases—in this case, it’s 0 and 1
Checking the main condition of a number not being prime (It’s easier to know whether a number is not prime, than whether it is)
If the above check fails, the number is a prime, so return True.
The first part is a simple if statement.

## Deal with special cases
if n == 0 or n == 1:
    return False
We can consider the cases when n is 0 or 1 and return False because these are not considered primes. Since we have a return statement here, if it’s executed (i.e., if n = 0 or n = 1), Python will ignore the rest of the code in this function. This behavior of return statements is essential for the rest of the code.

But why include this check here? Primes are strictly defined for natural numbers greater than 1—meaning 0 or 1 should not be considered when checking for prime numbers. But in practical coding, it's often more convenient to include these edge cases because it simplifies the function's future use and accommodates users who may not be aware that prime numbers exclusively apply to numbers greater than 1, as they might attempt to use the function with 0 or 1 regardless.

The next part of the function contains the main piece of code.

## Loop through all numbers between 2 and n - 1, and check if n is NOT prime
i = 2
while i < n:
    if n % i == 0:
        return False
    i = i + 1
If you recall, the definition of a prime is a number not divisible by any natural number between 2 and n - 1, inclusive. This definition should prompt you to loop through all the numbers between 2 and n - 1—precisely the purpose of this while loop. Of course, you could do the same thing with a for loop and the range() function, as such:

 for i in range(2, n):  

After the loop is set up, we can check whether n is divisible by each number in this loop through the  %  operator.  n % i  would give us the remainder of n divided by i. For n to be divisible by i, the remainder should be 0.

If that occurs, and n is divisible even once, it means n is not prime. (We mentioned that it’s easier to check if n is not prime than if n is prime.) Of course, if n is not prime, we can immediately return False. This will also immediately stop the execution of the function—crucial for the next part.

This next part is just one line, but it works precisely because of that return in the loop.

## If the program reached this point, that means the number is prime
return True  
We immediately stop the function whenever we ensure a number is not a prime. So, Python will only ever get to the last line in the function if the number itself is prime. That’s why we’re confident that n is prime and can return True.

There’s just no other possibility; if the number is not prime, we would’ve already stopped the program and returned False.

There is, however, another way to achieve the same result. We can use a flag variable representing our current understanding of whether n is prime. Note the following code for this:

def is_prime(n):
    
    # Assume the number is prime and try to find counterexamples
    flag = True

    # Deal with special cases
    if n == 0 or n == 1:
        flag = False
    
    # Loop through all numbers between 2 and n - 1, and check if n is NOT prime
    i = 2
    while i < n:
        if n % i == 0:
            flag = False
        i = i + 1
    
    # Output the current value of flag
    return flag
    
We first start by assuming that n is prime, so the flag variable is set to True initially. Then, if we find a counterexample that n is, in fact, not prime, we can change the flag to False. Ultimately, we output the flag variable in its final state.

The two versions of the code are equivalent and use the same logic. Try to find a number i so that n is divisible by i. In such a case, n is not prime. If that doesn’t occur, n is prime.



## Part 2: Count Prime Numbers in a Range
Now that we’ve created the function is_prime(), we can use it to find how many primes there are in the range of 100 to 151 inclusive. To do that, I have set up a loop that iterates through every single number in the range, tests it for primality, and increases a counter variable if it is.

Here, be mindful of the range() function inputs. Consider the range of 100 to 151 inclusive. So, the starting number in range() should be 100. But the end number in range() is not included in the resulting list—instead, the number just before it is considered the last.

## Note the following example to make matters more straightforward. If we write range(2, 5), the resulting list of numbers will be [2, 3, 4] – 5 is not included, and the list ends with 4.

So, to include 151 in the list, we should write range(100, 152).


## Part 3: Optimize the Code (Optional)
This part of the project is for those more interested in programming and optimizing and those with a knack for math.

Let’s delve deeper into the concept of non-prime numbers. When a number is not prime, it implies that it can be expressed as the product of at least two other numbers. For example, consider the number 12. It’s not prime because 12 is divisible by 2. You can write it as 2x6. But looking at that product, we can see that 12 is also divisible by both 6 and 2. Therefore, numbers that divide 12—or any other number—come in pairs. And, of course, there may be more than one pair. In the case of 12, we can also write it as 4x3.

The point is, the numbers we are interested in (those that divide n) come in pairs. And if we find one of those numbers, we immediately know the other one as well.

What does that have to do with making the code more efficient? When testing for primality, we’re not interested in how many such product pairs there are or precisely the numbers. We’re only curious if at least one such number exists.

And here's one handy mathematical relation—if such a pair exists, then one of the numbers would be smaller than the square root of n, and the other would be bigger than the square root, with only one exception. If both numbers are equal, they’re equal to the square root.

To clarify, let's designate the square root of n as sqrt(n), and according to its definition,  n = sqrt(n) * sqrt(n) . Moreover, as previously discussed, product pairs are denoted as  n = a * b  for non-prime numbers. So,  a * b = sqrt(n) * sqrt(n) .

In this context, when both a and b are less than sqrt(n), their product  a * b  will be smaller than  sqrt(n) * sqrt(n) . This occurs because we multiply two smaller values, resulting in a smaller product. Conversely, the same principle applies when a and b are both greater than sqrt(n):  a * b   will be greater than  sqrt(n) * sqrt(n)  under these conditions.

So, the only option is for a and b to be on the opposite sides of sqrt(n) (or for  a = b = sqrt(n) ). You can imagine this as if sqrt(n) is the ‘midpoint’ of all product pairs, where half the factors of n reside to the left of its square root, while the other half are to the right of it.

Suppose we return to the example with the number 12. The square root of 12 is approximately 3.4. And the product pairs we had were 2x6 and 3x4. 3.4 sits in the middle of both those pairs.

Let’s consider another example: 120. The square root of 120 is around 10.9. The product pairs for 120 are 2x60, 3x40, 4x30, 5x24, 6x20, 8x15 and 10x12. Notice how the square root sits between all of the pairs.

What does this all mean for the code? Well, we only need to search for factors of n up to sqrt(n) instead of n - 1 because we can find all available pairs by considering only the numbers up to sqrt(n). If we have not found a number that divides n by the point we reach sqrt(n), we won’t find any after that point. After all, if such a number existed, it would have a counterpart smaller than sqrt(n), and we already checked all of those.

That’s why the optimization for this function is to not loop from 2 to n – 1 but from 2 to the square root of n.

Finally, in order to include the square root in Python, we need to import the math library. Then, we can access the square root through math.sqrt().