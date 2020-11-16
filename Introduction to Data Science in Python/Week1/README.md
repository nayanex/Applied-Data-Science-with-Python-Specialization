# Introduction to Data Science in Python

## Functional Programming

In Python you can assign a variable to a function. By assigning a variable to a function, you can pass that variable into other functions allowing some basic functional programming. Here is an example where we define a function to add numbers, then we assign that function to a variable, and then we invoke that variable.

```python
def add_numbers(x, y):
    return x + y

a = add_numbers
print(a(1, 2))
```

The **map** function is one of the basis for functional programming in Python. Functional programming is a programming paradigm in which you explicitly declare all parameters which could change through execution of a given function. Thus functional programming is referred to as being **side-effect free**, because there is a software contract that describes what can actually change by calling a function. Now, Python isn't a functional programming language in the pure sense. Since you can have many side effects of functions, and certainly you don't have to pass in the parameters of everything that you're interested in changing.

But functional programming causes one to think more heavily while chaining operations together. And this really is a sort of underlying theme in much of data science and date cleaning in particular. So, functional programming methods are often used in Python, and it's not uncommon to see a parameter for a function, be a function itself. The map built-in function is one example of a functional programming feature of Python, that I think ties together a number of aspects of the language. The map function signature looks like this. The first parameters of function that you want executed, and the second parameter, and every following parameter, is something which can be iterated upon.

All the iterable arguments are unpacked together, and passed into the given function. That's a little cryptic, so let's take a look at an example. Imagine we have two list of numbers, maybe prices from two different stores on exactly the same items. And we wanted to find the minimum that we would have to pay if we bought the cheaper item between the two stores. To do this, we could iterate through each list, comparing items and choosing the cheapest. With map, we can do this comparison in a single statement.

But when we go to print out the map, we see that we get an odd reference value instead of a list of items that we're expecting. This is called **lazy evaluation**. In Python, the map function returns to you a map object. It doesn't actually try and run the function min on two items, until you look inside for a value. This is an interesting design pattern of the language, and it's commonly used when dealing with big data. This allows us to have very efficient memory management, even though something might be computationally complex.

```python
store1 = [10.00, 11.00, 12.34, 2.34]
store2 = [9.00, 11.10, 12.34, 2.01]
cheapest = map(min, store1, store2)
cheapest

# <map at 0x7f69185fe438>
```

Now let's iterate through the map object to see the values.

```python
for item in cheapest:
    print(item)
# 9.0
# 11.0
# 12.34
# 2.01
```

Maps are iterable, just like lists and tuples, so we can use a for loop to look at all of the values in the map. This passing around of functions and data structures which they should be applied to, is a hallmark of functional programming. It's very common in data analysis and cleaning. 

### Example 1

Here is a list of faculty. Can you write a function and apply it using `map()` to get a list of all faculty titles and last names (e.g. ['Dr. Brooks', 'Dr. Collins-Thompson', …]) ?

```python
people = ['Dr. Christopher Brooks', 'Dr. Kevyn Collins-Thompson', 'Dr. VG Vinod Vydiswaran', 'Dr. Daniel Romero']

def split_title_and_name(person):
    person_names = person.split(' ')
    return person_names[0] + person_names[-1]
    
list(map(split_title_and_name, people))

# ['Dr.Brooks', 'Dr.Collins-Thompson', 'Dr.Vydiswaran', 'Dr.Romero']
```

## Lambdas - Anonymous Functions

Lambda's are Python's way of creating anonymous functions. These are the same as other functions, but they have no name. The intent is that they're simple or short lived and it's easier just to write out the function in one line instead of going to the trouble of creating a named function.

Note that you can't have default values for lambda parameters and you can't have complex logic inside of the lambda itself because you're limited to a single expression. So lambdas are really much more limited than full function definitions. But they're very useful for simple little data cleaning tasks. 


### Example 1 

Convert the `split_title_and_name` into a lambda

```python
people = ['Dr. Christopher Brooks', 'Dr. Kevyn Collins-Thompson', 'Dr. VG Vinod Vydiswaran', 'Dr. Daniel Romero']

def split_title_and_name(person):
    return person.split()[0] + ' ' + person.split()[-1]

#option 1
for person in people:
    print(split_title_and_name(person) == (lambda x: x.split()[0] + ' ' + x.split()[-1])(person))

#option 2
list(map(split_title_and_name, people)) == list(map(lambda person: person.split()[0] + ' ' + person.split()[-1], people))

# True
# True
# True
# True
# True
```

### Resources

https://stackoverflow.com/questions/13669252/what-is-key-lambda

##  list comprehension 

Just like with lambdas, list comprehensions are a condensed format which may offer readability and performance benefits 

### Example 1

Why don’t you try converting a function into a list comprehension.

```python
def times_tables():
    lst = []
    for i in range(10):
        for j in range (10):
            lst.append(i*j)
    return lst

times_tables() == [j*i for i in range(10) for j in range(10)]
```

### Example 2

Here’s a harder question which brings a few things together.

Many organizations have user ids which are constrained in some way. Imagine you work at an internet service provider and the user ids are all two letters followed by two numbers (e.g. aa49). Your task at such an organization might be to hold a record on the billing activity for each possible user.

Write an initialization line as a single list comprehension which creates a list of all possible user ids. Assume the letters are all lower case.

```python
lowercase = 'abcdefghijklmnopqrstuvwxyz'
digits = '0123456789'

correct_answer = [a+b+c+d for a in lowercase for b in lowercase for c in digits for d in digits]

correct_answer[:50] # Display first 50 ids
```

### Resources

https://www.geeksforgeeks.org/nested-list-comprehensions-in-python/#:~:text=It%20is%20a%20smart%20and,similar%20to%20nested%20for%20loops.


## Quiz

### Q1

What will be the output of the following code?

```python
import re
string = 'bat, lat, mat, bet, let, met, bit, lit, mit, bot, lot, mot'
result = re.findall('b[ao]t', string)
print(result)

# ['bat', 'bot']
```

- [ ] ['bat', 'bot']
- [ ] bat, bet, bit, bot'
- [x] 'bat, bot'
- [ ] 'bat', 'bet', 'bit', 'bot']

### Q2

![alt text](https://mcq-s3-bucket.s3.amazonaws.com/static/week1/images/quiz/quiz1_q1.png "Euclidian Distance")

Assume `a` and `b` are two (20, 20) numpy arrays. The L2-distance (defined above) between two equal dimension arrays can be calculated in python as follows:


```python
def l2_dist(a, b):
    result = ((a - b) * (a - b)).sum()
    result = result ** 0.5
    return result
```

Which of the following expressions using this function will **give an error?**

```python
a = np.random.rand(20,20)
b = np.random.rand(20,20)
```

- [x] l2_dist(np.reshape(a, (20 * 20)), np.reshape(b, (20 * 20, 1)))
- [ ] l2_dist(np.reshape(a, (20 * 20)), np.reshape(b, (20 * 20)))
- [ ] l2_dist(a, b)
- [ ] l2_dist(a.T, b.T)

### Q3

Consider the following variables in Python:

```python
a1 = np.random.rand(4)
a2 = np.random.rand(4, 1)
a3 = np.array([[1, 2, 3, 4]])
a4 = np.arange(1, 4, 1)
a5 = np.linspace(1 ,4, 4)
```

Which of the following statements regarding these variables is correct?


- [ ] a3.shape == a4.shape
- [ ] a1.shape == a2.shape
- [x] a5.shape == a1.shape
- [ ] a4.ndim() == 1

### Q4

Which of the following is the correct output for the code given below?

```python
import numpy as np

old = np.array([[1, 1, 1], [1, 1, 1]])
new = old
new[0, :2] = 0
print(old)
```

- [ ] [[1 1 1][1 1 1]]
- [x] [[0 0 1][1 1 1]]
- [ ] [[0 1 1][0 1 1]]
- [ ] [1 1 0][1 1 0]]

### Q5

Given the 6x6 NumPy array r shown below, which of the following options would slice the shaded elements?

![alt text](https://mcq-s3-bucket.s3.amazonaws.com/static/week1/images/quiz/quiz1_q4.png"6x6 array")

```python
r = np.arange(0,36).reshape(6,6)
```

- [ ] r[[2,4],[2,4]]
- [ ] r[[2,3],[2,3]]
- [ ] r[2:3,2:3]
- [x] r[2:4,2:4]

### Q6

```python
import re
s = 'ACBCAC'
```

For the given string, which of the following regular expressions can be used to check if the string starts with 'AC'?

- [ ] re.findall('[^A]C', s)
- [ ] re.findall('^[AC]', s)
- [x] re.findall('^AC', s)
- [ ] re.findall('AC', s)

### Q7

What will be the output of the variable `L` after the following code is executed?


```python
import re

s = 'ACAABAACAAAB'
result = re.findall('A{1,2}', s)
L = len(result)
```

- [ ] 8
- [x] 5
- [ ] 12
- [ ] 4

### Q8

Which of the following is the correct regular expression to extract all the phone numbers from the following chunk of text:

```python
"""
Office of Research Administration: (734) 647-6333 | 4325 North Quad
Office of Budget and Financial Administration: (734) 647-8044 | 309 Maynard, Suite 205
Health Informatics Program: (734) 763-2285 | 333 Maynard, Suite 500
Office of the Dean: (734) 647-3576 | 4322 North Quad
UMSI Engagement Center: (734) 763-1251 | 777 North University
Faculty Adminstrative Support Staff: (734) 764-9376 | 4322 North Quad
"""

# ['(734) 647-6333', '(734) 647-8044', '(734) 763-2285', '(734) 647-3576', '(734) 763-1251', '(734) 764-9376']
```

- [x] pattern1 = "[(]\d{3}[)]\s\d{3}[-]\d{4}"
- [ ] pattern2 = "[(]\d{3}[)]\d{3}[-]\d{4}"
- [ ] pattern3 = "\d{3}[-]\d{3}[-]\d{4}"
- [ ] pattern4 = "\d{3}\s\d{3}[-]\d{4}"

### Q9

Which of the following regular expressions can be used to get the domain names (e.g. google.com, www.baidu.com) from the following sentence?

```python
'I refer to https://google.com and I never refer http://www.baidu.com if I have to search anything'
```

- [ ] pattern1 = "(?<=https:\/\/)([A-Za-z0-9.]*)"
- [ ] pattern2 = "(?<=https:\/\/)([.]*)"
- [x] pattern3 = "(?<=[https]:\/\/)([A-Za-z0-9.]*)"
- [ ] pattern4 = "(?<=https:\/\/)([A-Za-z0-9]*)"

### Q10

The text from the Canadian Charter of Rights and Freedoms section 2 lists the fundamental freedoms afforded to everyone. Of the four choices provided to replace X in the code below, which would accurately count the number of fundamental freedoms that Canadians have?

```python
text=r'''Everyone has the following fundamental freedoms:
(a) freedom of conscience and religion;
(b) freedom of thought, belief, opinion and expression, including freedom of the press and other media of communication;
(c) freedom of peaceful assembly; and
(d) freedom of association.'''

import re

pattern = X
print(len(re.findall(pattern,text)))
```

- [ ] pattern1 = '[a-d]'
- [x] pattern2 = 'freedom'
- [ ] pattern3 = '\(.\) '
- [ ] pattern4 = '(.)'

