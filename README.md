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

Assume Inductive Hypothesis true for k = k'  { if k' contains match -> already returned by Inductive

												else if k'+1 contains match by Inductive algorithm k'+1 against all students }

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