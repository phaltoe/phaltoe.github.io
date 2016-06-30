---
layout: post
title:  "A Sinatra Blog - Validation"
date:   2016-06-20 21:10:52 +0000
---


Hi everyone,

This is my last project with **Sinatra** before moving on to **Rails** land. It took me a while to feel confident writing Sinatra apps and I had to slow down and dive deeper to understand how it really works.

During the process there was one thing that I would like to share with you that made it very interesting.

I had to learn about **validation.**

What is validation?

Validation is what makes sure that only valid data is saved to our database. What this means is, when you are trying to creating a new user, in my blog app you will have 3 fields necessary to fill:

**Name**
**Email**
**Password**

When you are using the ```validation_presence_of```(you can choose what params you want to validate, in my app, all 3 fields have to be filled in order to be valid) if one name isn't provided, it will give you an error and not save it to the database. This will do the same for password and email(in this case it will check the presence of an @ in the text field as well).

***Only when we are trying to Create/Save/Update an object into our database validation will be triggered.***

You can use the `method valid?` on any instance method. Whenever your validation returns false, it will give you access to the `errors.messages` instance methods that are what we use to display error messages dynamically when trying to insert new data in our database.

The tricky part is:  when you are validating i.e a signup form, you are sending a POST request.  So if it validates to false you will basically have to render the form again.  However once you re-render the form, your instance of that object gets lost since it wasn't saved in the databased because it validated to false.

So here comes the question: how we are going to access the error instance methods without an instance from the object to call it on?  Simple.  Remember what I said above?

***_"Only when we are trying to Create/Save/Update an object into our database validation will be triggered."_***

So if we create a new instance of that object with `.new` it will not be saved in our database and we still can use it to call our `error.messages`. This lets us validate the form without losing the data.

After all, I am glad I spent a lot of time on it.  Now I feel readier to go and learn Rails.

Hope you enjoy,

Pedro
