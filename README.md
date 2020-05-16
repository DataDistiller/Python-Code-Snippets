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

# mcase_frequency == {'a': 17, 'z': 3, 'b': 34}

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

# Output: <generator object <genexpr> at 0x7fdaa8e407d8>
for x in multiples_gen:
  print(x)
  # Outputs numbers

