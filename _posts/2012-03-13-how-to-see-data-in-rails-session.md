---
layout: post
title: "How to see data in rails session"
category: 
tags:
- Rails
---
{% include JB/setup %}

{% highlight ruby %}

cookie = "BAh7CiIHdHQiQWJVaDlPTnlzeFAwT1J5eGZhOFNIVmV4aWR1RkFTZDdXVURmTHhOTnB2czVjVnZ0WFB2VXpRbEFITDZreiIQX2NzcmZfdG9rZW4iMS9UK0V0clZOUmgrVWp2M2Z0WkNWaHQxUWxtU3B1LzZBd3NTYjdJR0RkT1k9IhRsYXN0X3JlcXVlc3RfYXR1OglUaW1lDcXrG4BhsqGyIg9zZXNzaW9uX2lkIiUzZjg3NmVlM2VjMGJlOGViMjUyMDBhOThiM2VjNzU4NiITdXNlcl9yZXR1cm5fdG8iJi9teS9ydW5uaW5nP2ludGVydmFsPSZwZXJfcGFnZT0zMA%3D%3D--6490870d9173feeb8b92940740eadb30d740df25"

session_content, signature = cookie.split("--")

# Then you got the session content
session_hash = Marshal.load Base64.decode64 session_content

{% endhighlight %}

So please remember don't store sensitive data in session or signatured cookie, it's actually not safe.