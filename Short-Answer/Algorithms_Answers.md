#### Please add your answers to the ***Analysis of  Algorithms*** exercises here.

## Exercise I

a)

```
a)  a = 0
    while (a < n^3):
      a = (a + n^2)
```

The runtime complexity of this algorithin is N. This can be seen by  bombing like terms and seeing that the value of A is N^2, and the while condition is N^3. As a result, you will have to loop N times to meet the condition where a >= N^3.


b)

```
b)  sum = 0
    for i in range(n):
      j = 1
      while j < n:
        j *= 2
        sum += 1
```

The outer loop `for i in range(n):` adds a runtime complexity of O(N). The inner loop of `while j < n: j*=2` will run for O(log(n)) times. This is because as N grows larger, J will increment, but at a logarithmic rate since J grows multiplicatively but n grows linearly. The result is an algorithim that takes O(n*log(n))


c)
```
c)  def bunnyEars(bunnies):
      if bunnies == 0:
        return 0

      return 2 + bunnyEars(bunnies-1)
```

With a base case of n=0, the algorithim will recursively build a stack of n-1 until the base case is reached. So for every N values, the function will be called N times to arrive at an answer. For N=3, it will call f(3)=2+f(2)=4+f(1)=f(0)=6. N+1, aka O(N)

## Exercise II

```Suppose that you have an n-story building and plenty of eggs. Suppose also that an egg gets broken if it is thrown off floor f or higher, and doesn't get broken if dropped off a floor less than floor f. Devise a strategy to determine the value of f such that the number of dropped + broken eggs is minimized.

Write out your proposed algorithm in plain English or pseudocode AND give the runtime complexity of your solution.
```

So, the most efficient way to determine what floor an egg can be dropped from without breaking would be a binary search. This can be done because the floors in our apartment building are already sortted, floor 0 is the ground floor, and the next floor by definition is floor 1, this goes all the way to the top floor of floor N. Binary search has a runtime complexity of log(n) complexity, and works as follows:

* Given N floors in a building, pick the halfway point between current floor and the top floor. f = (n//2)
    * Drop an egg from floor f:
    * If it breaks, go to the halfway point between current floor f, and the ground floor (f=0). f' is the new floor.
            f' = f - (f//2)
    * If it does NOT break, go to the halfway point between current floor f, and the top floor (n). f' is the new floor.
            f' = f + (n-f//2)
    * Continue this process until at a floor f', the egg does not break, but at floor f'+1 it does break.
    * return the value of floor f' the current floor


def egg_check(f, n):
    '''
    f = current floor
    n = total floors
    '''

    

    if egg_check(f, n) == broken:
        #egg broke
        #go to halfway point between current floor f, and ground level 0.
        new_floor = f - (f//2)
        return egg_check(new_floor,n)
    elif egg_check(f, n) == safe:
        #egg is safe
        #go to halfway point between current floor f and the roof n
        new_floor = f + (n-f//2)
        return return egg_check(new_floor,n)
    elif (egg_check(f, n)==safe AND egg_check(f+1, n)==broken):
        return f
