# MIT Introduction To Algorithms

## Lecture 1 - Algorithms and Computation

### Goal

    1-> solve computational problems
    2-> prove correctness
    3-> argue efficiency
    4-> communication of these ideas

**Computational Problems -->** For example there are inputs and possible outputs for my problem. The problem is a binary relation between these inputs and outputs. We maybe say that give me the index in an array containing the value 5, there could be multiple 5's in that arrray and any of those indices would be correct.

If I give it an input, it will generate an output. If it generates and output it better one of correct outputs. I have an algorithm that takes in an input, I really want it to output to its output or else its not correct algorithm.

**f : I -> O**

#### Example : For Birthday Problem(finding two person the class has the same birthday)

    -Maintain records

    -Interview students in some order

        -check if birthday in record

    	    -if so return pair

        -add new student to record

    -Return None

**Correctness**

Inductive Hypothesis: if first k students contain match algorithm returns a match before interviewing student k+1

Base Case : k = 0 Because with 0 inductive hypothisesis is true just because initial predicate is false

Assume Inductive Hypothesis true for k = k' { if k' contains match -> already returned by Inductive else if k'+1 contains match by Inductive algorithm k'+1 against all students }

#### Efficiency

Efficiency just means not only how fast does this algorithm run, but how fast does it compare to other possible ways of approaching this problem

So how could we measure how fast an algorithm runs? -> Just the record the time it takes for a computer to do this thing.

There is a problem with just coding up an algorithm, telling a computer what to do, and timing how long it takes. Why? -> It depends on the stregth of your computer.

!!! Dont measure time, instead count fundamental operations(ops).

Expect performance to depend on size of our input. We usually use (n) for what the size of our input

- We have O(.) corresponds upper bound, ??(.) corresponds lower bounds and ??(.) corresponds to both.

- O(1): Constant Time, basically no matter how I change the input the amount of time, the performance of my algrithm takes, it does not really depend on that.

- O(log n): This is Logarithmic Time

- O(n) : Linear time

- O(n log n) : Log Linear

- O(n2) : Quadratic Running Time

- O(nc) : Polynomial Time, as long as c is some constant.

**FROM DOWN TO THE UP, THEY ARE MORE EFFICIENT(O(.)'s)**

![Time Complexity](https://miro.medium.com/max/1400/1*yiyfZodqXNwMouC0-B0Wlg.png)

### Model of Computation

**RAM ->** Random Access Memory, it means that I can randomly access different places in memory in constant time

**CPU ->** It can basically hold a small amount of information but it can change that information and it also has instructions to randomly access different places in memory bring it into the CPU, act on it and read it back. But we dont have an address for every bit in memory, every 0 and 1 in memory, What a modern computer is addressed in is bits, collections of bits, So there is an address I have every 8 bits in memory.So if I want to pull sth into the CPU I give it an address, it'll take some chunk, and bring it into the CPU, operate on it and spit it back. How big is thata chunk? -> 64 bits, that's how much i can operate on at a time.

- integer arithmetic
- logical operations
- bitwise operation , **those are the operations that available to me on most CPU's.**

## Lecture 2 - Data Structures and Dynamic Arrays

### Interface(API/ADT) vs. Data Structure

The idea is that an interface says what you want to do, a data structure says how you do it.

**Interface(API/ADT)**

- specipication
- what data can store
- what operations are supported what they mean
- problem

**Data Structure**

- representatiton
- how to data store
- algorithms to support operations
- solution

**Two main interfaces :**

- set
- sequence

**Two main data structure approaches:**

- arrays
- pointer based

#### Static Sequence Interface

**maintain a sequence of items x0,x1, x2, x3, xn-1 subject to these operations:**

- build(x) : make new DS for items in X
- length() : return n
- iter_seq(): output x0,x1,..., xn-1 in sequence order
- get_at(): return xi (index i)
- set_at(i,x) : set xi to x
- get_first/last()
- set_first/last(x)

**Solution(natural) of these interface :** Static Arrays

O(1) per get_at/set_at/len ops.

O(n) per build/iter_seq

**Memory Allocation Model :** allocate array of size n in ??(n) time

**Key :** word RAM model of computation

- memory : array of w-bit words
  ![w-bit](https://learnworthy.net/wp-content/uploads/2020/03/The-amazing-history-of-the-Data-Byte.png)

- "array" : consecutive chunk of memory

-> array[i] === memory[address(array)+ i ]

-> array access is O(1) time.

!!! Assume w >= lg n /// w : machine word size , in real computers this is currently 64

#### Dynamic Sequence Interface

**static sequence, plus :**

- insert_at(i,x) : make x the new xi, shifting xi -> xi+1 -> xi+2 ... -> xn-1->xn'-1(n': n+1) ----> |x0|x1|x2|x3|x4|...|x n-1| -- I wanna insert x to position 2 -- |x0|x1|x2=x|x3'(old x2)|x4'(old x3)|...|x n-1'|

!insert last changes anything but insert first changes all of them

- delete_at(i) : shift xi <- xi+1 <- ... <- xn'+1(n':n+1) <- xn-1

- insert/delete_fisrt/last(x)/()

### Linked List :

![linkedlist](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2013/03/Linkedlist.png)

#### Dynamic Sequence Operations Static Array vs. Linked List :

**static array**

- insert/delete_at() cost ??(n) time

  1.shifting
  2.allocation/ copying

!!!So static arrays are really bad for dyncamic ops. but we could do them.
!!! But they are good at get/set_at() ops.

**linked list**

- insert/delete_first() cost O(1) time
- get/set_at() need O(i) time and worst case O(n) time

!!! Efficient at insert/delete_at but not effcient get/set_at() ops

**!!! Linked lists are great if you are working on the ends even dynamically, Arrays are great if you are doing random access and nothing dynamic (adding or deleting)**

**Dynamic Arrays(python lists)**

- relax constraint size (array) = n <- # items in sequence
- enforce size = O(n)
- maintain A[i] = x
- insert_last(x) : add to end unless n = size
- if n = size allocate new array of size\*2
- n insert_last() from empty array resize at n=1, 2, 4, 8, 16... -> size cost = O(1+2+4+8+16+...+ n) = O(sum 2i) =O(2 lg n) = O(n)

**Amortization :** operations takes T(n) amortized time if any k operations take =< k T(n) time (averaging over operation sequence)

### Worst Cases O(.):

**array :** static(get_at(x), set_at(i,x))-> **1** -- Dynamic (insert_first(), delete_fisrt())-> **n** -- Dynamic (insert_last(), delete_last())-> **n** -- Dynamic (insert_at(), delete_at())-> n
**linked list :** static(get_at(x), set_at(i,x))-> **n** -- Dynamic (insert_first(), delete_fisrt())-> **1** -- Dynamic (insert_last(), delete_last())-> **n** -- Dynamic (insert_at(), delete_at())-> **n**
**dynamic array :** static(get_at(x), set_at(i,x))-> **1** -- Dynamic (insert_first(), delete_fisrt())-> **n** -- Dynamic (insert_last(), delete_last())-> **1(a)** -- Dynamic (insert_at(), delete_at())-> **n**

## Lecture 3 - Problem Session 1: Asymptotic Behavior of Functions and Double-ended...

![lecture-3](https://github.com/avahmetozdemir/MIT-6.006-Intro-to-Algorithms/blob/main/notes/notes-2.png?raw=true)

#### first-operation

**swap-ends(D)**

**Q:** Describe an algrithm to swap first and the last items

**A:**

    x1 = D.delete_first()
    x2 = D.delete_last()
    D.insert_front(x2)
    D.insert_last(x1)

#### second-operation

**shift_left(D,k)** kth item will be the last item and k+1 item become the first item

**A:**

    	if k < 1 or k > len(D) -1
    	return
    	x.delete_first()
    	D.insert_last()
    	shift_left(D,k-1) -recursive func.-

**Amortization:** You can do some work up front by making this thing make some of these operations faster. What amortization means is, if I have, say , a dynamic array where I'm going to be inserting things at the end, sometimes when I add sth, I'm gonna spent a lot of time to add that thing, I'm going to spend linear time. But what's the point of this data structure in the first place? The point is that I went to be able to potentially add a lot of things to this thing. Amortization is saying that, even though sometimes this operations will be bad, averaged over many operations, this is going to have a better running time. That's the amortization. Formally in amortized some amount of time -lets say k time- that means that if I do n operations, the total time it takes me to do all of those operations is not going to be more than n times k. So on average its gonna take me K time.

Amortization means that you have a usually a DS that you are operating on, and you are doing operations multiple times and you are getting a benefit, because you are doing that operations lots of times.

#### third-operation

![dynamic-arrays](https://media.geeksforgeeks.org/wp-content/uploads/darray.png)

#### fourth-operation

![linked-list](https://www.alphacodingskills.com/imgfiles/linked-list.PNG)

    1.Find nth node
    2.reverse next pointers of everything after nth
    3.cleans up ends

    (In video, this pseudo code is written on Python)

## Lecture 4 - Sets and Sorting

#### Review :

- Interface : Colletion of operations(e.g., sequence & set)
- Data Structure : Way to store data that supports a set of operations

### Set Interface :

#### Container

- build(A) | given an iterable A, build sequence from items in A
- len() | return the number of stored items

#### Static

- find(k) | return the stored item with key k

#### Dynamic

- insert(x) | add x to set(replace item with key x.key if one already exits)
- delete(k) | remove and return the stored item with key k

#### Order

- iter_ord() | return the stored items one-by-one in key order
- find_min()| return the stored item with the smallest key
- find_max() | return the stored item with largest key
- find_next(k) | return the stored item with smallest key larger than k
- find_prev(k) | return the stored item with largest key smaller than k

![operations](https://github.com/avahmetozdemir/MIT-6.006-Intro-to-Algorithms/blob/main/notes/notes-4.png?raw=true)

### Sorting Vocabulary:

- **Destructive :** Overwrites the input array
- **In place :** Uses O(1) extra space

**In :** Array of n numbers/keys - A
**Out :** Sorted Array - B

#### Permutation Sort :

    	def permutatiton_sort(A) :
    		'''Sort A'''
    		for B in permutatitons(A):
    			if is_sorted(B)
    				return B

- 1.Enumerute permutations ??(n!)
- 2.Check if the permutation is sorted O(n) (check list with this -> for i = 1 to n -1 B[i] =< B[i+1])

**--> ??(n! \* n)**

### Selection Sort Example :

- 1.Found biggest with index =< i
- 2.Swap
- 3.Sort 1,...,i-1

#### Helper Function for Selection Sort

    	def prefix_max(A, i)
    		'''Return index of maximum in A[:i+1]'''
    		if i>0
    			j = prefix_max(A,i-1)
    			if A[i] < A[j]
    			return j
    		return i

#### Selection Sort

    	def selection_sort(A,i = None) :
    		'''Sort A[:i+1] '''
    		if i is None: i = len(A) -1
    		if i > 0
    			j = prefix_max(A,i)
    			A[i], A[j] = A[j], A[i]
    			selection_sort(A, i - 1)

### Merge Sort Example:

    def merge_sort(A, a= 0, b=0)
    	''' Sort A[a:b] '''
    	if b is None: b = len(A)
    	if 1 < b-a:
    		c  = (a+b+1)//2
    		merge_sort(A, a,c)
    		merge_sort(A, c,b)
    		L, R = A[a:c], A[c:b]
    		merge(L,R,A, len(L), len(R), a,b)

#### Merge Function:

    	def merge(L,R,A,i,j,a,b):
    		'''Merge Sorted L[:i] and R[:j] into A[a:b]'''
    		if a < b
    			if(j =< 0) or (i > 0  and L[i-1 ] > R[j-1])
    				A[b -1] =L [i-1]
    				i = i -1
    			else :
    				A[b-1] = R[j-1]
    				j = j -1
    			merge(L,R,A,i,j,a,b-1)

- The array is initially divided into two equal halves and then they are combined in a sorted manner. We can think of it as a recursive algorithm that continuously splits the array in half until it cannot be further divided. This means that if the array becomes empty or has only one element left, the dividing will stop, i.e. it is the base case to stop the recursion. If the array has multiple elements, we split the array into halves and recursively invoke the merge sort on each of the halves. Finally, when both the halves are sorted, the merge operation is applied. Merge operation is the process of taking two smaller sorted arrays and combining them to eventually make a larger one.

## Lecture 5 - Hashing

- Prove that you can't find(k) faster than O(logn)
- Show how to find (k) faster than O(logn)

**Comparison Model :** The items,the objects I'm storing, I can kind of think of them as black boxes. I dont get to touch these things, except the only way that I can distinguish between them is to say , given a key and an item, or two items, I can do a comparison on these keys. Like are these keys the same? Is this key bigger than this one? -> =, < ,>, =< ,>=, != . There is only one thing that I can branch on. It's gonna branch two different lines. It's either true and I do some other computation, or it's false and I'll do a different set of computation.

![decision-tree](https://github.com/avahmetozdemir/MIT-6.006-Intro-to-Algorithms/blob/main/notes/decision-tree.png?raw=true)

**Why it needs n +1 leaves ? =>** If it's a correct algorithm it needs to be able to return any of the n items that I'm storing or say that the key I am looking for is not there.

**What is the minimum height of any binary tree that has at least n + 1 leaves ->** min height : ??(logn) (at least logn height)

**Direct Access Array :** | | | | | | | | | | 10th = x | | | | | x.key = 10

- we assume integer keys

![set-interface](https://github.com/avahmetozdemir/MIT-6.006-Intro-to-Algorithms/blob/main/notes/direct-access-array.png?raw=true)

![chaining](https://github.com/avahmetozdemir/MIT-6.006-Intro-to-Algorithms/blob/main/notes/chaining-.png?raw=true)

**Division hash function :**

h(k) = k mod m

**Universal hash function :**
hab(k) = (((ak+b) mod p) mod m)

    	H(p,m) = {hab(k)| a,b in {o, ... , p-1} and a != 0}

## Lecture 6 - Problem Session 2 (MIT 6.006 Introduction to Algorithms, Spring 2020)

### Problem 1-1. Solving recurrences

- Derive solutions to the following recurrences in two ways: via a recursion tree and via Master
  Theorem. A solution should include the tightest upper and lower bounds that the recurrence will
  allow. Assume T (1) 2 ???(1).

| Solution a-b                                                                                                                                       |                                                                    Solution b-c                                                                    |
| -------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------: |
| <img width="361" alt="lecture-6-1" src="https://github.com/avahmetozdemir/MIT-6.006-Intro-to-Algorithms/blob/main/notes/lecture-6-1.png?raw=true"> | <img width="361" alt="lecture-6-2" src="https://github.com/avahmetozdemir/MIT-6.006-Intro-to-Algorithms/blob/main/notes/lecture-6-2.png?raw=true"> |

### Problem 1-2. Stone Searching

- Sanos is a supervillain on an intergalactic quest in search of an ancient and powerful artifact called
  the Thoul Stone. Unfortunately she has no idea what planet the stone is on. The universe is
  composed of an in???nite number of planets, each identi???ed by a unique positive integer. On each
  planet is an oracle who, after some persuasion, will tell Sanos whether or not the Thoul Stone
  is on a planet having a strictly higher planet identi???er than their own. Interviewing every oracle
  in the universe would take forever, and Sanos wants to ???nd the Thoul Stone quickly. Supposing
  the Thoul Stone resides on planet k, describe an algorithm to help Sanos ???nd the Thoul Stone by
  interviewing at most O(log k) oracles.

**Solution:** First observe that if we could ???nd a planet with identi???er x > k that is not too much
larger than k (speci???cally, x = ???(k)), then we would be done, as binary searching the planets from
1 to x 1 would ???nd the value of k by visiting at most O(log x) = O(log k) oracles. It remains to
???nd such a planent x.
???
To ???nd x, instruct Sanos to visit planets 2 i starting at i = 0 until an orcale on planet x = 2 i
???rst tells Sanos that x > k. Since x is the ???rst planet for which 2 i > k, then x/2 < k and
???
x < 2k = ???(k) as desired. To reach planet x = 2 i , Sanos interviews i ??? = dlog 2 ke = ???(log k)
oracles, so to ???nd k, this algorithm interviews at most O(log k) oracles as desired.

### Problem 1-3. Collage Collating

- Fodoby is a company that makes customized software tools for creative people. Their newest
  software, Ottoshop, helps users make collages by allowing them to overlay images on top of each
  other in a single document. Describe a database to keep track of the images in a given document
  which supports the following operations:

      	1. make document() : construct an empty document containing no images
      	2. import image(x) : add an image with unique integer ID x to the top of the document
      	3. display() : return an array of the document???s image IDs in order from bottom to top
      	4. move below(x, y) : move the image with ID x directly below the image with ID y

Operation (1) should run in worst-case O(1) time, operations (2) and (3) should each run in worst-
case O(n) time, while operation (4) should run in worst-case O(log n) time, where n is the number
of images contained in a document at the time of the operation.

**Solution:** This database requires us to maintain a sequence of images ordered extrinsically, but also
support searching intrinsically for images based on their ID. So, we will implement the database
with a combination of both a sequence data structure, speci???cally a doubly linked list (as imple-
mented in PS1-4) storing image IDs, and a set data structure, speci???cally a sorted array storing
pairs (x, v x ) sorted by x values, where x is the ID of an image, and v x is a pointer to the linked list
node containing x.

To implement make document() , simply initialize an empty linked list L and an empty sorted
array S, each in O(1) time. There is no output to this operation, so it is trivially correct.
To implement import image(x) , add x to the front of L in node v x in O(1) time and add (x, v x )
to S in O(n) time. Delegating to these data structures ensures that x is added to front of the
sequence stored in L, and that S now contains (x, v x ) and remains sorted after insertion.
To implement display() , construct and return an array by iterating the items of L in sequence
order which can be done in O(n).

To implement move below(x, y) , use binary search to ???nd pairs (x, v x ) and (y, v y ) in S, each
in O(log n) time. Then we can remove node v x from L in O(1) time and insert it after node v y ,
also in O(1) time, by relinking pointers. For completeness, here is one way to relink the pointers
in a doubly linked list:

    	def relink(S, vx, vy):
    		if vx.prev: vx.prev.next = vx.next
    		else:     S.head = vx.next
    		if vx.next: vx.next.prev = vx.prev
    		else:   S.tail = vx.prev
    		vx.prev = vy
    		vx.next = vy.next
    		if vy.next: vy.next.prev = vx
    		else:    S.tail = vx
    		vy.next = vx

### Problem 1-4. Brick Blowing

Porkland is a community of pigs who live in n houses lined up along one side of a long, straight
street running east to west. Every house in Porkland was built from straw and bricks, but some
houses were built with more bricks than others. One day, a wolf arrives in Porkland and all the
pigs run inside their homes to hide. Unfortunately for the pigs, this wolf is extremely skilled at
blowing down pig houses, aided by a strong wind already blowing from west to east. If the wolf
blows in an easterly direction on a house containing b bricks, that house will fall down, along with
every house east of it containing strictly fewer than b bricks. For every house in Porkland, the wolf
wants to know its damage, i.e., the number of houses that would fall were he to blow on it in an
easterly direction.

- **(a)** Suppose n = 10 and the number of bricks in each house in Porkland from west to east
  is [34, 57, 70, 19, 48, 2, 94, 7, 63, 75] . Compute for this instance the
  damage for every house in Porkland.

**Solution:** [4, 5, 6, 3, 3, 1, 4, 1, 1, 1]

- **(b)** A house in Porkland is special if it either (1) has no easterly neighbor or (2) its adja-
  cent neighbor to the east contains at least as many bricks as it does. Given an array
  containing the number of bricks in each house of Porkland, describe an O(n)-time
  algorithm to return the damage for every house in Porkland when all but one house
  in Porkland is special.

**Solution:** Maintain an array D of the same size as the input array H to store updated
damages, where the i th item of D is an integer representing the number of damages
counted so far. To add damage to the i th house, add to the value at D[i] in O(1) time.
As each house will itself fall down when blown on, initialize every element of D to 1
in O(n) time, and count other damages using the following algorithm.

If exactly one house (say the h th house) in Porkland is not special, that means the
subarray A from the east-most house to h non-strictly monotonically increases, as
does the subarray B from the (h + 1) th house to the west-most house. We can ???nd
h in O(n) time via a linear scan. The damage for any house in subarray B is 1, as
no house to the west contains strictly fewer bricks, so these values are set correctly at
initialization.

It remains to compute the damage for the houses in A. Use a two-???nger algorithm
starting with one index i at the beginning of A (i = 0) and another index j at the
beginning of B (j = 0). Then repeat the following process until i = |A|: if j < |B|
and house A[i] has strictly more bricks than B[j], then increase j by 1; otherwise, add
j to the damage at D[i] and increase i by 1. This loop halts when i+j = |A|+|B| = n,
and i + j increases by one in each iteration. Since the work done in each iteration is
O(1), this algorithm runs in O(n) time.

To prove that this algorithm correctly computes the damage for each house in A we
???rst prove that the loop above maintains the invariant that at the start of each iteration,
A[i] > B[k] for all k 2 {0, . . . , j 1}. This property implies the algorithm computes
damage correctly for each house in A: the algorithm updates the damage for A[i] when
A[i] ??? B[j], so the claim implies the houses west of A[i] with strictly fewer bricks are
exactly the houses H = {B[k] | k 2 {0, . . . , j 1}} where |H| = j; so the damage
blowing on house A[i] is D[i] = j + 1 as recorded.

To prove the claim, we induct on i + j. When i + j = 0, the claim is vacuously true
as the set of possible k is empty. Now assume for induction that the claim holds for
some i + j. If A[i] > B[j], then increasing j by one directly maintains the invariant
since A[i] > B[k] for k 2 {0, . . . , j 1} by induction. Alternatively, if A[i] ??? B[j],
then increasing i by 1 also maintains the induction hypothesis since A[i + 1] > A[i],
proving the claim.

- **(c)** Given an array containing the number of bricks in each house of Porkland, describe
  an O(n log n)-time algorithm to return the damage for every house in Porkland.

Solution: We modify merge sort to record all damages that occur between houses
within each subarray before every merge. Since we will be moving brick values in H
from their original locations, we will replace each brick value b i = H[i] with tuples
H[i] = (b i , i), to keep track which house is associated with b i .

As in (b), initialize a damages array D to 1s. Then, recursively sort and record dam-
ages that would occur between houses in the ???rst half of H, and then do the same for
the second half. Next use the O(n)-time algorithm from part (b) to count the damages
that would occur between one house in the ???rst half and one house in the second half,
and then use the merge step of merge sort to combine the two sorted halves into one
sorted array in O(n) time. Since both (b) and merge take O(n) time, the recurrence
for this algorithm is the same as merge sort, yielding an O(n log n) running time.

Now we prove this algorithm correctly records the damage of every house in a given
subarray with any other house in the subarray (in addition to sorting the subarray), by
inducting on the size of the subarray. When the subarray has size 1, there is exactly
one damage between houses within that subarray, and the initialization step records
it. Alternatively, assume for induction that the claim is true for all k < n. By induc-
tion, the algorithm correctly records all damages between houses within the ???rst half
of the subarray, and also all damages between houses within the second half.
It remains to record damages between houses in the left half with houses on the right half.

Fortunately, since the ???rst and last halves of the subarray are sorted, the algorithm in
(b) counts exactly those damages. Then sorting using the merge step of merge sort
maintains the invariant as desired.

Note that the merge step and the algorithm in part (b) are both two ???nger algorithms
that traverse from the starts of the same two subarrays. Our implementation for (d)
utilizes this observation to record the damages with the merge step of merge sort,
rather than separately.

- **(d)** Write a Python function get damages that implements your algorithm.

**Solution:**

    	def get_damages(H):
    		D = [1 for _ in H]
    		H2 = [(H[i], i) for i in range(len(H))]
    			def merge_sort(A, a = 0, b = None):
    				if b is None:  b = len(A)
    				if 1 < b - a:
    					c = (a + b + 1) // 2
    					merge_sort(A, a, c)
    					merge_sort(A, c, b)
    					i, j, L, R = 0, 0, A[a:c], A[c:b]
    					while a < b:
    						if (j >= len(R)) or (i < len(L) and L[i][0] <= R[j][0]):
    							D[L[i][1]] += j
    							A[a] = L[i]
    							i += 1
    						else:
    							A[a] = R[j]
    							j += 1
    						a += 1
    		merge_sort(H2)
    		return D

## Lecture 7- Linear Sorting

**Last Time:**

- Comparison model => ??(logn) time to search
- Do faster using RAM and direct access array

  What was the problem with direct access array ? -> Space (much larger than n )

- Space O(u), reduce space via hash h(k) : u-> N

  How to fix that space problem? ->We can reduce the space by taking that larger key space from 0 to u, which could be very large, and map it down to a small space

- Expected O(1) time dictionary ops!

![hash-table](https://github.com/avahmetozdemir/MIT-6.006-Intro-to-Algorithms/blob/main/notes/lecture-7-hash-table.png?raw=true)

![sorting-algorithms](https://github.com/avahmetozdemir/MIT-6.006-Intro-to-Algorithms/blob/main/notes/lecture-7-sorting-algo.png?raw=true)

#### Comparison Model

![draw-1](https://github.com/avahmetozdemir/MIT-6.006-Intro-to-Algorithms/blob/main/notes/lecture-7-draw-1-1.png?raw=true)

**How could I use a direct access array to sort faster?**

Instantiate a big direct access array, I take each one of the items in the things that I am trying to sort, I look at each one of their keys and I stick it in the direct accessory exactly where it needs to go in constant time.

0 ---------k---------- (u-1) this algorithm takes O(n+u)

- make Dynamic Access Array -> O(u)
- store item x in index x.key -> n \* O(1)
- walk down Dynamic Access Array and return items seen in order -> O(u)

u = ??(n) => O(n)

![draw-2](https://github.com/avahmetozdemir/MIT-6.006-Intro-to-Algorithms/blob/main/notes/lecture-7-draw-2.png?raw=true)

![radix-sort](https://github.com/avahmetozdemir/MIT-6.006-Intro-to-Algorithms/blob/main/notes/lecture-7-radix-sort.png?raw=true)

## Lecture 8 - Problem Session 3

### Problem 3-2. Hash Sequence

Hash tables are not only useful for implementing Set operations; they can be used to implement
Sequences as well! (Recall the Set and Sequence interfaces were defined in Lecture and Recitation 02.) Given a hash table, describe how to use it as a black-box1 (using only its Set interface
operations) to implement the Sequence interface such that:

??? build(A) runs in expected O(n) time,
??? get at and set at each run in expected O(1) time,
??? insert at and delete at each run in expected O(n) time, and
??? the four dynamic first/last operations each run in amortized expected O(1) time.

**Solution:** To use a hash table H to implement the Sequence operations, store each Sequence item
x in an object b with key b.key and value b.val = x, and we will store these keyed objects in the
hash table. We also maintain the lowest key s stored in the hash table, to maintain invariant that
the n stored objects have keys (s, . . . , s + n ??? 1), where the i
th item in the Sequence is stored in
the object with key s + i.

To implement build(A), for each item xi in A = (x0, . . . , xn???1) construct its keyed object b,
initially with key b.key = i, in worst-case O(1) time; then insert it into the hash table using Set
insert(b) in expected O(1) time, for an expected total of O(n) time. Initializing s = 0 ensures
the invariant is satisfied.

To implement get at(i), return the value of the stored object with key s+i using Set find(s +
i) in expected O(1) time, which is correct by the invariant. Similarly, to implement set at(i,
x), find the object with key s + i using find(s + i) and change its value to x, also in expected
O(1) time.

To implement insert at(i, x), for each j from s + n ??? 1 down to s + i, remove the object b
with key j using delete(j) in expected O(1) time, change its key to j + 1 in worst-case O(1)
time, and then insert the object with insert(b) in expected O(1) time. Then, construct a keyed
object b0 with value x and key s + i, and insert with insert(b???) in expected O(1) time, for an
expected total of O(n) time. This operation restores the invariant for each affected item.
Similarly, to implement delete at(i), remove the object b0 stored at s + i with delete(s +
i) in expected O(1) time; then for each j from s+i+ 1 to s+n???1, remove the object b with key
j using delete(j) in expected O(1) time, change its key to j ??? 1 in worst-case O(1) time, and
then insert the object with insert(b) in expected O(1) time. Then return the value of object b0
,
for an expected total of O(n) time. This operation returns the correct value by the invariant, and
restores the invariant for each affected item.

To implement insert last(x) or delete last(), simply reduce to insert at(s + n) or
delete at(s + n - 1) in expected O(1) time since no objects need to be shifted.
To implement insert first(x), construct a keyed object b with value x and key s???1 and insert
it with insert(b) in expected O(1) time. Then setting the stored value of s to s ??? 1 restores the
invariant. Similarly for delete first(), remove the object with key s using delete(s) in
expected O(1) time, and return the value of the object. Then setting the stored value of s to s + 1
restores the invariant.

### Problem 3-3. Critter sort

Ashley Getem collects and trains Pocket Critters to fight other Pocket Critters in battle. She has
collected n Critters in total, and she keeps track of a variety of statistics for each Critter Ci. Describe efficient2 algorithms to sort Ashley???s Critters based on each of the following keys:

**(a) Species ID: an integer xi between ???n and n (negative IDs are grumpy)**

**Solution:** These integers are in a linearly bounded range, but are not positive. So
take worst-case O(n) time to add n to each critter???s ID so that xi ??? 2n = u for all i,
sort them using counting sort in worst-case O(n+2n) = O(n) time, and then subtract
n from each ID, again in worst-case O(n) time.

**(b) Name: a unique string si containing at most 10dlg ne English letters**

**Solution:** We do not know whether all si ??? S are polynomially bounded in n; but we
do know that h is. If some si ??? h, it can certainly not be part of a pair of positive side lengths from S that sum to under h. So first perform a linear scan of S and remove all
si ??? h to construct set S0
. Now the integers in S0 are each upper bounded by O(n6),
so we can sort them in worst-case O(n + n logn n6) time using radix-sort, and store
the output in an array A.
Now we can sweep the sorted list using a two-finger algorithm similar to the merge
step in merge sort to find a pair with the largest sum at most h, if such a pair exists. Specifically, initialize indices i = 0 and j = |S0
| ??? 1, and repeat the following procedure, keeping track of the largest sum t found so far initialized to zero.
If A[i] + A[j] ??? h, then if t < A[i] + A[j], you have found a better pair, so set
t = A[i] + A[j]; regardless A[k] + A[j] < t for all k ??? i, so increase i by one. Otherwise if A[i] + A[j] > h, then A[i] + A[`] > h for all ` ??? j, so decrease j by one. If j < i (or j = i and we want distinct si, sj ), then return False. This loop maintains the invariant that at the start of each loop, we have confirmed that A[k] + A[`] ??? t
for all k ??? i ??? j ??? ` for which A[k] + A[`] ??? h, so the algorithm is correct. Since
each iteration of the loop takes O(1) time and decreases j ??? i decrease by one, and
j ??? i = |S0
| ??? 1 starts positive and ends when j ??? i < 0, this procedure takes at most
O(n) time in the worst case.

### Problem 3-5. Po-k-er Hands

Meff Ja is a card shark who enjoys playing card games. He has found an unusual deck of cards,
where each of the n cards in the deck is marked with a lowercase letter from the 26-character
English alphabet. We represent a deck of cards as a sequence of letters, where the first letter
corresponds to the top of the deck. Meff wants to play a game of Po-k-er with you. To begin the
game, he deals you a Po-k-er hand of k cards in the following way:

1. The deck D starts in a pile face down in a known order.
2. Meff cuts the deck uniformly at random at some location i ??? {0, . . . , n ??? 1},i.e., move the top i cards in order to the bottom of the deck.
3. Meff then deals you the top k cards from the top of the cut deck.
4. You sort your k cards alphabetically, resulting in your Po-k-er hand.

Let P(D, i, k) be the Po-k-er hand resulting from cutting a deck D at location i. Then cutting
deck D = ???abcdbc??? at location 2 would result in the deck ???cdbcab???, which would then yield
the Po-4-er hand P(D, 2, 4) = ???bccd???. From a given starting deck, many hands are possible
depending on where the deck is cut. Meff wants to know the most likely Po-k-er hand for a given
deck. Given that the most likely Po-k-er hand is not necessarily unique, Meff always prefers the
lexicographically smallest hand.

**(a)** Describe a data structure that can be built in O(n) time from a deck D of n cards and
integer k, after which it can support same(i, j): a constant-time operation which
returns True if P(D, i, k) = P(D, j, k) and False otherwise.

**Solution:** We build a direct access array mapping each index i ??? {0, . . . , n ??? 1} to
a frequency table of the letters in hand P(D, i, k), specifically a direct access array
A of length 26 where A[j] corresponds to the number of times the (j + 1)th letter
of the English alphabet occurs in the hand. The frequency table of hand P(D, 0, k)
can be computed in O(k) time by simply looping through the cards in the hand and
adding them to the frequency table. Then given the frequency table of P(D, i, k), we
can compute the frequency table of P(D, i + 1, k) in constant time by subtracting one
from letter D[i] and adding one to letter D[i + k]. Building the above hash table then
takes O(k) + nO(1) = O(n) time. To support same(i, j), look up indices i and j
in the direct access array in constant time. If the corresponding frequency tables are
the same, then the hands must also match. We can check if they match in worst-case
constant time since each frequency has constant length (i.e., 26), so this operation
takes worst-case O(1) time. Students my use a hash table to achieve expected O(1)
time.

**(b)** Given a deck of n cards, describe an O(n)-time algorithm to find the most likely Po-ker hand, breaking ties lexicographically. State whether your algorithm???s running time is worst-case, amortized, and/or expected.

**Solution:** Build the data structure from part (a) in worst-case O(n) time, specifically
a direct access array of hand frequency tables. Now, compute the frequency of each
hand directly: loop through the direct access array and add each hand frequency table
to a hash table T mapping to value 1; if a hand table h already exists in T, increase
T[h] by 1. This procedure performs one hash table operation for each of the n hand
tables, so it runs in expected O(n) time. Next, find the largest frequency of any hand
directly by looping through all hands in T, keeping track of f the largest frequency
seen in worst-case O(n) time. Then, construct a list of hand tables with frequency
f directly by looping through all hands in T again, appending to the end of a dynamic array A every hand table that has frequency f, also in worst-case O(n) time.
The lexicographically first hand will be the one whose hand frequency table is lexicographically last (e.g., (1,0,...)>(0,1,...) but ???a...???<???b...???), so loop
through the hand tables and keep track of the lexicographically last hand table t in
worst-case O(n) time. Lastly, convert hand table t back into a hand by concatenating
k letters in order based on their frequency in worst-case O(k) time, and then return
the hand. Then in total, this procedure runs in expected O(n) time.

We can reduce to worst-case O(n) time using radix sort instead of a hash table to
count the frequencies of hand tables. Namely, we apply tuple/radix sort to the data
structure from part (a). Each hand frequency table consists of 26 numbers between 0
and n, so we can treat them as a base-(n + 1) integer of 26 digits. Sorting by each
digit from least to most significant, we put the hand frequency tables into lexically increasing order. Now a single scan through the array, at each step checking whether the
hand frequency table matches the previous, lets us compute the frequency of each table. A scan of these occurrence frequencies lets us find the maximum frequency f, and
another scan of the array lets us find the lexicographically last hand with frequency f.

## Lecture 9 - Binary Trees, Part 1

### Today :

- binary tree & traversal order
- subtree ops: first, successor, insert, delete
- set binary tree(Binary Search Tree = BST)
- sequence binary tree via subtree size augmentation

![data-structures](https://github.com/avahmetozdemir/MIT-6.006-Intro-to-Algorithms/blob/main/notes/data-structures.png?raw=true)

### What is Binary Tree ?

![binary-tree](https://upload.wikimedia.org/wikipedia/commons/5/5e/Binary_tree_v2.svg)

![binary-tree-pointers](https://bournetocode.com/projects/AQA_A_Theory/pages/img/binaryTreeSimple.png)

![binary-note-1](https://github.com/avahmetozdemir/MIT-6.006-Intro-to-Algorithms/blob/main/notes/binary-note.png?raw=true)

![subtree-ops](https://github.com/avahmetozdemir/MIT-6.006-Intro-to-Algorithms/blob/main/notes/subtree-opss.png?raw=true)

**Sequence:**
trav. order = sequence order

**Set:**
trav order = increasing item.key
find(k)
