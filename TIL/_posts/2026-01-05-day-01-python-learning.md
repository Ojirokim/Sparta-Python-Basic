---
layout: post
title: "Day 1 - Python Learning"
categories: [til, python]
---

# Day 1 — Python Learning  
📅 2026-01-05

Today is **Day 1 of my Python learning journey**.  
In this post, I want to organize concepts that confused me at first:
**iterables, iterators, and the `map()` function, format(), F-string**.

This post is written mainly for myself, but it may also help other beginners.

---

## What is an Iterable?
An **iterable** is anything in Python that you can go through **one item at a time**.

If this works:
```python
for x in something:
    print(x)
```
Then something is an iterable.

Common examples of iterables:
- lists, strings, tuples

## Iterable vs Iterator
At first, I thought iterable and iterator were the same thing, but they are not.

## Iterable
- Can be looped over
- Can usually be reused

Example:
```python
nums = [1, 2, 3]
for x in nums:
    print(x)
for x in nums:
    print(x)   # works again
```

## Iterator
- produces values one at a time
- gets used up after being consumed
- Once it is exhausted, it cannot be reused unless recreated.


## map()
- map() returns a map object, which is an iterator, not a list.
- How I proved map() is not a list
```python
m = map(int, ["1", "2", "3"])
print(list(m))  # [1, 2, 3]
print(list(m))  # []
```
- If I were to use the outcome as a list I need to cover the whole thing in list()
Example:
```
nums = list(map(int, "1 2 3 4".split()))
print(nums, "합:", sum(nums))
```


## format()
- Put {} inside a string and fill it later using .format()
Example:
```python
name = "적토마"
score = 95
print("{}의 점수는 {}점입니다.".format(name, score))
```

## F-string()
- A more modern and commonly used alternative to format is to prefix the string with f and put variables directly inside {}


## Input()
- Always produces a String from input value


## Split
- Splits the string and creates a list out of that.
- Usually spit does not exclude spaces, thus you can use strip to delete that space
Example:
```python
lst = ["  apple  ", "  banana ", " cherry  "]
clean = [x.strip() for x in lst]
print(clean)
```

## Question
Why does some parts of python starts with 0 and count up, but some parts it starts with 1
- Zero-Based indexing
Used when referring to positions inside a sequence
Strings , Lists, Tuples, Indexing & slicing

- One-based counting
Used when counting “things” or when humans expect natural counting
range() when you choose it, enumerate(start=1)
User-facing output (ranking, order, steps)
Math / statistics concepts
Example code:
```
items = ["apple", "banana", "cherry"]
for i, item in enumerate(items, start=1):
print(i, item)
```

## Important note
When slicing last index does not get included
Example:
```python
s= "forty"
print(s[0:2])
# fo
```


