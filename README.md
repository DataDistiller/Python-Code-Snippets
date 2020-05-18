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

# iterable, iterator, iteration 

interable is the item which can be interated 
Iterator is the item with method __next__ defined. item.Next
Iternation is the process involving iterator

iterator = iter(iterable)
e.g. list is iterable and not iterator. However when used in for loop its converted into iternator

An iterable is any object in Python which has an __iter__ or a __getitem__ method defined which returns an iterator or can take indexes 

An iterator is any object in Python which has a next (Python2) or __next__ method defined. That’s it. That’s an iterator

So why can we iterate over a list in a for loop?

The reason is that a list is iterable (as opposed to an iterator).

Formally, an object is iterable if it can be converted to an iterator using the built-in function iter().

Lists are one such object

x = ['foo', 'bar']
type(x)
list

y = iter(x)
type(y)
list_iterator

To conclude our discussion of for loops

for loops work on either iterators or iterables.
In the second case, the iterable is converted into an iterator before the loop starts.

# yield 

To understand what yield does, you must understand what generators are. And before you can understand generators, you must understand iterables.

Iterables

When you create a list, you can read its items one by one. Reading its items one by one is called iteration:

>>> mylist = [1, 2, 3]
>>> for i in mylist:
...    print(i)
1
2
3
mylist is an iterable. When you use a list comprehension, you create a list, and so an iterable:

>>> mylist = [x*x for x in range(3)]
>>> for i in mylist:
...    print(i)
0
1
4
Everything you can use "for... in..." on is an iterable; lists, strings, files...

These iterables are handy because you can read them as much as you wish, but you store all the values in memory and this is not always what you want when you have a lot of values.

Generators

Generators are iterators, a kind of iterable you can only iterate over once. Generators do not store all the values in memory, they generate the values on the fly:

>>> mygenerator = (x*x for x in range(3))
>>> for i in mygenerator:
...    print(i)
0
1
4
It is just the same except you used () instead of []. BUT, you cannot perform for i in mygenerator a second time since generators can only be used once: they calculate 0, then forget about it and calculate 1, and end calculating 4, one by one.

Yield

yield is a keyword that is used like return, except the function will return a generator.

>>> def createGenerator():
...    mylist = range(3)
...    for i in mylist:
...        yield i*i
...
>>> mygenerator = createGenerator() # create a generator
>>> print(mygenerator) # mygenerator is an object!
<generator object createGenerator at 0xb7555c34>
>>> for i in mygenerator:
...     print(i)
0
1
4
Here it's a useless example, but it's handy when you know your function will return a huge set of values that you will only need to read once.

To master yield, you must understand that when you call the function, the code you have written in the function body does not run. The function only returns the generator object, this is a bit tricky :-)

Then, your code will continue from where it left off each time for uses the generator.

Now the hard part:

The first time the for calls the generator object created from your function, it will run the code in your function from the beginning until it hits yield, then it'll return the first value of the loop. Then, each subsequent call will run another iteration of the loop you have written in the function and return the next value. This will continue until the generator is considered empty, which happens when the function runs without hitting yield. That can be because the loop has come to an end, or because you no longer satisfy an "if/else".

# Itertools, your best friend

The itertools module contains special functions to manipulate iterables. Ever wish to duplicate a generator? Chain two generators? Group values in a nested list with a one-liner? Map / Zip without creating another list?

Then just import itertools.

An example? Let's see the possible orders of arrival for a four-horse race:

>>> horses = [1, 2, 3, 4]
>>> races = itertools.permutations(horses)
>>> print(races)
<itertools.permutations object at 0xb754f1dc>
>>> print(list(itertools.permutations(horses)))
[(1, 2, 3, 4),
 (1, 2, 4, 3),
 (1, 3, 2, 4),
 (1, 3, 4, 2),
 (1, 4, 2, 3),
 (1, 4, 3, 2),
 (2, 1, 3, 4),
 (2, 1, 4, 3),
 (2, 3, 1, 4),
 (2, 3, 4, 1),
 (2, 4, 1, 3),
 (2, 4, 3, 1),
 (3, 1, 2, 4),
 (3, 1, 4, 2),
 (3, 2, 1, 4),
 (3, 2, 4, 1),
 (3, 4, 1, 2),
 (3, 4, 2, 1),
 (4, 1, 2, 3),
 (4, 1, 3, 2),
 (4, 2, 1, 3),
 (4, 2, 3, 1),
 (4, 3, 1, 2),
 (4, 3, 2, 1)]
Understanding the inner mechanisms of iteration

Iteration is a process implying iterables (implementing the __iter__() method) and iterators (implementing the __next__() method). Iterables are any objects you can get an iterator from. Iterators are objects that let you iterate on iterables.



# yield vs return
