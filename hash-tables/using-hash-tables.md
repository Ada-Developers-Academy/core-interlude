# Using Hash Tables

## Goals

It's all well and good to know what hash tables _are_, but how can we use them? Using hash tables creatively will allow us to create efficient and organized solutions!

- Apply knowledge about hash tables to solve problems

## Python Dictionaries Are Hash Tables

All hash tables are data structures that hold key-value pairs and implement an associative array. They all perform find, insert, and remove at O(1). Hash tables can be implemented in nearly any programming language.

Python implements hash tables and made a hash table into a data structure we use all the time: dictionaries!

### !callout-info

## We Can See How Python Implements Dictionaries

We can look at [Python's source code for dictionaries](https://github.com/python/cpython/blob/master/Objects/dictobject.c). The very first commented line titles the file as `/* Dictionary object implementation using a hash table */`! We can continue to read through the code and see comments about the hash function and how it handles collisions.

### !end-callout

## Strategies

We can practice using hash tables to solve problems by thinking about how to use a Python dictionary.

Python dictionaries can be used in many ways:

- Creating a frequency map that counts how frequently...
  - A character occurs in a string
  - A word occurs in a list
  - A value occurs in a collection
- Creating a map that maps...
  - A `True` or `False` value to each key
  - String or integer values attached to each key

Or so many more possibilities!

Overall, here are some general strategies to consider when using a hash table to solve a problem:

1. Are there any pieces of data that we need to tie together, such as counting the frequency of some value, or attaching a description to some name?
   - Could we turn those into key-value pairs?
1. For those key-value pairs, what keys and values would help us find the answer?
1. For those key-value pairs, what is the initial state of the key-value pairs?

## Walk-through Example: Missing Elements in a Range

Let's walk through solving this problem, discovering how to use a hash table to our advantage.

Write a function named `get_missing_numbers_in_range`. This function takes in an `array` of distinct integers, an integer `low` which is the lowest number in a range, and an integer `high` which is the highest number in a range.

This function returns a list of all numbers that are between `low` (inclusive) and `high` (exclusive) and are **not** inside `array`.

The missing elements should be returned in the relative order that they are originally listed.

Examples:

| `array`               | `low` | `high` | Expected return value |
| --------------------- | ----- | ------ | --------------------- |
| `[10, 12, 11, 15]`    | `10`  | `15`   | `[13, 14]`            |
| `[1, 14, 11, 51, 15]` | `50`  | `55`   | `[50, 52, 53, 54]`    |

Take five minutes to answer:

1. Are there any pieces of data that we can tie together here to create key-value pairs? Consider:
   - A value and the number of occurrences of that value
   - A value and `True` or `False` to associate with that value
1. What keys and values would help us find the answer?
1. What is the initial state of the key-value pairs?

### Brainstorm Associated Data

Our problem states that we need to find the _numbers_ that are _missing_ from a _range_.

Therefore, we have the following pieces of data we could keep track of:

- Each number in the input `array`
- Each number within the range of `low` and `high`
- If each number in `array` is within the range of `low` and `high`
- If each number within the range is accounted for in `array`

Which pieces of data have a close relationship with each other?

### Key-Value Pairs to Solve Our Problem

In this problem, _numbers_ are **either** _present_ or _missing_ from a range.

We want to create a list of numbers that are missing, also known as numbers where **their presence in the range is `False`**.

Let's consider making our key-value pairs into pairs of a **number** and **a boolean** indicating if it's present. Therefore, we will use a hash table (dictionary) to store number-boolean pairs.

### Initial State of Key-Value Pairs

The initial state of our number-boolean pairs will be based on the input `array`.

At the beginning of our problem, we can make a hash table where each number is a key, with the value `True` for being present.

Consider our example:

| `array`            | `low` | `high` | Expected return value |
| ------------------ | ----- | ------ | --------------------- |
| `[10, 12, 11, 15]` | `10`  | `15`   | `[13, 14]`            |

The initial hash table's key-value pairs will be:

| Key (Number) | Value (Is Present) |
| ------------ | ------------------ |
| `10`         | `True`             |
| `12`         | `True`             |
| `11`         | `True`             |
| `15`         | `True`             |

### Pseudocode

With this strategy, our code will take this approach:

1. Create a hash table (using a dictionary) that maps a number in an array to `True`, to show that it is present
1. Create an empty list to hold all missing numbers
1. For each number in the range between `low` and `high`, check the value in the map:
   - If the number-boolean pair exists and the value is `True`, then the number is present
   - If the value is `False`, then the number is missing
     - Append it to our list that holds all missing numbers

### Solution: Get Missing Numbers in Range

<!-- Question 1 -->
<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: NUVA0m
* title: Using Hash Tables
### !question

Using a dictionary and the pseudocode above, implement `get_missing_numbers_in_range`.

Here is the original prompt again:

Write a function named `get_missing_numbers_in_range`. This function takes in an `array` of distinct integers, an integer `low` which is the lowest number in a range, and an integer `high` which is the highest number in a range.

This function returns a list of all numbers that are between `low` (inclusive) and `high` (exclusive) and are **not** inside `array`.

The missing elements should be returned in the relative order that they are originally listed.

Here are the tests:

```python
def test_get_missing_numbers_in_range():
    assert get_missing_numbers_in_range([10, 12, 11, 15], 10, 15) == [13, 14]


def test_get_missing_numbers_in_range_small_range():
    assert get_missing_numbers_in_range(
        [1, 14, 11, 51, 15], 50, 55) == [50, 52, 53, 54]
```

### !end-question
### !tests
```python
import unittest
from main import *

class TestChallenge(unittest.TestCase):

    def test_get_missing_numbers_in_range(self):
        self.assertEqual(get_missing_numbers_in_range(
            [10, 12, 11, 15], 10, 15), [13, 14])

    def test_get_missing_numbers_in_range_small_range(self):
        self.assertEqual(get_missing_numbers_in_range(
            [1, 14, 11, 51, 15], 50, 55), [50, 52, 53, 54])
```
### !end-tests
### !explanation

An example of a working implementation:

```python
def get_missing_numbers_in_range(array, low, high):
    map = {}

    for num in array:
        map[num] = True

    missing_nums = []
    for i in range(low, high):
        if not map.get(i):
            missing_nums.append(i)

    return missing_nums
```

### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

### Time Complexity Comparison

#### Iterative Solution

While solving this problem, we may have considered an iterative solution to this that did not use a hash table. For example:

```python
def get_missing_numbers_in_range(array, low, high):
    missing_nums = []

    for i in range(low, high):
        if i not in array:
            missing_nums.append(i)

    return missing_nums
```

This solution may seem more straightforward compared to a hash table. Why would we choose to use a hash table here?

Let's analyze the time complexity of this solution:

- There is `array` with a size of `n`.
- There is a variable range between `low` and `high` that is a size of `m`.

Because we iterate through the range, we loop `m` times.

_Inside_ each loop, we also search through the array of length `n` with `if i not in array`, which is O(n).

Therefore, the time complexity of the iterative solution is O(n\*m).

### !callout-info

## Finding the Big O of Python's `in`

How did we know that the time complexity of `if i not in array` is O(n)? [We looked up Python documentation about the time complexity of a list's `in` operator!](https://wiki.python.org/moin/TimeComplexity)

### !end-callout

#### Hash Table Solution

Let's compare this to using a hash table:

- To initialize the dictionary with all numbers in `array` set to `True`, we loop through the array of size `n` once
- To check if a number is missing from the range, we iterate through the range of size `m` once
  - Inside each loop, we search for the element from the dictionary. The complexity of finding an element from a dictionary is O(1).

Therefore, our time complexity is O(n+m). This solution is more time-efficient than the iterative solution!

## Walk-Through Example: Find All Symmetric Pairs

Let's practice solving a different problem using hash tables.

Two pairs _[a, b]_ and _[c, d]_ are said to be symmetric if _a_ is equal to _d_ and _b_ is equal to _c_. For example, _[10, 20]_ and _[20, 10]_ are symmetric.

Write a function named `get_symmetric_pairs`. This function takes in a list (`pairs`) of lists. Each sub-list is a list of two elements.

This function should return a list of all symmetric pairs. A pair should only be listed once (without its symmetric counterpart). List the first pair of a pair of symmetric pairs.

Assume that the first element of all pairs are distinct.

Examples:

| Input `pairs` list                                                                                                     | Symmetric Pairs                                    | Return value          |
| ---------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------- | --------------------- |
| `[[11, 20], [30, 40], [5, 10], [40, 30], [10, 5]]`                                                                     | `[30, 40]` and `[40, 30]`; `[5, 10]` and `[10, 5]` | `[[30, 40], [5, 10]]` |
| `[["Dan", "Kari"], ["Jeremy", "Val"], ["Jeremy", "Charles"], ["Devin", "Susan"], ["Kari", "Dan"], ["Devin", "Susan"]]` | `["Dan", "Kari"]` and `["Kari", "Dan"]`            | `[["Dan", "Kari"]]`   |
| `[["Dan", "Kari"], ["Lisa", "Val"], ["Jeremy", "Charles"], ["Devin", "Susan"], ["Charles", "Jamie"]]`                  | -                                                  | `[]`                  |

Take five minutes to answer:

1. Are there any pieces of data that we can tie together here to create key-value pairs? Consider:
   - A list and the number of times a word occurs in that list
   - A string and a second string or integer value associated with it
1. What keys and values would help us find the answer?
1. What is the initial state of the key-value pairs?

### Brainstorm Associated Data

This problem requires us to focus on each pair and any data we can possibly track from them.

We'll need to apply our knowledge about dictionaries and understand that lists are not valid keys, even though strings and numbers are.

Consider the following possible pieces of data to keep track of in a hash table:

- The first item in the pair and the second item in the pair
- The first item in the pair and the number of times it occurs in any sub-list

### Key-Value Pairs to Solve Our Problem

Let's consider making our key-value pairs into pairs of **first item** and **second item**.

In our hash table, the first item of a pair will be the key, and the second item of the pair will be the value.

### Initial State of Key-Value Pairs

The initial state of our pairs will be based on the input list of `pairs`.

Consider our example:

| Input `pairs` list                                 | Symmetric Pairs                                    | Return value          |
| -------------------------------------------------- | -------------------------------------------------- | --------------------- |
| `[[11, 20], [30, 40], [5, 10], [40, 30], [10, 5]]` | `[30, 40]` and `[40, 30]`; `[5, 10]` and `[10, 5]` | `[[30, 40], [5, 10]]` |

The initial hash table will be:

| Key (First Item) | Value (Second Item) |
| ---------------- | ------------------- |
| `11`             | `20`                |
| `30`             | `40`                |
| `5`              | `10`                |
| `40`             | `30`                |
| `10`             | `5`                 |

### Pseudocode

Our solution will take this approach:

1. Create a hash table that maps every pair's first item to its second item
1. Create an empty list to hold all symmetric pairs
1. For each "first item"-"second item" pair in the hash table:
   1. Check the hash table if the symmetric pair exists:
      1. Take the current second item, and use it as a key in the hash table
      1. If the hash table has the current second item as a key, check if its value is equal to the current key (current first item)
      1. If it's equal, then there's a symmetric pair!
         1. Append it to our list of symmetric pairs
         1. Set the symmetric pair to `None` in the hash table so that the symmetric pair does not get duplicated in our final result

### Solution: Get Symmetric Pairs

<!-- Question 2 -->
<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: 2gLI5x
* title: Using Hash Tables
### !question

Using a dictionary and the pseudocode above, implement `get_symmetric_pairs`.

Here is the original prompt again:

Write a function named `get_symmetric_pairs`. This function takes in a list (`pairs`) of lists. Each sub-list is a list of two elements.

This function should return a list of all symmetric pairs. A pair should only be listed once (without its symmetric counterpart). List the first pair of a pair of symmetric pairs.

Assume that the first element of all pairs are distinct.

Here are the tests:

```python
def test_get_symmetric_pairs():
    pairs = [[11, 20], [30, 40], [5, 10], [40, 30], [10, 5]]
    assert get_symmetric_pairs(pairs) == [[30, 40], [5, 10]]


def test_get_symmetric_pairs_strings():
    pairs = [["Dan", "Kari"], ["Jeremy", "Val"], ["Jeremy", "Charles"], [
        "Devin", "Susan"], ["Kari", "Dan"], ["Devin", "Susan"]]
    assert get_symmetric_pairs(pairs) == [["Dan", "Kari"]]


def test_get_symmetric_pairs_no_pairs():
    pairs = [["Dan", "Kari"], ["Lisa", "Val"], ["Jeremy", "Charles"],
             ["Devin", "Susan"], ["Charles", "Jamie"]]
    assert get_symmetric_pairs(pairs) == []
```

### !end-question
### !tests
```python
import unittest
from main import *

class TestChallenge(unittest.TestCase):

    def test_get_symmetric_pairs(self):
        pairs = [[11, 20], [30, 40], [5, 10], [40, 30], [10, 5]]

        self.assertEqual(get_symmetric_pairs(pairs), [[30, 40], [5, 10]])

    def test_get_symmetric_pairs_strings(self):
        pairs = [["Dan", "Kari"], ["Jeremy", "Val"], ["Jeremy", "Charles"], [
            "Devin", "Susan"], ["Kari", "Dan"], ["Devin", "Susan"]]

        self.assertEqual(get_symmetric_pairs(pairs), [["Dan", "Kari"]])

    def test_get_symmetric_pairs_no_pairs(self):
        pairs = [["Dan", "Kari"], ["Lisa", "Val"], ["Jeremy", "Charles"],
                 ["Devin", "Susan"], ["Charles", "Jamie"]]

        self.assertEqual(get_symmetric_pairs(pairs), [])
```
### !end-tests
### !explanation

An example of a working implementation:

```python
def get_symmetric_pairs(pairs):
    pairs_map = {}

    for pair in pairs:
        pairs_map[pair[0]] = pair[1]

    symmetric_pairs = []

    for key, val in pairs_map.items():
        if pairs_map.get(val) and pairs_map[val] == key:
            symmetric_pairs.append([key, val])
            pairs_map[val] = None

    return symmetric_pairs
```

### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

## Resources

- [Basics of Hash Tables](https://www.hackerearth.com/practice/data-structures/hash-tables/basics-of-hash-tables/tutorial/)
- [Video: Hash Tables and Hash Functions](https://www.youtube.com/watch?v=KyUTuwz_b7Q)

## Check for Understanding

<!-- Question Takeaway -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: F5OeNB
* title: Using Hash Tables
##### !question

What was your biggest takeaway from this lesson? Feel free to answer in 1-2 sentences, draw a picture and describe it, or write a poem, an analogy, or a story.

##### !end-question
##### !placeholder

My biggest takeaway from this lesson is...

##### !end-placeholder
### !end-challenge
<!-- prettier-ignore-end -->