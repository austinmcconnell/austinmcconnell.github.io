---
layout: post
title: 'Dive Into: Dictionaries'
categories: blog
date: 2017-02-20 18:30:00 -0600
tags: dive-into
---

Welcome to the first post in the 'Dive Into' series! In an effort to better understand the core components that Python is built around, I've decided to start taking deep dives into them and write about what I find.

The first topic I would like to cover is dictionaries. Much of Python is built with dictionary, incluing classes! Let's begin with some of the basics.

### Overview
Dictionaries are Python's standard mutable mapping type. They are comprised of keys and values, are inherently unordered, and require hashable values as keys. What does that mean?

### Ordered
A dictionary is **unordered** because the order really doesn't matter. Think about a physical dictionary(do they still have those?). When you use one, do you ever look up the 374th value? Or the 10045th? Nope. That just doesn't make a whole lot of sense. You look up a particular word and want to know the definition. Well the word is the 'key' and the definition is the 'value'.


### Hashable
Also, a dictionary must only use **hashable** keys. Let's step back a minute and consider what hashable means.

A hash value is an integer that uniquely identifies a piece of data.

For example
```python
>>>hash('peanuts')
5364670550989854731
```

A string (e.g. 'peanuts') is hashable and **immutable**. It cannot be changed. A list, however, is not hashable by virtue of being mutable. If it can change, then it does not have a unique value that can be used for equality testing.

```python
>>>shopping = ['eggs', 'milk', 'cheese']
>>>hash(shopping)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'"
```

### Creation

Dictionaries can be created three separate ways

* with keyword arguments
* with a mapping and keyword arguments
* with an iterable and keyword arguments
 
 Using keyword arguments
 ```python
 >>>first = dict(year=2017, month=2, day=20)
 >>>first
 {'year': 2017, 'month': 2, 'day': 20}
```

Using a mapping
```python
>>>second = dict({'year':2017, 'month':2, 'day':20})
>>>second
{'year': 2017, 'month': 2, 'day': 20}
```


Using an iterable
```python
>>>an_iterable = zip(['year', 'month', 'day'], [2017, 2, 20])
>>>third = dict(an_iterable)
>>>third
{'year': 2017, 'month': 2, 'day': 20}
```

## Operations

### get(key, [default])
Calling get(key) or get(key, [default]) will return the value assocated for the given key if the key is in the dictionary. Without providing a default value, the value defaults to None. If a default is provided, that shall be returned in the event a key is not found. Calling a dictionary with this operation will never return a KeyError. 

For example, let's lookup the year from our dictionary above
```python
>>>first.get('year')
2017
```

What if we misremembered the key values and tried to get the value for the hour key?

```python
>>>first.get('hour')

```

There was no KeyError because None was returned. However, if we had called with a default value...
```python
>>>first.get('hour', 12)
12
```

The provided default value of 12 is returned.

This is a very useful construct because it allows you to check for a value without needing a try/except block. Note, when the key is not found and a default value returned, there is no new key:value entry in the dictionary.

### items()
Calling d.items() will return a view of the dictionaries key, value pairs as tuples. A view is a dynamic look at the dictionary items which will reflect to show changes to the underlying dictionary.

```python
>>>my_view = first.items()
>>>my_view
dict_items([('year', 2017), ('month', 2), ('day', 20)])

>>>first['year'] = 2020
>>>my_view
dict_items([('year', 2020), ('month', 2), ('day', 20)])
```

### keys
Return a view (remember, dynamic reference) to the dictionaries keys. Similar to items().

```python
>>> first.keys()
dict_keys(['year', 'month', 'day'])
```

### iter(d)
Calling iter(d) will return an iterator of the keys. It's a simple shortcut to the longer version iter(d.keys()) and quite useful.

Iterating over a dictionary
```python
>>>for key in iter(first):
...    print(key, '\t', first[key])
year 	 2017
month 	 2
day 	 20
```

### pop(key, [default])
pop is a neat way to retrieve a value and remove it from the dictionary (if found) or return default (if not found). If a default is not provided, a KeyError will be raised if the key is not found. 

```python
>>> first.keys()
dict_keys(['year', 'month', 'day'])

>>> first.pop('year')
2017

>>> first.keys()
dict_keys(['month', 'day'])

>>> first.pop('hour')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'hour'

first.pop('hour', 'missing')
'missing'
```

### popitem()
This is a fantastically useful operation that will remove and return a random (key, value) pair from the dictionary. This allows you to destructively iterate over the dictionary with minimal code.

```python
>>> first.keys()
dict_keys(['year', 'month', 'day'])

>>> first.popitem()
('year', 2017)

>>> first.keys()
dict_keys(['month', 'day'])
``` 
This will raise a KeyError if called on an empty dictionary.

### values
Returns a view(dynamic reference) of the dictionary values.

```python
>>> first.values()
dict_values([2017, 2, 20])

>>> the_values = first.values()
>>> the_values
dict_values([2017, 2, 20])

>>> first['month'] = 5
>>> the_values
dict_values([2017, 5, 20])
```

### setdefault(key, [default])
Return value if key is in the dictionary. If no key found, insert value with default value and return default.

```python
>>> first.keys()
dict_keys(['month', 'day'])

>>> first.setdefault('month', 7)
2

>>> first.setdefault('year', 2017)
2017

>>> first.keys()
dict_keys(['year', 'month', 'day'])
```

### update([other])
This operation updates key/values pairs based on the *other* parameter passed in. This accepts the same input formats that dictionary creation does keyword arguments, mapping, or iterable.

```python
>>> first.items()
dict_items([('year', 2017), ('sec', 0), ('month', 2)])

>>> first.update(year=2025, hour=12, min=30, sec=00)
>>> first.items()
dict_items([('year', 2025), ('sec', 0), ('month', 2), ('min', 30), ('day', 20), ('hour', 12)])
```
 Note how the `year` value was updated/overwritten while the remaining key/values were simply added.

Well that's it for the first deep dive! I learned a lot by digging through the documentation and reading about some of the more obscure/less used features of dictionaries. I hope you got something out of it! If so, let me know on Twitter at [@austin_s_mcc](https://twitter.com/austin_s_mcc)
