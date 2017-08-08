---
layout: post
title: Getting a List of Unique Values From an Array
---

I ran into a situation where I had to create a list of questions for a test. The test comprised of just only ten questions and I just had to figure out what questions I wanted to put in. That was pretty easy to implement. But wait, what if I wanted to increase the amount of questions from ten to let’s say, fifteen? What if I wanted to change it to twenty? Basically I ran into the problem, what if I wanted to change it to an x amount of questions? That’s pretty easy enough but what that led me to, was realizing that I should have a test bank of questions.


Now let’s say I created a test bank of one hundred questions and then for my little test, I wanted to only have ten questions. I basically had to find a way to go into the test bank and get ten questions BUT each question I chose, had to be unique; I could not have a duplicate question in the test. I mean, what good of a test will it be if you find out that you get the same question three times?
Anyway, it got me thinking. For simplicity sake, my test bank would be an array and the numbers that represent each question would be the index but I start counting at one instead of zero. Simple enough. now from this test bank of questions that I have, I wanted to grab a unique subset of these questions (ten in total). I had to figure out, what data structure to use.


My options were:
1. Array
2. Hash Map
3. Linked List


I felt like a linked list was overkill for this type of simple thing and there was no benefit it had to an array other than the fact that you can add/change the size of the list. In my situation, it could be used as a solution but if it was already predetermined to have a certain limit, then it wouldn’t be needed. Would an array work? I mean if it’s just like the linked list, then it should still work right? What about the fact that it can’t have a duplicate? Array’s don’t really cover that and if Implement an if statement, that could get tricky. Wait does this mean I would also have to implement another loop and make my solution O(n)²? That doesn’t sound very efficient to me.
I thought about using a hash map but what would I use for the key-value pair? I could use the specific question number (index) as the key and then the count to be the value. If the value is greater than one, that means the question is already in the subset and I should try again. This would prevent any possible duplicates.


Then I went back and looked at other types of data structures and I realized that I completely forgot about sets. A set would work perfectly in this situation as it already filters out duplicate values if you try to add one into it. Because of this specific feature, I decided to use it and forego the little extra step of adding that if statement into the mix. Here’s what i came up with:


{% highlight js %}
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20];
var myset = new Set();

var i = 0;
var j = 0;


while (i <= 10) {
  var x = Math.floor(Math.random() * arr.length);
  myset.add(x);
  i++;
}

console.log("numbers tried: " + j);
console.log(myset);
{% endhighlight %}



As you can see, it’s a simple process, I just loop through the array which represents my test bank. In reality, the test bank could be an associative array or an array of JSON objects. I loop through the test bank array ten times and I generate a random number which represents the question number in the test bank. I add this into the set and continue until I hit ten. Unfortunately that did not work because I forgot to take into account that if the set finds a duplicate number, it would spit it out and then I’d have to try again. Basically, I have to add in a new if statement anyway. What’s the point of having a set then? It’s more memory intensive as compared to an array and if I have to add that extra if statement in there which adds a tiny bit more complexity, there goes the advantage…so I just reverted back to using a hash map:


{% highlight js %}
var arr = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20];
var hash = {};	//empty array to hold questions
var i = 0;
var j = 0;
var duplicateExists = true;


for (i = 0; i < 10; i++){
  duplicateExists = true;
  
  while (duplicateExists){
		j++;  
    var x = Math.floor(Math.random() * arr.length);
  
  	if (Object.values(hash).indexOf(x) > -1){
    	console.log("found duplicate for " + x);
      console.log("trying again...");
    	duplicateExists = true;
    }else{
    	hash[i] = x;
      duplicateExists = false;
    }
    
  }
}
console.log("numbers tried: " + j);
console.log(hash);
{% endhighlight %}


So there you have it, one way of choosing a unique subset from a larger set. This solution implements a hash map. I’m sure however that this could be easily done using functional programming but that will be for another time.


    - Andrew
