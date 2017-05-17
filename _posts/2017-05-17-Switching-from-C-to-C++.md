---
layout: post
title: "Switching from C to C++"
date: 2017-05-17
---

Before we even begin, let's get our hands dirty. Say we are given to sort an array of strings. Here's what we could achieve with a program in C :

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