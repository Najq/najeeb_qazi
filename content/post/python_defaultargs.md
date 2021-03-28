+++
author = "Najeeb Qazi"
title = "Python default arguments can be...tricky"
date = "2021-01-05"
description = "Making a note so that I don't make the same mistake again"
tags = [
    "python",
]
+++

Debugging is fun, and according to me debugging time exponentially increases if the code was written in a sloppy manner.
Point being...python default arguments can be tricky to deal with.
If the code you've written is - 
{{< highlight python3  >}}
def append_to(element, to=[]):
    to.append(element)
    return to
{{< / highlight >}}

**You might expect this to -**
{{< highlight python3  >}}
my_list = append_to(12)
print(my_list)

my_other_list = append_to(42)
print(my_other_list)
{{< / highlight >}}
**give this output -**
{{< highlight python3  >}}
[12]
[42]
{{< / highlight >}}
**But, what actually happens is -**
{{< highlight python3  >}}
[12]
[12, 42]
{{< / highlight >}}
A new list is only created once during the function definition, and the same reference is used for future calls. So...if you use a mutable default argument, it will have the same reference for all the future function calls. Pretty sucky. That's why follow this code pattern -
{{< highlight python3  >}}
def append_to(element, to=None):
    if to is None:
        to = []
    to.append(element)
    return to
{{< / highlight >}}

Buh bye!



