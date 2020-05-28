---
layout: post
title:  "Arduino serial speed"
date:   2020-05-28 20:04:59 +0200
categories: Arduino Serial
---
Did you know that the arduino can use arbitary serial speeds? I have connected my UNO to my pc and uploaded the following sketch:
{% highlight c %}
void setup() {
    // put your setup code here, to run once:
    Serial.begin(500000);
    Serial.write("hello");
}
void loop() {
}
{% endhighlight %}

This works fine when I connect my pc to the arduino via putty and set the speed to 500,000

I wonder what the maximum speed is.
My tests showed that it is 4,000,000. This is 4 megabit/s. About 16 times the memory of an arduino UNO. I am not sure how this could be useful, but it is good to know.
