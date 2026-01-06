---
layout: post
title: "Day 2 - Python Learning"
categories: [til, python]
---

# Day 1 — Python Learning  
📅 2026-01-06

Today is **Day 2 of my Python learning journey**.
---

## How join() works in Python
join() is a string method, not a list method
The correct syntax is:
```python
separator.join(iterable)
```

✅ Correct:
```python
result = "-".join(split_text)
```

### Reason:
join() must be called on the separator string
The argument must be an iterable of strings
All elements in the iterable must be strings, otherwise use:
"-".join(map(str, split_text))

## Key takeaway:
Think of join() as “use this string to glue things together.”


## How end numbers act in range and slicing
In Python, both range() and slicing are start-inclusive, end-exclusive.
range(1, 10) goes from 1 to 9, and seq[1:4] includes index 1 but excludes index 4.
This design avoids off-by-one errors and makes len(seq[:n]) == n.


## find()
Python’s .find() searches for a substring in a string and returns the starting index if found, or -1 if not found. It returns an integer (not True/False), so using it directly in if statements can be dangerous because 0 is False and -1 is True.
```python
string.find("@")
```

## equal
!= means “not equal”; /= means “divide and assign” and is unrelated.
