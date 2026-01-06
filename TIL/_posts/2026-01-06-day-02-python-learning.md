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




