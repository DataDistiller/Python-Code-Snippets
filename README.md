# Python-Code-Snippets

Filter out of dir function


import numpy as np
[a for a in dir(np) if 'rand' in a]




[a for a in dir(list) if re.match(r'__\w{,2}__',a)]
