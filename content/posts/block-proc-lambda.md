---
title: "Block Proc Lambda"
date: 2018-07-11T23:13:36+02:00
draft: false
---

I was reading the [Mastering Ruby blocks in less than 5 minutes](https://mixandgo.com/learn/mastering-ruby-blocks-in-less-than-5-minutes) and I was confused on the part on how `&block` means. So I went back to the basic.

Blocks are syntactic structures in Ruby; they are not objects, and cannot be manipulated as objects. It is possible, however, to create an object that represents a block. And that object is call `Proc` object.

```
# Block
[-1, 0, 1].map { |x| x > 0 } # block is in between the curly braces
[-1, 0, 1].map do |x|
  x > 0
end                          # block is everything between the do and end

# Creating a proc object that represents a block
a_proc = Proc.new { |x| x > 0 }
```

Procs have block-like behaviour and lambdas have method-like behaviour. Both, however, are instances of class `Proc` [333]

`Proc` is a class in Ruby, and it represents blocks of code. And Procs object can either have block-like behavior (for _procs_) or method-like behaviour (for _lambdas_). We only saw how to create a proc. Next sections will represent different ways to construct both type of `Proc` object. 

### `Proc` object that is a proc(not a lambda)

```
is_positive_proc = Proc.new { |x| x > 0 } #<Proc:...>
is_positive_proc_2 = proc { |x| x > 0 } #<Proc: ...> From Ruby 1.9 only
```

### `Proc` object that is a lambda (not a proc)

```
is_positive_lambda = lambda { |x| x > 0 } #<Proc:... (lambda)>
is_positive_lambda_2 = -> (x) { x > 0 } #<Proc:... (lambda)>
```

### Calling `Proc` object

`Proc` object (either procs or lambdas) are objects, not methods. They can be invoked by `call` method, or `[]`

```
is_positive_proc #<Proc:...>
is_positive_proc(3) # NoMethodError: undefined method `is_positive_proc' for main:Object
is_positive_proc.call(3) # true
is_positive_proc[-5] # false
```

### Resources
1. [What Is the Difference Between a Block, a Proc, and a Lambda in Ruby?](https://awaxman11.github.io/blog/2013/08/05/what-is-the-difference-between-a-block/) by Adam Waxman 
2. [Mastering Ruby blocks in less than 5 minutes](https://mixandgo.com/learn/mastering-ruby-blocks-in-less-than-5-minutes) by Cezar Halmagean
3. _The Ruby Programming Language_ - David Flanagan and Yukihiro Matsumoto. Though it covers Ruby 1.8 and 1.9, many points are still relevant and for me, it always good to know the background really well.

