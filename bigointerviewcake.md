#The Big Idea Behind Big O Notation
Big O Notation is the language we use for articulating how long a problem takes to run. It's how we compare the efficiency
of different approaches to a problem.

With big O notation we express the runtime in terms of - brace yourself - how quickly it grows relative the input, as the 
input gets arbitrarily large.

Let's break that down:

1. how quickly the runtime grows - some external factors affect the time it takes for a function to run: the speed of 
the processor, what else the computer is running, etc. So it's hard to make strong statements about the exact runtime of
the algorithm. Instead we use big O notation to express how quickly its runtime grows.
2. relative to the input - since we're not looking at an exact number, we need something to phase our runtime growth in
terms of. We use the size of the input. So we can say things like the runtime grows "on the order of the size of the input"
O(n) or "on the order of the square of the size of the input" O(n^2). 
3.as the input gets arbitrarily large - Our algorithm may have steps that seem expensive when n is small but are eclipsed
eventually by other steps as n gets huge. If you know what an asymptote is, you might see why "Big O analysis" is sometimes
called asymptotic analysis.

#Some Examples

                              public void printFirstItem(int[] arrayOfItems){
                              System.out.println(arrayOfItems[0]);
                              }
                              
This function runs O(1) (constant time) relative to its input. The input array could be one item or 1,000 items, but this
function would still require one "step".

                             public void printAllItems(int[] arrayOfItems){
                              for(item: arrayOfItems) {
                                System.out.println(item);
                                }
                             }
                             
This function runs in O(n) time (or "linear time"), where n is the number of items in the array. If an array has 10 items,
we have to print 10 times. If it had 1,000 items, we have to print 1,000 times. 

                            public void PrintAllPossibleOrderedPairs(int[] arrayOfItems){
                             for(int firstItem: arrayOfItems) {
                              for(int secondItem: arrayOfItems) {
                                int[] orderedPair = new int[]{firstItem, secondItem};
                                System.out.println(Arrays.toString(orderedPair));
                                }
                            }
                            
Here, we're nesting two loops. If our array has n items, our outer loop runs n times and our inner loop runs n times
for each iteration of the outer loop, giving us n^2 total prints. Thus this function runs is O(n^2) in quadratic time.
If the array has 10 items, we have to print 100 times. If it has 1,000 items, we have to print 1,000,000 times.

#N could be the actual input, or the size of the input
Both of these functions have O(n) runtime, even though one takes an integer as its input  and the other takes the array:

                       public void sayHiNTimes(int n){
                        for(int x=0; x<n; x++) {
                         System.out.println("hi");
                         }
                       }
                       
                       public void printAllItemsInArray(int[] theArray) {
                        for(int item: theArray) {
                         System.out.println(item);
                         }
                        }
                       
