---
title: Switching from C to C++
layout: post
comments: true
date: '2017-05-18'
---

Before we even begin, let's get our hands dirty. Say we are given to sort an array of strings. Here's what one could achieve with a program in C :

{% highlight c linenos %}
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int comparator (const void *a, const void *b) { 
    const char **ia = (const char **)a;
    const char **ib = (const char **)b;

    return strcmp (*ia, *ib);
} 

void print_sorted_stringarray (char **array, int len) { 
    int i;
    for(i = 0; i < len; ++i) 
        printf("%s | ", array[i]);

    putchar('\n');
} 

int main () {
    /*array to be sorted*/
    char *s[] = {"Alexia", "Celine", "Alex", "Billie", "Forest", "Bill"};

    /*sort the strings*/
    qsort (s, 6, sizeof (char *), comparator);

    /*print the sorted array*/
    print_sorted_stringarray (s, 6);

    return 0;
}
{% endhighlight %}

Creepy, isn't it?
In C++, this is as simple as :

{% highlight cpp linenos %}

#include <iostream>
#include <string>
#include <algorithm>

using namespace std;

void print_sorted_stringarray (string s[], int len) { 
    for(int i = 0; i < len; ++i) 
        cout << s[i] << " | "; 
    
    cout << '\n';
} 

int main () {
    /*array to be sorted*/
    string s[] = {"Alexia", "Celine", "Alex", "Billie", "Forest", "Bill"};

    /*sort the strings*/
    sort (s, s + 6);

    /*print the sorted array*/
    print_sorted_stringarray (s, 6);

    return 0;
}

{% endhighlight %}


If you are unfamiliar with the library function **qsort()** you might want to peep into [this](http://www.geeksforgeeks.org/comparator-function-of-qsort-in-c/) or [this](https://www.tutorialspoint.com/c_standard_library/c_function_qsort.htm). It's not needed for now though. The C++ [sort()](http://www.cplusplus.com/reference/algorithm/sort/) function defined in the header **<<algorithm>>** is much easier to use in comparison.  
Also notice how the C++ [string](http://www.cplusplus.com/reference/string/string/) type replaces the more complicated **char*** or a **char[]** type that is normally used to represent a string in C.    

One no longer needs to specify the type when writing to the standard output as one did while using printf. Writing something like this would do:  
{% highlight cpp %}
  
	int a = 10, b = 20;
	cout << a << ' ' << b;
  
{% endhighlight %}  
Likewise, cin can be used to read values from the standard input in place of scanf.  
{% highlight cpp %}
  
	int a, b;
	cin >> a >> b;
  
{% endhighlight %}  
[Learn more about Basic I/O in C++....](http://www.cplusplus.com/doc/tutorial/basic_io/)  
    
Let's look at this line:   
{% highlight cpp %}
  
	using namespace std;
  
{% endhighlight %}  
This tells the compiler that the namespace **std** is intended for use. Let's not dig into **namespaces** in a simple blog post. Only thing, without this line, one would need to replace **string** with **std::string**.  


Though one might be knowing that these two languages are syntactically similar to each other, one might come across something fancy from time to time (or ***code to code***). Take this snippet for instance:  
{% highlight cpp %}
  
  	int year;
  	cin >> year;
	/*check for a leap year*/
	if ((year % 4 == 0 and year % 100 != 0) or year % 400 == 0)
		cout << "Leap year!";
	else
		cout << "Not a leap year";
  
{% endhighlight %}   
One can actually use the pythonic **and**, **or** and **not** instead of the punctuations.   


Here's how a [singly linked list](https://en.wikipedia.org/wiki/Linked_list) can be built from a C++ [string](http://www.cplusplus.com/reference/string/string/):  
{% highlight cpp linenos %}

#include <iostream>
using namespace std;

struct Node {
    char data;
    Node *next;
    Node (char data = 0) {
        this->data = data;
        next = NULL;
    }
};

bool BuildList (Node **head, string s) {
    Node *temp = *head;
    for (int i = 0; i < s.size(); ++i) { 
        if (!i) {
            *head = new Node (s[i]);
            temp = *head;
            continue;
        }
        temp->next = new Node (s[i]);
        temp = temp->next;
    }
    return true;
}

bool PrintList (Node *head) {
    Node *temp = head;
    while (temp) {
        cout << temp->data << ' ';
        temp = temp->next;
    }
    cout << '\n';
    return true;
}

int main() {
    string s = "2b || ! 2b";
    Node *ListHead = NULL;
    BuildList (&ListHead, s);
    PrintList (ListHead);
    return 0;
}
  
{% endhighlight %} 

While builing a linked list in C, one had to write a routine that would ***make*** a node, i.e., allocate memory to a node and then make its next pointer point to NULL. The **Node()** method does this for us here. Whenever a new node is created, this method is invoked at runtime. The **new Node()** instruction returns a pointer to the block of memory allocated [dynamically](http://www.cplusplus.com/reference/new/operator%20new[]/) by it.  

C++ has built in functionalities for using data structures like lists, stacks, queues, heaps and so on. These are popularly known as [STL containers](http://www.cplusplus.com/reference/stl/).   

{% highlight cpp linenos %}

#include <iostream>
#include <list>
using namespace std;

int main () {
    list <char> mylist;
    string s = "2b || ! 2b";
    /*insert items in mylist*/
    for (int i = 0; i < s.size(); ++i)
        mylist.push_back (s[i]);
    /*iterate over list items*/
    list <char>::iterator it = mylist.begin();
    for (it = mylist.begin(); it != mylist.end(); ++it)
        cout << *it << ' ';
    return 0;
}

{% endhighlight %}
As one can deduce, the [iterator](http://www.cplusplus.com/reference/iterator/) is a pointer to any of the container elements.  

**NOTES**
* The main [reason](http://objectorientedprogrammingcpp.blogspot.in/2010/01/how-c-programming-language-came-into.html) C++ came into existence was to introduce [abstraction](https://www.tutorialspoint.com/cplusplus/cpp_data_abstraction.htm).   
* C++ is an **object oriented programming** language. Classes and objects facilitate other programming paradigms such as **polymorphism**.   
* One must not confuse the c strings to c++ library strings. They have different signatures and routines defined for them have different functionalities and time complexities.  

**RESOURCES to Learn C++ From** 
* C++ Primer, 5th Edition by Stanley B. Lippman, Josée Lajoie, Barbara E. Moo  
* The C++ Programming Language by Bjarne Stroustrup
* Bjarne Stroustrup - The Essence of C++  
<iframe width="560" height="315" src="https://www.youtube.com/embed/86xWVb4XIyE" frameborder="0" allowfullscreen></iframe> 
* [Hackerrank](https://www.hackerrank.com/domains/cpp/cpp-introduction) can serve as a good platform to kick off practising. 
* [TutorialsPoint](https://www.tutorialspoint.com/cplusplus/)  
* [LearnCPP](http://www.learncpp.com/)  
* To start with [STL in Competitive Programming](https://www.topcoder.com/community/data-science/data-science-tutorials/power-up-c-with-the-standard-template-library-part-1/)