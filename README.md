# Python-Code-Snippets



Filter out of dir function : Idea is to understand return type, and use function/methods of that object. Here dir function returns list, and any of the list functions ( such as list comprehension) can be applied to output. Think about piping further. As list comprehension does only one thing - return another list .


import numpy as np
[a for a in dir(np) if 'rand' in a]

[a for a in dir(list) if re.match(r'__\w{,2}__',a)]


some_list = ['a', 'b', 'c', 'b', 'd', 'm', 'n', 'n']
duplicates = set([x for x in some_list if some_list.count(x) > 1])
print(duplicates)

Output: set(['b', 'n'])


Unpacking tupple OR list

Unpacking works as long as count of assigned variables and values  match. in this case its 3 on both sides.

integers = (10, 20, 30)
x, y, z = integers
x
10

integers = [10, 20, 30]
x, y, z = integers
y

# Comprehension

list comprehensions
dictionary comprehensions
set comprehensions
generator comprehensions

Syntax
variable = [f(x) for x in xs if x == 2]

List Comprehension

multiples = [i for i in range(30) if i % 3 == 0]
print(multiples)

squared = [x**2 for x in range(10)]

Dictionary Comprehension
Key value pairs

mcase = {'a': 10, 'b': 34, 'A': 7, 'Z': 3}

mcase_frequency = {
    k.lower(): mcase.get(k.lower(), 0) + mcase.get(k.upper(), 0)
    for k in mcase.keys()
}

mcase_frequency == {'a': 17, 'z': 3, 'b': 34}

You can also quickly switch keys and values of a dictionary:

abdict ={'a': 17, 'z': 3, 'b': 34}
badict={v: k for k, v in abdict.items()}
badict

Set Comprehension

squared = {x**2 for x in [1, 1, 2]}
print(squared)
( set will de dup its items first)

Generator Comprehension

multiples_gen = (i for i in range(30) if i % 3 == 0)
print(multiples_gen)

Output: <generator object <genexpr> at 0x7fdaaad07d8>
    
for x in multiples_gen:
  print(x)
  Outputs numbers

# Slice Notation

a[start:stop]  # items start through stop-1
a[start:]      # items start through the rest of the array
a[:stop]       # items from the beginning through stop-1
a[:]           # a copy of the whole array

a[start:stop:step] # start through not past stop, by step

The key point to remember is that the :stop value represents the first value that is not in the selected slice. So, the difference between stop and start is the number of elements selected (if step is 1, the default).

The other feature is that start or stop may be a negative number, which means it counts from the end of the array instead of the beginning. So:

a[-1]    # last item in the array
a[-2:]   # last two items in the array
a[:-2]   # everything except the last two items
Similarly, step may be a negative number:

a[::-1]    # all items in the array, reversed
a[1::-1]   # the first two items, reversed
a[:-3:-1]  # the last two items, reversed
a[-3::-1]  # everything except the last two items, reversed
Python is kind to the programmer if there are fewer items than you ask for. For example, if you ask for a[:-2] and a only contains one element, you get an empty list instead of an error. Sometimes you would prefer the error, so you have to be aware that this may happen.

Relation to slice() object

The slicing operator [] is actually being used in the above code with a slice() object using the : notation (which is only valid within []), i.e.:

a[start:stop:step]
is equivalent to:

a[slice(start, stop, step)]
Slice objects also behave slightly differently depending on the number of arguments, similarly to range(), i.e. both slice(stop) and slice(start, stop[, step]) are supported. To skip specifying a given argument, one might use None, so that e.g. a[start:] is equivalent to a[slice(start, None)] or a[::-1] is equivalent to a[slice(None, None, -1)].

While the :-based notation is very helpful for simple slicing, the explicit use of slice() objects simplifies the programmatic generation of slicing.
