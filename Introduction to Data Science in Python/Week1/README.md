# Applied-Data-Science-with-Python-Specialization

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

## Lamdas - Anonymous Functions