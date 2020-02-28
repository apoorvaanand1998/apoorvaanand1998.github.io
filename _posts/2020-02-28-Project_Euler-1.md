---
layout: post
title: How Project Euler teaches you to think about Data Structures and Algorithms
subtitle: My journey through problem 71, 72 and 73
tags: [Computer Science, Project Euler, Data Structures, Algorithms]
---

## Problem 71

> Consider the fraction, n/d, where n and d are positive integers. If n<d and HCF(n,d)=1, it is called a reduced proper fraction. If we list the set of reduced proper fractions for d <= 8 in ascending order of size, we get: 
>
> 1/8, 1/7, 1/6, 1/5, 1/4, 2/7, 1/3, 3/8, 2/5, 3/7, 1/2, 4/7, 3/5, 5/8, 2/3, 5/7, 3/4, 4/5, 5/6, 6/7, 7/8
>
> It can be seen that 2/5 is the fraction immediately to the left of 3/7. By listing the set of reduced proper fractions for d <= 1,000,000 in ascending order of size, find the numerator of the fraction immediately to the left of 3/7.

Whenever I try and solve these problems, I always try to write out the "simplest" solution first. There are three reasons for this -
1. Sometimes the simplest solution just works (This seems to be working less and less as I'm going further along the problems).
2. The simplest solution might not solve the problem but it helps in the identification of patterns, that is, it helps you by giving you more "observations" about the problem.
3. And of course, in the iterative development of a better solution.

My solution to Problem 71 falls under the second category above. I started off with only one single observation - **For a given denominator d, a numerator n appears in the list of ascending proper fractions only if n < d and ((d % n) != 0)**

Armed with only this, I wrote the following program:

```python
diff = [1, 1, 1] ## difference between fraction being tested and 3/7
## we went this difference to be the smallest for d <= 10**6
## while the fraction itself is smaller than 3/7

for denominator in range(2, 10**6+1):
    for numerator in range(2, denominator):
        if denominator % numerator != 0:
            if numerator / denominator >= 3/7:
                break
            else:
                our_frac_val = numerator / denominator
                if (3/7 - our_frac_val) < diff[2]:
                    diff = [our_frac_val,
                            str(numerator) + "/" +
                            str(denominator),
                            3/7 - our_frac_val]
                    print(diff)
```

This is a terribly inefficient program, especially when you have to search through all denominators <= 10**6 and all numerators <= d for each denominator d. This makes our solution O(n^2), *but* by printing diff we get a great observation. For each denominator, we notice -

**Starting from 2/5 (which is already given to us in the problem statement), every time diff improves the numerator increases by 3 and the denominator increases by 7**

Now there's a great observation to have stumbled into. Knowing this, this really simple program immediately solves the problem -

```python
denom = 12  ## first denom found by above program
denom_counter = 0
while (denom+7) < 10**6:
    denom += 7
    denom_counter += 1

numer = 5  ## first numer found by above program
numer = numer + denom_counter * 3
print(numer)
```

## Problem 72

> Consider the fraction, n/d, where n and d are positive integers. If n<d and HCF(n,d)=1, it is called a reduced proper fraction. If we list the set of reduced proper fractions for d <= 8 in ascending order of size, we get:
>
> 1/8, 1/7, 1/6, 1/5, 1/4, 2/7, 1/3, 3/8, 2/5, 3/7, 1/2, 4/7, 3/5, 5/8, 2/3, 5/7, 3/4, 4/5, 5/6, 6/7, 7/8
>
> It can be seen that there are 21 elements in this set. How many elements would be contained in the set of reduced proper fractions for d <= 1,000,000?

I started off this problem by thinking of a better way to generate the fractions. After playing around with different values of denominators and numerators, I stumbled upon this observation -

**The fraction in between two fractions a/b and p/q is (a+p)/(b+q)**

Using this observation, I tried solving the question by generating the fractions. Turns out, for d <= 10**6, that's a very bad way to do it. I left the program and when I came back to it later, I realized I don't need to know the fractions at all, simply the _number of fractions_.

This immediately made me think of [Problem 69](https://projecteuler.net/problem=69) and [Problem 70](https://projecteuler.net/problem=70) which touches on the concept of the [Totient Function](https://en.wikipedia.org/wiki/Euler%27s_totient_function).

Project Euler, you clever teacher you. Harkening back to something like that!

Using this, here's a program I wrote -

```python
def primes(n):
    pl = [True] * n
    pl[0] = pl[1] = False

    for i in range(int(n**0.5)+2):
        if pl[i]:
            for j in range(i*i, n, i):
                pl[j] = False

    prime_set = set()
    for i in range(n):
        if pl[i]:
            prime_set.add(i)
    return prime_set

def phi(n):
    result = n
    i = 2
    while (i*i <= n):
        if (n % i == 0):
            while (n % i == 0):
                n /= i
            result -= result // i
        i += 1
    if n > 1:
        result -= result // n
    return result

p = primes(10**6)
d = 10**6 + 1
ans = 0

for i in range(2, d):
    if i in p:
        ans += (i-1)
    else:
        ans += phi(i)
print(int(ans))
```

Here's the problem with this solution. Although it does give us a solution, it takes far too long to do it. On my computer ~20 seconds and one can see why this happens. For each composite number c, phi(c) is calculated by factoring c again and again. For a better explanation, look at [Euler's product formula](https://en.wikipedia.org/wiki/Euler's_totient_function#Euler's_product_formula).

Unfortunately this is one of those questions where I had to settle for my "worse" answer. I could think of no way to improve my solution so I proceeded to read the overview of the solution after submitting the answer from my previous program.

Here's where most of my learning happened amongst these 3 problems. The overview does go over my approach to this problem but calls it inefficient (as it should!). It then goes on to explain that we could use a sieve to solve this issue, because we factor all numbers between 1 and 10**6 to calculate phi.

This honestly blew my mind. Up until this point, the only "sieve" I'd been using was [Sieve of Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes) but as soon as the overview mentioned how you could use a sieve to improve the computation of all phis, it made complete sense.

I saw how the concept carried over to the calculation of phis, especially when it involved numbers between 1 and 10**6. We know that phi(n) = n * product of (1 - 1/prime factors). From this we get the algorithm below -

1. Create a list of numbers where initially the list holds the index number of each position of the list ([0, 1, 2,...]).
2. Iterate through the list, for every number = it's index, multiply every multiple of that number n, with (1 - 1/n).
3. And that's it! From this one trick (combining the concept of euler totient function with the sieving technique introduced in the prime sieve, which deals with cutting down repeated computations), we get the phi for every number on the list.

Here's the program -

```python
d = 10**6

phi = []
for i in range(d+1):
   phi.append(i)

for i in range(2, d+1):
    if phi[i] == i:
        for j in range(i, d+1, i):
            phi[j] -= phi[j] / i

result = 0            
for i in range(2, d+1):
    result += phi[i]
print(result)
```

Looking at the above program and the techniques involved is what inspired me to write this blog. This program solves the question in around 1 second on my computer.

## Problem 73

> Consider the fraction, n/d, where n and d are positive integers. If n<d and HCF(n,d)=1, it is called a reduced proper fraction. If we list the set of reduced proper fractions for d <= 8 in ascending order of size, we get:
>
> 1/8, 1/7, 1/6, 1/5, 1/4, 2/7, 1/3, 3/8, 2/5, 3/7, 1/2, 4/7, 3/5, 5/8, 2/3, 5/7, 3/4, 4/5, 5/6, 6/7, 7/8
>
> It can be seen that there are 3 fractions between 1/3 and 1/2. How many fractions lie between 1/3 and 1/2 in the sorted set of reduced proper fractions for d <= 12,000?

Looks like my observation from the previous problem that I'd discarded wasn't so useless after all. I could use it to simply generate the list of fractions. Here's the first iteration of the program I wrote:

```python
l = [[1, 3], [1, 2]]
d = 12000
i = 0

while (i < len(l) - 1):
    num = l[i][0] + l[i+1][0]
    denom = l[i][1] + l[i+1][1]

    if num < d and denom <= d:
        l.insert(i + 1, [num, denom])
    else:
        i += 1
print(len(l)-2)
```

Thanks to the observation and python's insert() function this program is straightforward. Each element in the list l is a representation of a fraction. For example it starts with 1/3 and 1/2. But running it only got me an answer at around 12 seconds on my computer which was far too much to my liking.

Thinking about where most of the time was being taken, I looked up the [time complexity of the list functions](https://wiki.python.org/moin/TimeComplexity#list). So there's the culprit, insert was O(n) and this was what was slowing my program down. I also noticed that the pop() function on a list was O(1).

That got me thinking about a way to use the stack data structure to solve the problem. After a bit of thinking I arrived at this -

```python
d = 12000
curr = [1, 3]
frac_list = [[1, 2]]
count = 0

while (len(frac_list) > 0):
    num = curr[0] + frac_list[-1][0]
    denom = curr[1] + frac_list[-1][1]

    if num < d and denom <= d:
        frac_list.append([num, denom])
        count += 1
    else:
        curr = frac_list.pop()
print(count)
```

By only using O(1) functions, we reduce the computation time to around 7 seconds. But wait, there's more we can do. When we look at the programs above we see that we check to see if num < d and denom <= d. This is unnecessary, checking if denom <= d is enough. Also, we don't need to keep track of the numerators at all. This reduces our frac_list from a list of lists to a list of numbers. And for an additional speedup of a few milliseconds, we can also use deque (double ended queue) that python provides.

```python
from collections import deque

d = 12000
curr = 3
denom_deque = deque([2])
count = 0

while (len(denom_deque) > 0):
    denom = curr + denom_deque[-1]

    if denom <= d:
        denom_deque.append(denom)
        count += 1
    else:
        curr = denom_deque.pop()
print(count)
```

This reduces our computation time to around 4 seconds. Good enough for me! :) The overview for this problem goes through some really mind-blowing math to solve this problem and also introduces the [Stern-Brocot tree](https://en.wikipedia.org/wiki/Stern%E2%80%93Brocot_tree) data structure, things I wouldn't feel confident blogging about (for now, at least).
