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

So sometimes n is an actual number that's an input to our function, and other times n is the number of items in an input
array (or an input map, or an input object, etc.)

#Drop the Constants
That is why big O notation rules. When you're calculating the big O complexity of something, you just throw out the constants. So like:

                      public void printAllItemsTwice(int[] theArray) {
                       for(int item: theArray) {
                       System.out.println(item);
                       }
                       
                      //once more, with feeling
                      for(int item: theArray) {
                       System.out.println(item);
                       }
                      }
                      
This is just O(2n), which we call O(n).

                    public void printFirstItemThenFirstHalfThenSayHi100Times() {
                     System.out.println(theArray[0]);
                     
                     int middleIndex = theArray.length/2;
                     int index=0;
                     
                     while(index<middleIndex) {
                     System.out.println(theArray[index]);
                     index++;
                     }
                     
                     for(int x=0; x<100; x++) {
                     System.out.println();
                     }
                    }
                    
This is O(1) + O(n)/2 + 100, which we just call O(n)

Why can we get away with this? Remember, as big O notation we're looking for what happens as n gets arbitrarily large.
As n gets really big, adding 100 or dividing by 2 has a decreasingly significant effect.

#Dropping the less significant terms

                  public void printAllNumbersThenAllPairSums(int[] arrayOfNumbers) {
                      System.out.println("these are the numbers");
                      for(int number: arrayOfNumbers) {
                        System.out.println(number);
                      }
                      
                      System.out.println("and these are their sums:");
                      for(int firstNumber: arrayOfNumbers) {
                       for(int secondNumber: arrayOfNumbers) {
                         System.out.println(firstnumber+secondNumber);
                              }
                            }
                      }

Here, our runtime is O(n + n^2), which we just call O(n^2). Even if it was O(n^2/2 + 100/n), it would still be O(n^2)

Similarly:

- O(n^3 + 50n^2 + 10000) is O(n^3)
- O((n+30) *(n+5)) is O(n^2)

Again, we can get away with this because the less significant terms quickly become, well, less significant as n gets big.

#We're usually talking about the "worse case"
Often the "worse case" situation is implied. But sometimes you can impress your interviewer by saying it implicitly.

Sometimes the worse case running time is significantly worse than the best case runtime:

                     public boolean contains(int[] haystack, int needle){
                      //does the haystack contain the needle?
                      for(int i=0; i<haystack.length; i++) {
                       if(haystack[i]==needle) return true;
                      }
                      return false;
                      }
                      
Here we might have 100 items in our haystack, but the first item might be the needle, in which case we would return
in just 1 iteration of the loop.

In general we'd say this is O(n) runtime and the "worse case" runtime would be implied. But to be more specific we could
say this is the worse case O(n) and best case O(1) runtime. For some algorithms, we can also make rigorous statements
about the "average case" runtime.

#Space Complexity: the Final Frontier
Sometimes we want to optimize for using less memory instead of (or in addition to) using less time. Talking about
memory cost (or space complexity) is vry similar to talking about time cost. We simply look at the total size (relative
to the size of the input) of the new variables we're allocating.

The function takes O(1) space (we aren't allocating any new variables):

                       public void sayHiNTimes(int n){
                        for(int x=0; x<n; x++){
                        System.out.println("hi");
                        }
                       }
                       
The function takes O(n) space (the size of hiArray scales with the size of the input):

                       public String[] arrayOfHiNTimes(int n) {
                        String hiArray = new String[n];
                        for(int i=0; i<n; i++) {
                         hiArray[i]="hi";
                         }
                        return hiArray;
                        }
                        
 Usually when we talk about space complexity, we're talking about additional space, so we don't include space taken up by
 the inputs. For example, this function takes constant space even though the input has n items:
 
                     public int getLargestItem(int[] arrayOfItems) {
                      int largest = 0;
                      for(int item: arrayOfItems) {
                       if(item>largest) {
                        largest = item;
                        }
                      }
                      return largest;
                      }
                      
Sometimes there's a tradeoff between saving time and saving space, so you have to decide which one you're optimizing for.

#Big O analysis is awesome except when it's not
Big O ignores constants but sometimes constants matter. If we have a script that takes five hours to run, an optimization
that divides the runtime by 5 might not affect big O, but it still saves you 4 hours of waiting.
