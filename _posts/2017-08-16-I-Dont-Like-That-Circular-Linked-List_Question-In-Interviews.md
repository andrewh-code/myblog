---
layout: post
title: I Don't Like That Circular Linked List Question in Interviews
---

I remember back in school, one of the most revered questions we had to think about was detecting whether or not a linked list was circular or if it had a loop in it aka if it had a cycle in it. It was hard enough trying to learn and understand what a linked list was. To many of us, it was a pretty foreign concept and so much harder to understand compared to arrays. That, or maybe my professor was shit when it came to teaching us the intermediate aspects of programming.


I’ve seen this question come up many times in interviews I have partaken and I have read through so many stories of where students interviewing for co-op/summer placements or new grad positions get asked this question so many times. It’s a good question to ask developers in interviews because it can gauge how well your knowledge and understanding of linked lists is because you have to take into account extra things with linked lists that arrays don’t have. Unfortunately though there is pretty much only one answer to this question and that’s using [Floyd’s cycle detection algorithm](https://en.wikipedia.org/wiki/Cycle_detection) or more commonly known as the Tortoise and the Hare algorithm.


If you don’t know how to answer this question, here it is (which is taken from this [stack overflow post](https://stackoverflow.com/questions/2663115/how-to-detect-a-loop-in-a-linked-list/2663147#2663147):


{% highlight java %}
boolean hasLoop(Node first) {

    if(first == null) // list does not exist..so no loop either
        return false;

    Node slow, fast; // create two references.

    slow = fast = first; // make both refer to the start of the list

    while(true) {

        slow = slow.next;          // 1 hop

        if(fast.next != null)
            fast = fast.next.next; // 2 hops
        else
            return false;          // next node null => no loop

        if(slow == null || fast == null) // if either hits null..no loop
            return false;

        if(slow == fast) // if the two ever meet...we must have a loop
            return true;
    }
}
{% endhighlight %}


Since there’s pretty much only one accepted answer to this kind of question, is it really worth it to ask in an interview? I mean, now a days, people just memorized the algorithm just like how they’ve memorized how to create a for loop — it’s easy now. The interviewee will literally just need to explain the tortoise and hare algorithm or just say it and they’ll get full marks. But what if the interviewee was never taught this type of algorithm. You’re going to give them five minutes to answer the question? It took how long for Robert Floyd to develop this algorithm? This guy was a PhD right? I bet you it took him more than five minutes to figure out this algorithm and this is coming from a computer science legend. How long do you think a college/university student take to develop their own algorithm to find a loop in a linked list? I bet you if you gave them the time, it would take probably about four years, enough for them to write a PhD thesis on it.


Anyways, even though this question can be used as a basic filter for interviewees, it’s not a great one. I think fizz-buzz is a much better question to ask than this question. How would you make this better though, in terms of gauging their understanding of linked lists and detecting loops? Obviously you can ask follow up questions. My favourite follow up question was one that threw me off guard; usually no student would think about this when they first learn the algorithm. The question is:


*__When would you use the tortoise and hare algorithm or when would you need to check to see if there was a loop/cycle in a linked list (doesn’t matter if the linked list was a singly or doubly linked list)?__*



So everyone learns about this algorithm but how many actually stopped to think, why would this algorithm need to be created? Why did Floyd spend so many years trying to develop and prove this algorithm? There has to be a use case for this. Ask this to any software developer and I bet that a lot of them wouldn’t be able to answer this question correctly.


    - Andrew