# shedding-python
Small Python Ideas contained in jupyter notebooks 


```python
def the_walrus():
	return """
			   ___
            .-9 9 `\
          =(:(::)=  ;
            ||||     \
            ||||      `-.
           ,\|\|         `,
          /                \
         ;                  `'---.,
         |                         `\
         ;                     /     |
         \                    |      /
  jgs     )           \  __,.--\    /
       .-' \,..._\     \`   .-'  .-'
      `-=``      `:    |   /-/-/`
                   `.__/
"""
```

---
Here's a Pattern in python you've probably seen before!

```python
from functools import cache
from datetime import datetime
from random import choice
  

def build_data():
	return [{"a": choice([None, i]), "b": choice([None, i]), "c": choice([None, i])} for i in range(100000000)]

def the_way_you_have_always_done_it(data):
	return [d.get("a") for d in data if d.get("a")]

def the_walrus_way(data):
	return [x for d in if (x := d.get("a"))]
```

---

What about something syntactically helpful?

```python
from dataclasses import dataclass


@dataclass
class ContactInfo:
    first_name: str
    middle_name: str
    last_name: str
    full_name: str
    address: str


def address_book(list_of_users: list[dict]) -> list[ContactInfo]:
    return [
        ContactInfo(
            first_name=(f_name := user.get("fname")),
            last_name=(l_name := user.get("lname")),
            middle_name=(m_name := user.get("mname")),
            full_name=" ".join([name_segment for name_segment in [f_name, m_name, l_name] if name_segment]),
            address=user.get("address"),
        )
        for user in list_of_users
    ]
```

A  check with an assign:
```python
def check_length_of_n(n: list[int]) -> bool:
	if (check := len(n)) > 2:
		LOG.error(f"N is too long: {check} ")
		return False
	return True
```

Accumulate some things:
```python
def grow():
	values = [1,2,3,4,5]
	total = 0
	return [total := total + value for value in values]

assert grow() == [1,3,6,10,15]
```

Stupid Python Tricks with Dataclasses:
```python
from dataclasses import dataclass
from enum import StrEnum

class Environment(StrEnum):
	DEV = "DEV"
	TEST = "TEST"
	PROD = "PROD"

@dataclass(frozen=True)
class Configuration:
	environment: Environment
	config_option_one: str
	config_option_two: str
	config_option_three: str


```

Truthy assignment:
```python
import random

def do_a_thing_because_its_true(x: int):
	return x**2

def some_function_which_might_return_an_int() -> int | bool:
	pick_a_number = random.choice([1, 2, 3, 4, 5])
	return random.choice([pick_a_number, False])

if x := (some_function_which_might_return_an_int() or some_function_which_might_return_an_int()):
	assert x**2 == do_a_thing_because_its_true(x)
else:
	assert x is False
```
