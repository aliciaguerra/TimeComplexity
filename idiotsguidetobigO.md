#O(1): Constant Complexity
Constant. This means irrelevant of the size of the data set, the algorithm will always take constant time.
1 item takes 1 second, 10 items take 1 second, 100 items takes 1 second
It always takes the same amount of time.

#O(logn): Logarithmic Complexity
Not as good as constant, but still pretty good. The time taken increases size of the data set, but not proportionately so.
This means the algorithm takes longer per item on smaller datasets relative to larger ones.

1 item takes 1 second, 10 items takes 2 seconds, 100 items takes 3 seconds

If your dataset has 10 items, each item causes 0.2 seconds latency. If your dataset has 100, it only takes 0.3 seconds extra
per item. This makes logn algorithms very scalable.

#O(n): Linear Complexity
The larger the data set, the time grows proportionally. 

1 item takes 1 second, 10 items take 10 seconds, 100 items take 100 seconds

#O(nlogn)
A nice combination of the previous two. Normally, there's 2 parts to the sort, the first loop is O(n), the second is
O(logn), combining to form O(nlogn)

1 item takes 2 seconds, 10 items take 12 seconds, 100 items takes 103 seconds

#O(n^2): Quadratic Complexity
Things are getting extra slow. 
1 item takes 1 second, 10 items take 100 seconds, 100 items take 10000

#O(2^n): Exponential Growth
This item takes twice as long for every new element added. 
1 item takes 1 second, 10 items take 1024 seconds, 100 items takes
1267650600228229401496703205376 seconds

Imagine an algorithm which loops through a list exactly two times. This would be O(2n) complexity, as it's going through 
your list length n twice!

#Why does this matter?
Simply put: an algorithm that works on a small dataset is not guaranteed to work well on a large dataset. Just because
something is lightning on your machine doesn't mean it's going to work when you're scaling up a serious dataset. You need
to understand exactly what your algorithm is doing, and what it's big O complexity is in order to choose the right solution.

There are 3 things we care about with algorithms: best case, worst case, and expected case. In reality, we only care about
the latter two, as we're a bunch of pessimists. If you ask an algorithm to sort a pre-sorted list, it's probably going to
do it much faster than a completely jumbled list. Instead, we want to know the worst case (the absolutely maximum amount
of steps the algorithm could take) and the expected case (the likely or average number of steps). 

#O(1)
Irrelevant of the size, it will always return at constant speed. The JavaDoc for Queue states that it is "constant
time for the retrieval methods (peak, element, and size)". It's pretty clear why this is the case. For peek, we are always
returning the first element which we always have a reference to; it doesn't matter how many elements follow it. The size of
this list is updated upong addition/removal, and referencing this number is just one operation to access no matter what size
the list is.

#O(logn)
The classic example is binary search. You're a massive movie geek so you've obviously alphabetized your movie collection. 
To find your copy of "Back to the Future", you first go to the middle of the list. You discover the middle film is 
"Meet the Fockers", so you head to the move in between the start and this film. You discover this is "Children of Men".
You repeat this again and you've found "Back to the Future". 
Although more elements will increase the amount of time it takes to search, it doesn't do so proportionately. Therefore,
it is O(logn).

#O(n)
As discussed in the Collections chapter, LinkedLists are not so good (relatively speaking) when it comes to retrieval.
It actually has a complexity of O(n) for the worst case: to find an element T, which is the last element in the list,
it is necessary to navigate the entire list of n elements. As the number of elements increases so does the access time
in proprotion.

O(nlogn) 
The best example of O(nlogn) is a merge sort. This is a divide and conquer algorithm. Imagine you have a list of integers.
We divide the list in two again and again until we are left with a number of lists with 1 item in: each of these lists 
is therefore sorted. We then merge each list with its nieghbor (comparing the first elements of each every time). We 
repeat with the new composite list until we have our sorted result. 
To explain why this is O(nlogn) is a little more complex. In the above example of 8 integers, we have 3 levels of 
sorting:

- 4 list sorts when the list sizes are 2
- 2 list sorts when the list sizes are 4
- 1 list sort when the list size is 8

Now if I were to double the level of sorting to 16: this would only require one more level of sorting. Hopefully you
recognize this is a logn scale.

However, on each level of sorting a total of n operations takes place(looking at the red boxes in the diagram above).
The results in (n*logn) operations, e.g. O(nlogn).

#O(n^2)
The Bubble sort algorithm is everyone's first algorithm in school, and interestingly is quadratic complexity. If you need
a reminder, we go through the list and compare each element with the one next to it, swapping the elements if they are
out of order. At the end of the first iteration, we then start again from the beginning, witht the caveat that we now 
know the last element is correct.

Imagine writing the code for this; it's two loops of n iterations:

                          public int[] sort(int[] toSort){
                           for(int i=0; i<toSort.length -1; i++) {
                            boolean swapped = false;
                            for(int j=0; j<toSort.length-1-i; j++) {
                             if(toSort[j]>toSort[j+1]) {
                             swapped = true;
                             int swap = toSort[j+1];
                             toSort[j+1] = toSort[j];
                             toSort[j] = swap;
                               }
                             }
                            if(!swapped)
                              break;
                            }
                            return toSort;
                            }
  
This is also a good example of best vs worst case. If the list to sort is already sorted, then it will only take one
iteration (e.g. n) to sort. However, in the worst case, we have to go through the list n times and each time looping
through another n times (less how may loops we have done before) which is slow.


























