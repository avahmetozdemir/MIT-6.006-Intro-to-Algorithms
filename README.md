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

Assume Inductive Hypothesis true for k = k'  { if k' contains match -> already returned by Inductive else if k'+1 contains match by Inductive algorithm k'+1 against all students }

#### Efficiency

Efficiency just means not only how fast does this algorithm run, but how fast does it compare to other possible ways of approaching this problem

So how could we measure how fast an algorithm runs? -> Just the record the time it takes for a computer to do this thing. 

There is a problem with just coding up an algorithm, telling a computer what to do, and timing how long it takes. Why? -> It depends on the stregth of your computer. 

!!! Dont measure time, instead count fundamental operations(ops).

Expect performance to depend on size of our input. We usually use (n) for what the size of our input 

- We have O(.) corresponds upper bound, Ω(.) corresponds lower bounds and θ(.) corresponds to both. 

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

**CPU ->** It can basically hold a small amount of information but it can change that information and it also has instructions to randomly access different places in memory bring it into the 		CPU, act on it and read it back. But we dont have an address for every bit in memory, every 0 and 1 in memory, What a modern computer is addressed in is bits, collections of bits, 	  So there is an address I have every 8 bits in memory.So if I want to pull sth into the CPU I give it an address, it'll take some chunk, and bring it into the CPU, operate on it and 	   	  spit it back. How big is thata chunk? -> 64 bits, that's how much i can operate on at a time. 

- integer arithmetic
- logical operations
- bitwise operation , **those are the operations that available to me on most CPU's.** 

## Lecture 2 - Data Structures and Dynamic Arrays

### Interface(API/ADT)  vs. Data Structure 

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

**maintain  a sequence of items x0,x1, x2, x3, xn-1 subject to these operations:**

- build(x) : make new DS for items in X
- length() : return n
- iter_seq(): output x0,x1,..., xn-1 in sequence order
- get_at(): return xi (index i)
- set_at(i,x) : set xi to x 
- get_first/last()
- set_first/last(x)

**Solution(natural) of these interface :** Static Arrays

O(1) per  get_at/set_at/len ops. 

O(n) per build/iter_seq

**Memory Allocation Model :** allocate array of size n in θ(n) time  

**Key :** word RAM model of computation 

- memory : 	array  of w-bit words 
![w-bit](https://learnworthy.net/wp-content/uploads/2020/03/The-amazing-history-of-the-Data-Byte.png)

- "array" : consecutive chunk of memory

-> array[i] === memory[address(array)+ i ]

-> array access is O(1) time. 

!!! Assume w >= lg n  /// w : machine word size , in real computers this is currently 64 

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

- insert/delete_at() cost θ(n) time  

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
- enforce size  = O(n) 
- maintain  A[i] = x
- insert_last(x) : add to end unless n = size
- if n = size allocate new array of size*2
- n insert_last() from empty array resize at n=1, 2, 4, 8, 16...  -> size cost  = O(1+2+4+8+16+...+ n)  =  O(sum 2i)  =O(2 lg n) = O(n)

**Amortization :** operations takes T(n) amortized time if any k operations take =< k T(n) time (averaging over operation sequence)

### Worst Cases O(.): 

**array :** static(get_at(x), set_at(i,x))-> **1** -- Dynamic (insert_first(), delete_fisrt())-> **n** --  Dynamic (insert_last(), delete_last())-> **n** -- Dynamic (insert_at(), delete_at())-> n
	
**linked list :** static(get_at(x), set_at(i,x))-> **n** -- Dynamic (insert_first(), delete_fisrt())-> **1** --  Dynamic (insert_last(), delete_last())-> **n** -- Dynamic (insert_at(), delete_at())-> **n**
	
**dynamic array :** static(get_at(x), set_at(i,x))-> **1** -- Dynamic (insert_first(), delete_fisrt())-> **n** --  Dynamic (insert_last(), delete_last())-> **1(a)** -- Dynamic (insert_at(), delete_at())-> **n**

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


**shift_left(D,k)**  kth item will be the last item and k+1 item become the first item

**A:** if k < 1 or k > len(D) -1 
		return

		x.delete_first()
		D.insert_last()
		shift_left(D,k-1) -recursive func.-

**Amortization:** You can do some work up front by making this thing make some of these operations faster. What amortization means is, if I have, say , a dynamic array where  I'm going to be inserting things at the end, sometimes when I add sth, I'm gonna spent a lot of time to add that thing, I'm going to spend linear time. But what's the point of this data structure in the first place? The point is that I went to be able to potentially add a lot of things to this thing. Amortization is saying that, even though sometimes this operations will be bad, averaged over many operations, this is going to have a better running time. That's the amortization. Formally in amortized some amount of time -lets say k time- that means that if I do n operations, the total time it takes me to do all of those operations is not going to be more than n times k. So on average its gonna take me K time. 

Amortization means that you have a usually a DS that you are operating on, and you are doing operations multiple times and you are getting a benefit, because you are doing that operations lots of times. 

#### third-operation

![dynamic-arrays](https://media.geeksforgeeks.org/wp-content/uploads/darray.png)

#### fourth-operation

![linked-list](https://www.alphacodingskills.com/imgfiles/linked-list.PNG)

	1.Find nth node
	2.reverse next pointers of everything after nth
	3.cleans up ends 

	(In video, this pseudo code is written on Python)

