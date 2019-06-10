Add your answers to the Algorithms exercises here.

## Exercise I

Give an analysis of the running time of each snippet of
pseudocode with respect to the input size n of each of the following:

```
a)  a = 0 
    while (a < n * n * n):
      a = a + n * n
```
Exercise I(a) is O(N). It combines a O(0) or O(C) with a while iterator N times that is O(N). The O(C) can be dropped as a worst case leaving it as O(N) time complexity.

```
b)  sum = 0
    for i in range(n):
      i += 1
      for j in range(i + 1, n):
        j += 1
        for k in range(j + 1, n):
          k += 1
          for l in range(k + 1, 10 + k):
            l += 1
            sum += 1
```
Exercise I(b) is O(N^3). It has nested loops which combines 3 for loops based on N inputs and 1 for loop based on a k constant range of 10. O(N) * O(N) * O(N) + O(C) => O(N^3) with the O(C) dropped.

```
c)  def bunnyEars(bunnies):
      if bunnies == 0:
        return 0

      return 2 + bunnyEars(bunnies-1)

Exercise I(c) is O(N). It is called recursively N times (deducting 1 bunny before calling function).

## Exercise II

Suppose that you have an _n_-story building and plenty of eggs. Suppose also that an egg gets broken if it is thrown off floor _f_ or higher, and doesn't get broken if dropped off a floor less than floor _f_. Devise a strategy to determine the value of _f_ such that the number of dropped eggs is minimized.

Write out your proposed algorithm in plain English or pseudocode and give the runtime complexity of your solution.

The conservative approach assuming no domain knowledge and a potential large range of floors, I would pursue a binary search that can divide and conquer. First check the mid point floor out of N stories of the building. If the egg breaks, go down and check the mid point floor between ground level and the floor we just checked and repeat this divide by 2 process until we can locate the floor in which the egg does not break. If the egg does not break and the floor right above has already been checked to have broken an egg then that current floor is the value of f to be returned. If the floor is not directly above then we continue our binary search process checking the mid point floor that is between the current checked floor without the egg broken and the last floor checked (which should be the closest) that did break the egg. This process mirrors the reverse if the first mid point floor of the building is checked and the egg does not break. The time complexity is O(log N) as it is a log base 2 by binary searching mid points. 

If we approached this problem with some domain knowledge and a very limited N story building(s) then an incremental iterative strategy is more appropriate. I would start from the first floor with the expectation that the eggs are highly sensitive to height of building and that we should reach the egg broken floor quickly just by going up one at a time. This approach optimizes the number of eggs dropped if there is a boundary on scale (number of floors in buildings) and that height of building's relationship to egg broken is not random. It would technically be O(N) but in practice it would actually have the efficiency of O(C).