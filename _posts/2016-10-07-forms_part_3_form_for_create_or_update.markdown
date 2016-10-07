---
layout: post
title:  "Forms Part 3 — Form For | CREATE or UPDATE?"
date:   2016-10-07 17:45:33 +0000
---


How does Rails know if we are trying to create or update an object?

At this point, we are assuming that the convention form for form_for is the exactly the same for CREATE AND UPDATE.
First, lets display a Post form:
…
```
 <%= form_for(@post) do |f| %>
  <%= f.text_field :name %>
 
  <%= f.submit %>
 <% end %> 
```
…
Question: If both forms are the same then how does Rails knows if we are trying to create or update an object?
It will check a method called .persisted?
If @post.persisted? returns true: this means that it is not a new_record and is already in the Database.
Rails knows that it is an EDIT form.
If @post.persisted? returns false: this means that it is a new_record and is not in the Database yet.
Rails knows that it is a CREATE form.
— —
Another way of understanding it is to look at your Controller.
(Please bear in mind that this is not how Rails recognises the pattern for CREATE or UPDATE but it will give you an idea)
```
def update
  @post = Post.find(params[:id])
  @post.update(list_params)
  redirect_to post_path(@post.id)
end

def create
 @post = Post.new(post_params)
 if @post.valid?
  @post.save
  redirect_to post_path(@post.id)
 else
  render :new
 end
end
```
Can you spot the difference between the two actions?
When you try to UPDATE, you are retrieving data from your database:
…
` @post = Post.find(params[:id])`
…
This is different from when you are trying to create a new instance, which means that you are explicitly trying to insert data in your database.
…
```
 @post = Post.new(post_params)
if @post.valid?
 @post.save
 redirect_to post_path(@post.id)
```
…
 
You can try it by yourself using these methods:
```
.persisted?
.new_record?
```
Rgds
