---
layout: post
title: Getting Started With Recursion
author: Soham Mukerjee
date: '2017-06-26'
comments: true
---

      				RECURSION

When we come across the term recursion it might seem very interesting as well as difficult.. Well yes and yes. :p. But with practice comes perfection. Now we will start off by defining what are recurrence relations.
Def: A recurrence relation is the relation that depends on itself.
Now what was that? We have come across functions like f(x)=2*x , f(x,y)=x+y
Well recursion is not much different. Here function f is written in terms of itself.
One simple example can be, f(x)=f(x-1). Well clearly its solution is f(x)=f(0).
Let us start with another simple yet very important recurrence relation.  The Fibonacci numbers.
As we know nth term of Fibonacci sequence is sum of its (n-1)th term and (n-2)th term. Let f be a function that generates a Fibonacci number. Then clearly by definition, f(n)=f(n-1)+f(n-2). Okay so are we done? No. One most important thing mandatory for every recurrence relation is base cases. These are the stopping condition for a recurrence relation. Base cases are usually the ones that we can manually solve without any or a little effort. Here base cases will be f(0)=f(1)=1. 
But does recursion always means top-down? That is we calculate the value of function for some greater value of parameters/arguments from smaller ones? The answer is no. We calculate function values for a state which will be difficult to calculate otherwise from a state which we can easily calculate provided the value of function at any state depends on the same function at some previous state..
Now let us start thinking recursively.
We must have heard about basic combination formula  nCr=n!/((n-r)!r!).
We also might have come across the recurrence relation nCr=(n-1)Cr+(n-1)C(r-1).
Now how did we get it? Ofcourse we can start by expanding RHS and then forming LHS. But had we not known the formula beforehand is there a way to find the formula. Yes definitely. By LOGIC!
Well lets first focus on the definition of nCr. It is how many ways we can choose r objects out of n objects. Now consider the nth object. We can either choose this object or not. So if we choose the nth object we are left with n-1 objects and need to choose r-1 objects out of them which is basically (n-1)C(r-1). Now if we dont choose the nth object we are left with (n-1) objects and we have to choose r objects out of them which is nC(r-1). Therefore nCr=(n-1)C(r-1)+nC(r-1) as we can do nothing else with the nth object. Thus we successfully found the Combination Recurrence relation.
Now its time to increase our level of thinking. Lets consider another classic problem The Tower Of Hanoi.
<script src="http://ideone.com/e.js/3MeMfp" type="text/javascript" ></script>
     			THE TOWER OF HANOI
The problem states that there are 3 pegs A,B,C. Initially there are n disks placed on peg A in increasing order of dimension that is the disk with lowest radius at top and the disk with highest radius at bottom. Our task is to move all the disks from peg A(source)  to peg C(destination)  using peg B(auxiliary peg) following 2 rules:
1. We can move only one disk at a time.
2. A smaller disk must be always placed over a larger disk.
So how can we do it? The problem seems pretty complex isnt it? But the solution becomes very simple with recursion.
First we have all disks at peg A. Let us define a move using a function f(n,a,b,c).
Here we can explain what is a move using a simple example. Let n=1, a=A, b=B ,c=C. Then f(1,A,B,C) means moving 1 disk from A to C using B. Thus f(n,a,b,c) means moving n disks from a to c using b. Let us find answers to some smaller instances first. What is ans of f(1,A,B,C)? It prints disk is moved from A to C as when we have 1 disk we just move it to C.
What will f(2,A,B,C) print then? We first move the topmost disk to B. Then move the next disk to C. Then move the smaller disk from B to C. You can easily see no other smaller way is possible satisfying the given conditions.
So we have got the basic idea. Move the smaller disks to B. Then move the larger disk to C. Then move the smaller disks on top of it.. We are done!! :p
First of all you need to trust that f will always be true for smaller instances. Then use it as our advantage and find a formula for larger instance. It seems more like Principle Of Mathematical Induction isnt it? Yes infact the basic theory of recursion is based on induction.
So we assume the f we defined for Hanoi problem which depicts a move to be true for all values <n. And then we use it to find for n. So our task is to move all disks upto (n-1) to B using C from A. We know f is true for all values <n. So the answer to this will be simply f(n-1,A,C,B). Now we move nth disk(largest) from A to C. The we move the remaining disks from B to C using A. This is simply f(n-1,B,A,C).
The pseudo code for Tower Of Hanoi problem is:
  TowerOfHanoi(n,a,b,c){
If n=0
Return //base case
TowerOfHanoi(n-1,a,c,b)
Print move disk from a to c
TowerOfHanoi(n-1,b,a,c)
}
Here when n=0 we have no disk left so we dont perform any move.
Now we will take up yet another complicated but very common problem the coin change problem.
  				THE COIN CHANGE PROBLEM
The problem states that you are given a set of coins of worth coin[i]. Count of each coin is infinite. That is suppose coin[i]=2 for some i. Then you have infinite supply of coins of value 2. You are also given a required value K. Find how many ways u can get a value K using these coins.
As you have reached so far I can expect you to try solving this yourself before seeing the solution.
Now suppose f is a function that returns answer to this problem. That is f(n,K) returns how many ways you can form a value K using infinite supply of n coins each having worth coin[i]. Now suppose we are at the nth coin. We have 2 choices. Either include it to form K. Or exclude it.
If you include it you are left with n coins (WHY?) and you need to form a value K-coin[n].
If you exclude it you are left with n-1 coins and need to form a value K.
So f(n,K)=f(n,K-coin[n])+f(n-1,K)
Now lets think of base cases. Suppose you have reached K.Then you have successfully found 1 combination to form K. Therefore, f(n,0)=1 for all n.
Now suppose you have exceeded K. Means this is a wrong combination you have chosen as it can never form K from here as all coins have positive value. Therefore f(n,>K)=0.
Now suppose you have run out (WHY?)of all coins. Then you again cant reach K. Therefore f(0,K)=0.
Pseudocode:

Coinchange(n,k)
{
If n=0
Return 0
If k>K
Return 0
If k==0
Return 1
Return Coinchange(n-1,k)+Coinchange(n,k-coin[n])



You can get more problems from geeksforgeeks.com under Dynamic Programming Category