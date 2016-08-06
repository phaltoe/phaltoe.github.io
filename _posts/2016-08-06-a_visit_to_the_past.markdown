---
layout: post
title:  "A Visit to the Past"
date:   2016-08-06 20:24:08 +0000
---


Hi guys,

This is my blog post for my OOP - CLI Gem assessment.

Honestly, this was pretty tough. By the time I was doing it, I wasn’t very sure what some of the methods I built were doing, but I kept building it and it finally clicked.

```
def create(name)
  self_instance = self.new(name)
  self_instance.save
  self_instance
end
```


```
def save
  self.class.all << self
end
```

Looking right now, it seems like a non-brainer and obvious, but when I was asked if I knew the difference from `save` to `create` method, I couldn't answer.

```
def self.find_by_name(name)
  self.all.detect { |x| x.name == name }
end

def self.find_or_create_by_name(name)
  self.find_by_name(name) || self.create(name)
end
```

It was also cool to handicraft these methods, these are methods that we will use for a great portion of the program, but lately ActiveRecord will provide it for us along some other very cool and useful methods.

Looking back in time, now I can have a clear vision of how much I evolved since I built this Gem.  I can't wait to see what comes next.

Regards,
Pedro
