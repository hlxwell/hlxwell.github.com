---
layout: post
title: "How to send Multipart email in Rails."
category: 
tags:
- Rails
---
{% include JB/setup %}

Yes, it sounds pretty easy, just write code like below:

{% highlight ruby %}
mail(:to => user.email,
     :subject => "Welcome to My Awesome Site") do |format|
   format.html
   format.text
end
{% endhighlight %}

This code will generate a multipart email, that put the html content as the first part, 
and text content as second part. This will cause a problem is, when you open the email in mailbox, 
Oh, 奶奶的, why it's text version. You must expect "It should show html when mail client support MIME,
and show text version if it's not support MIME."

Actually, the truth is:

Before the first boundary is an area that is ignored by MIME-compliant clients. 
This area is generally used to put a message to users of old non-MIME clients.

