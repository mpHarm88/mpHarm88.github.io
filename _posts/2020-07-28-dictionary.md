---

layout: post
title: 🐍 How to Use Python Dictionaries
subtitle: An Introduction to Python Dictionaries
bigimg: img/python_dict.png
gh-repo: mpHarm88/projects/dictionaries
gh-badge: [star, watch, fork, follow]
tags: [python]

---

Put merely, dictionaries are key-value pairs. Dictionaries are created by using the curly brackets ({}) and can hold multiple key-value pairs separated by commas. If you want to find a specific value, then you will need to know the values associated key.

```python
{key: value}
```

- Keys can be any string or number as long as it's unique to the keys of the dictionary.
- Values can be anything you want including [Integers]("https://docs.python.org/3.8/library/functions.html#int"), [Floats]("https://docs.python.org/3.8/library/functions.html#float"), [Strings](https://docs.python.org/3.8/library/functions.html#func-str), [Lists]("https://docs.python.org/3/library/functions.html#func-list"), [Dictionaries]("https://docs.python.org/3/tutorial/datastructures.html#dictionaries"), [Variables]("https://docs.python.org/3/library/functions.html#vars")

Let's look at an example.

```python
# Create an empty dictionary
d = {}
print(d)

# Add some key:value pair to d
d["one"] = 1
d[2] = "two"
d["three"]= [1.1,2.22,3.333]
d[4] = {"cat": "dog", 555: "3 fives"}
print(d)

# Look at the keys in d
print(d.keys())

# Look at the values in d
print(d.values())

# Output
{}

{'one': 1, 2: 'two', 'three': [1.1, 2.22, 3.333], 4: {'cat': 'dog', 555: '3 fives'}}

dict_keys(['one', 2, 'three', 4])

dict_values([1, 'two', [1.1, 2.22, 3.333], {'cat': 'dog', 555: '3 fives'}])
```
Indexing into a dictionary is not the same as indexing into a list. When working with a list inside of the dictionary, you will have to first use the associated key then use the associated index to get your intended value.

```python
# Access the 2nd list value in key "three"
val = d["three"]
val2 = d["three"][1]
print(type(val), type(val2))
print(val, val2)

# Combine val and val2 into a single call
val3 = d["three"][1]
print(val3)

# Output
<class 'list'> <class 'float'>

[1.1, 2.22, 3.333] 2.22

2.22
```
When we look at ```val``` we see that it is of type [list()]("https://docs.python.org/3/tutorial/datastructures.html#more-on-lists") and it's not until we index into the list using zero-based list indexing to get our desired value. We do this using ```val2``` and see that it is of type [float()]("https://docs.python.org/3/library/functions.html#float") and is also the correct value.

- If you need a refresher on Python lists, take a look at my short blog about them [here]("https://www.mikioharman.com/2020-07-27-lists/").

What if we wanted to look up the second key-value pair of the 4th key of d? We would only have to do the following:

```python
# Access the 2nd key of the 4th key in d
val4 = d[4]
val5 = d[4][555]

print(type(val4), type(val5))
print(val4, val5)

# Refactor val3 and val4 to one line
val6 = d[4][555]
print(val6)

# Output
<class 'dict'> <class 'str'>

{'cat': 'dog', 555: '3 fives'} 3 fives

3 fives
```
### Benefits of using the type function
Using [type()]("https://docs.python.org/3/library/functions.html#type") is a great way of building your dictionary calls when you have multiple nested datatypes within one another. I often use ```type()``` to locate where I'm at when I am inside a giant JSON object that was returned from an API. This helps me write my functions quicker and more concisely.

## Common Dictionary Methods
Before we get into some more interesting parts of a dictionary, let's look over some of the methods associated with dictionaries.

```python
# Get the value of a key
print(d.get("one"))

# View the key-value pairs
print(d.items())

# Remove and return the given key from the dictionary
print(d.pop("one"))

# Remove and return the latest element from the Dictionary
print(d.popitem())

# Check the dictionary for a certain key and create it if it doesnt exists, return the value if it does exist
print(d.setdefault("pie")) # default value is None if not specified
print(d.setdefault(2))

# Add a dictionary to another dictionary
# New keys are added if they dont exist already
# Since this key already exists, it will be updated with the new value
d2 = {
      "hot": "cold", 
      "three": 3 
     }
d.update(d2)
print(d)

# Delete the contents of a dictionary
d.clear()
print(d)

# Output
1

dict_items([('one', 1), (2, 'two'), ('three', [1.1, 2.22, 3.333]), (4, {'cat': 'dog', 555: '3 fives'})])

1

(4, {'cat': 'dog', 555: '3 fives'})

None

two

{2: 'two', 'three': 3, 'pie': None, 'hot': 'cold'}

{}
```
## Dictionary Comprehension
Just like list comprehension, dictionary comprehension transforms one dictionary into another dictionary. We will use the builtin function [chr()]("https://docs.python.org/3/library/functions.html#chr") to create our keys and [range()]("https://docs.python.org/3/library/functions.html#func-range") to create a specified number of elements and associated values. Let's take a look at some simple examples.

```python
# Create a dictionary using chr() and range()
d = {chr(65+x):x for x in range(10)}
print(d)

# Add 1 to each value
d = {k:v+1 for (k,v) in d.items()}
print(d)

# Keep the value if divisible by 2 else add 5
d = {k:v if v%2==0 else v+5 for (k,v) in d.items()}
print(d)

# Create a list of range value for each key
d = {k:[x for x in range(v)] for (k,v) in d.items()}
print(d)

# Add "1" to each key and 10 to each value in the list if it's divisible by 3 else "X"
d = {k+"1":[x+10 if x%3 == 0 else "X" for x in v] for (k,v) in d.items()}
print(d)

# Output
{'A': 0, 'B': 1, 'C': 2, 'D': 3, 'E': 4, 'F': 5, 'G': 6, 'H': 7, 'I': 8, 'J': 9}

{'A': 1, 'B': 2, 'C': 3, 'D': 4, 'E': 5, 'F': 6, 'G': 7, 'H': 8, 'I': 9, 'J': 10}

{'A': 6, 'B': 2, 'C': 8, 'D': 4, 'E': 10, 'F': 6, 'G': 12, 'H': 8, 'I': 14, 'J': 10}

{'A': [0, 1, 2, 3, 4, 5], 'B': [0, 1], 'C': [0, 1, 2, 3, 4, 5, 6, 7], 'D': [0, 1, 2, 3], 'E': [0, 1, 2, 3, 4, 5, 6, 7, 8, 9], 'F': [0, 1, 2, 3, 4, 5], 'G': [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11], 'H': [0, 1, 2, 3, 4, 5, 6, 7], 'I': [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13], 'J': [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]}

{'A1': [10, 'X', 'X', 13, 'X', 'X'], 'B1': [10, 'X'], 'C1': [10, 'X', 'X', 13, 'X', 'X', 16, 'X'], 'D1': [10, 'X', 'X', 13], 'E1': [10, 'X', 'X', 13, 'X', 'X', 16, 'X', 'X', 19], 'F1': [10, 'X', 'X', 13, 'X', 'X'], 'G1': [10, 'X', 'X', 13, 'X', 'X', 16, 'X', 'X', 19, 'X', 'X'], 'H1': [10, 'X', 'X', 13, 'X', 'X', 16, 'X'], 'I1': [10, 'X', 'X', 13, 'X', 'X', 16, 'X', 'X', 19, 'X', 'X', 22, 'X'], 'J1': [10, 'X', 'X', 13, 'X', 'X', 16, 'X', 'X', 19]}
```

After the first comprehension, you can see a common theme in each subsequent iteration. We are able to change key and values as long as we follow the rules associated with the data type we are transforming. Don't forget that ```d.items()``` returns a list of tuples as was previously shown. This is why we always use ```(k,v)``` after the ```for``` statement.

The most important takeaway is that the more processes you add to your comprehension, the harder it becomes to read for you and anyone else. Always strive for readable code instead of complex code. If you can break apart complex code into separate, more readable portions, then that is better than having a monster one-liner that no one can comprehend.

## Dictionary Iteration
Now that we know how to make and search through a dictionary let's focus on iterating through one. Sometimes it's difficult to think of the correct dictionary comprehension syntax to perform your transformation. Using a for loop will help increase readability and is more beginner-friendly in my opinion.

It's important to note that we have to access the list of the key we are using before we can alter its contents. This is easy using the ```range()``` function coupled with proper list indexing to adjust our values as intended. We also look at the type of each item to make sure we can perform the required operation before moving to the next element in the list.

```python
%%time
# Iterate through the dictionary and add 3.14 else add "-ray"
for k, v in d.items():
    for x in range(len(v)):
        if type(v[x]) == int:
            d[k][x] = v[x] + 3.14 
        else:
            d[k][x] = v[x]+"-ray"
            
# Output
CPU times: user 59 µs, sys: 0 ns, total: 59 µs
Wall time: 62 µs
```
Using a for loop increases the readability, but also adds a lot of extra code and time. To prove how slow the for-loop is, let's time the same process using a dictionary comprehension.

```python
%%time
# Perform the same task as above except using a comprehension
d = {k:[x+3.14 if type(x)==int else x+"-ray" for x in v] for (k,v) in d.items()}

# Output
CPU times: user 33 µs, sys: 0 ns, total: 33 µs
Wall time: 36 µs
```
Wow! The dictionary comprehension wall time when compared to the for-loop, is ~42% faster! This is a considerable improvement and a big reason to consider using these types of comprehension.

### You did it!
Now that you have an understanding of how dictionaries work in Python, can you think of other ways to utilize them? What are some real world applications that could use a dictionary? This is just the beginning of using dictionaries in Python, and like anything, only gets better with practice, so get out there and use some dictionaries!
Feel free to leave feedback or address any errors I've made. I'm always looking to improve and value your feedback!
Find the code for this blog [here]("https://github.com/mpHarm88/projects/blob/master/dictionaries/dictionary.ipynb")!
