## Part 1: Create a Function to Check if a Number Is Prime
You can find the complete code of the solution in the attached file. Please review the code and try to understand it in the notebook. If you encounter any aspects that appear unclear, return here to consult the solution.

Your first task was to write a function that will return True if the provided number is a prime number and False otherwise.

The most basic form of this function consists of three parts:

Evaluating special cases—in this case, it’s 0 and 1
Checking the main condition of a number not being prime (It’s easier to know whether a number is not prime, than whether it is)
If the above check fails, the number is a prime, so return True.
The first part is a simple if statement.

# Deal with special cases
if n == 0 or n == 1:
    return False
We can consider the cases when n is 0 or 1 and return False because these are not considered primes. Since we have a return statement here, if it’s executed (i.e., if n = 0 or n = 1), Python will ignore the rest of the code in this function. This behavior of return statements is essential for the rest of the code.

But why include this check here? Primes are strictly defined for natural numbers greater than 1—meaning 0 or 1 should not be considered when checking for prime numbers. But in practical coding, it's often more convenient to include these edge cases because it simplifies the function's future use and accommodates users who may not be aware that prime numbers exclusively apply to numbers greater than 1, as they might attempt to use the function with 0 or 1 regardless.

The next part of the function contains the main piece of code.

# Loop through all numbers between 2 and n - 1, and check if n is NOT prime
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

# If the program reached this point, that means the number is prime
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