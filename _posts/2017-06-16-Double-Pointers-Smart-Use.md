---
layout: post
title: Smart Usage of Double Pointers
author: Zeeshan Amjad
date: '2017-06-16'
comments: true
---

So what's in a double pointer? It's just a pointer to a pointer. We're done.  
😋    
Since a pointer is a variable that contains the address of some other variable, a double pointer contains the address of a pointer variable.  

{% highlight cpp linenos %}
int x = 10;
int *a = &x;
int **b = &a;
cout << a << ' ' << b << ' ' << *a << ' ' << *b << ' ' << **b << '\n';
{% endhighlight %}

To understand the output, here's how these quantities could be roughly mapped in memory:  

<img src="images/Double-Pointers-Smart-Use/Node.png">

Now we can relate the results we get on dereferencing the variable **b** once and twice.  


Now given the address of a variable which points to some other variable, we can write more flexible code. In a part of this video Linus Torvalds hints at how someone who knows how to utilise the double pointer can flexibly remove a node from a singly linked list in mere 2 lines of code, without dealing separately with the case in which the head of the list needs to be removed.

<iframe width="560" height="315" src="https://www.youtube.com/embed/o8NPllzkFhE?rel=0" frameborder="0" allowfullscreen></iframe>  

Let's follow up on this thought using the singly linked list 0 --> 1 --> 2.

<img src="images/Double-Pointers-Smart-Use/LinkedList.png">  

{% highlight cpp linenos %}
struct Node {
    int data;
    Node *next;
};
{% endhighlight %}

The head pointer (address: 0x887) points to the first node in the list. The last node in the list (address: 0x708) has its next pointer pointing to NULL (0x000).  

Deleting a node simply requires changing the next pointer of the previous node. Since the head node of the list does not have a previous node, deleting it requires special care. But not when we have the address of the head pointer.

{% highlight cpp linenos %}
void deleteNode (Node **walk, int key) {
    /*
        perform action
    */
}

int main () {
    /*       */
    deleteNode (&head, 1);
    /*       */
}
{% endhighlight %}  

When the method deleteNode() is called, the variable **walk** which is local to the called method has the address of the head pointer of the list (0x887 in this case).

<img src="images/Double-Pointers-Smart-Use/walk.png">  

Here are the values we are going to store in **walk** while iterating through the list:  
At iteration 1, walk = 0x887.  
At iteration 2, walk = 0x304.  
At iteration 3, walk = 0x174.  
At iteration 4, walk = 0x712.  
We intend **walk** to store the address of the next pointers of the node. Hence, if we want to delete the node with key '1', we need to store the value 0x708 at the address 0x304 (address of the previous pointer of node with key '1'). Simple!  

But what if we had to delete the first node? Then we need only change **walk** to store **0x170** (address of the second node).

{% highlight cpp linenos %}
void deleteNode (Node **walk, int key) {
    while ((*walk)->data != key)
        walk = &((*walk)->next);
    *walk = (*walk)->next;
}
{% endhighlight %}  

Notes:  
1. Address of a variable **a** is given by **&a**.
2. **a->next** is equivalent to writing **(*a).next**.  
3. The phrase **'points to'** is analogous to **'contains the address of'**.  


That's it! This can handle all cases we have. At each iteration we check whether the node that **walk** points to is the target node. If this is true we stop and make the final change, else we continue with the iteration described above.  

**Exercise:** Remove duplicates from a sorted linked list.  
**Function Signature:** void deleteDuplicates (Node **head);

*Also, trace what happens when we have only one node in the list, and that needs to be deleted.*  

That's all folks, **CHEERS! 😃**
