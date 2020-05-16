# Python-Code-Snippets

Filter out of dir function


import numpy as np
[a for a in dir(np) if 'rand' in a]


[a for a in dir(list) if re.match(r'__\w{,2}__',a)]



some_list = ['a', 'b', 'c', 'b', 'd', 'm', 'n', 'n']
duplicates = set([x for x in some_list if some_list.count(x) > 1])
print(duplicates)
# Output: set(['b', 'n'])


Unpacking tupple OR list

Unpacking works as long as count of assigned variables and values  match. in this case its 3 on both sides.

integers = (10, 20, 30)
x, y, z = integers
x
10

integers = [10, 20, 30]
x, y, z = integers
y
