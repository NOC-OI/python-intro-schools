---
title: Making Choices
---

::::::::::::::::::::::::::::::::::::::::::  prereq
## About this lesson

#### Questions:
- "How can my programs do different things based on data values?"

#### Objectives:
- "Write conditional statements including `if`, `elif`, and `else` branches."
- "Correctly evaluate expressions containing `and` and `or`."

#### Keypoints:
- "Use `if condition` to start a conditional statement, `elif condition` to
   provide additional tests, and `else` to provide a default."
- "The bodies of the branches of conditional statements must be indented."
- "Use `==` to test for equality."
- "`X and Y` is only true if both `X` and `Y` are true."
- "`X or Y` is true if either `X` or `Y`, or both, are true."
- "Zero, the empty string, and the empty list are considered false;
   all other numbers, strings, and lists are considered true."
- "`True` and `False` represent truth values."

::::::::::::::::::::::::::::::::::::::::::::::::::

In our previous lessons, we examined the seasonal behaviour of sea waves.
How can we use this data to make practical decisions?

How can we use Python to identify thresholds, and take a different action for each?
In this lesson, we'll learn how to write code that runs only when certain conditions are true.


## Conditionals

We can ask Python to take different actions, depending on a condition, with an `if` statement:

```python
num = 37
if num 100:
    print("greater")
else:
    print("not greater")
print('done')
```


```output
not greater
done
```


The second line of this code uses the keyword `if` to tell Python that we want to make a choice.
If the test that follows the `if` statement is true,
the body of the `if`
(i.e., the set of lines indented underneath it) is executed, and "greater" is printed.
If the test is false,
the body of the `else` is executed instead, and "not greater" is printed.
Only one or the other is ever executed before continuing on with program execution to print "done":

![](fig/python-flowchart-conditional.png){alt="A flowchart diagram of the if-else construct that tests if variable num is greater than 100"}

Conditional statements don't have to include an `else`.
If there isn't one,
Python simply does nothing if the test is false:

```python
num = 53
print('before conditional...')
if num 100:
    print(num, "is greater than 100")
print('...after conditional')
```


```output
before conditional...
...after conditional
```


We can also chain several tests together using `elif`,
which is short for "else if".
The following Python code uses `elif` to print the sign of a number.

```python
num = -3

if num 0:
    print(num, "is positive")
elif num == 0:
    print(num, "is zero")
else:
    print(num, "is negative")
```


```output
-3 is negative
```


Note that to test for equality we use a double equals sign `==`
rather than a single equals sign `=` which is used to assign values.

::::::::::::::::::::::::::::::::::::::::::  prereq

## Comparing in Python

Along with the `>` and `==` operators we have already used for comparing values in our
conditionals, there are a few more options to know about:

- `>`: greater than
- `<`: less than
- `==`: equal to
- `!=`: does not equal
- `>=`: greater than or equal to
- `<=`: less than or equal to
::::::::::::::::::::::::::::::::::::::::::::::::::

We can also combine tests using `and` and `or`.
`and` is only true if both parts are true:

```python
if (1 0) and (-1 >= 0):
    print("both parts are true")
else:
    print("at least one part is false")
```


```output
at least one part is false
```


while `or` is true if at least one part is true:

```python
if (1 < 0) or (1 >= 0):
    print("at least one test is true")
```


```output
at least one test is true
```


## `True` and `False`
`True` and `False` are special words in Python called `booleans`,
which represent truth values. A statement such as `1 < 0` returns
the value `False`, while `-1 < 0` returns the value `True`.

## Checking our Data

Now that we've seen how conditionals work,
we can use them to look for thresholds in our wave data.
We are about to use functions provided by the `numpy` module again.
Therefore, if you're working in a new Python session, make sure to load the
module, and load and reshape one of the data files:

```python
import numpy

data = numpy.loadtxt(fname = "waves_80s.csv", delimiter=",")
data = numpy.reshape(data[:,2], [10,12])
```


If you are operating a boat, for carrying passengers of working offshore, you need to know that it will be save to go to sea.
Ideally you wouldn't want to have passengers transported if the wave height is above 3 metres

Let's look at our wave data, and find which months we can operate the boats, based on the monthly mean wave-height.

We could look at each month individually:

```python
data = numpy.loadtxt(fname='data/wavesmonthly.csv', delimiter=',', skiprows=1)
reshaped_data = numpy.reshape(data[:,2], [37,12])

month0 = numpy.mean(reshaped_data, axis=0)[0]

if month0 < 3:
    print("Can take passengers this month")
```


Survey vehicles can operate in stormier waters, with wave heights up to 4m

```python
elif month0 < 4:
    print("Can take survey vehicles (but not passengers)")
```


And if neither of these conditions are true, then it's too stormy, and nothing can go out.

```python
else:
    print("Can't take any boats out to sea")
```


Let's test that out for February:

```python
month1 = numpy.mean(reshaped_data, axis=0)[1]

if month1 < 3:
    print("Can take passengers this month")
elif month1 < 4:
    print("Can take survey vehicles (but not passengers)")
else:
    print("Can't take any boats out to sea")
```


```output
Can't take any boats out to sea
```


Now let's try for June

```python
month5 = numpy.mean(reshaped_data, axis=0)[5]

if month5 < 3:
    print("Can take passengers this month")
elif month5 < 4:
    print("Can take survey vehicles (but not passengers)")
else:
    print("Can't take any boats out to sea")
```


```output
Can take passengers this month
```


Notice how the statement stops as soon as it reaches a condition which is `True`.

We could test for all months less manually, using a `for loop`:

```python
for month_index, monthly_waveheight in enumerate(numpy.mean(reshaped_data, axis=0)):
    if monthly_waveheight < 3:
        print(f"Month {month_index}: we can take passengers this month")
    elif monthly_waveheight < 4:
        print(f"Month {month_index}: we can take survey vehicles (but not passengers) this month")
    else:
        print(f"Month {month_index}: we can't take any boats out to sea this month")
```


```output
Month 0: can't take any boats out to sea this month
Month 1: can't take any boats out to sea this month
Month 2: can't take any boats out to sea this month
Month 3: can take survey vehicles (but not passengers) this month
Month 4: can take passengers this month
Month 5: can take passengers this month
Month 6: can take passengers this month
Month 7: can take passengers this month
Month 8: can take passengers this month
Month 9: can take survey vehicles (but not passengers) this month
Month 10: can take survey vehicles (but not passengers) this month
Month 11: can't take any boats out to sea this month
```


The `enumerate` function is the _Pythonic_ way of getting the index of values in a loop - in this case it allows us to
list the month number in the output. We need a variable to store this value in, which we're calling `month_index`. Because the loop returns two
variables form each iteration (month index and monthly waveheight), we need two variables.

We can see that we could suggest a timetable for passenger ferries in
May - September (inclusive), we could plan to take survey boats out in April, October, and November; and we should not plan
any sea-going activities in January, February, March, or December.

This is a relatively crude example, but shows how we can use these programming constructs to help
make some decisions using the data.

In this way,
we have asked Python to do something different depending on the condition of our data.
Here we printed messages in all cases,
but we could also imagine not using the `else` catch-all
so that messages are only printed when something is wrong,
freeing us from having to manually examine every plot for features we've seen before.

:::::::::::::::::::::::::::::::::::::::  challenge

## How Many Paths?

Consider this code:

```python
if 4 5:
    print("A")
elif 4 == 5:
    print("B")
elif 4 < 5:
    print("C")
```


Which of the following would be printed if you were to run this code?
Why did you pick this answer?

1.  A
2.  B
3.  C
4.  B and C

:::::::::::::::  solution
C gets printed because the first two conditions, `4 5` and `4 == 5`, are not true,
but `4 < 5` is true.
:::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## What Is Truth?

`True` and `False` booleans are not the only values in Python that are true and false.
In fact, *any* value can be used in an `if` or `elif`.
After reading and running the code below,
explain what the rule is for which values are considered true and which are considered false.

```python
if '':
    print("empty string is true")
if 'word':
    print("word is true")
if []:
    print("empty list is true")
if [1, 2, 3]:
    print("non-empty list is true")
if 0:
    print("zero is true")
if 1:
    print("one is true")
```


:::::::::::::::  solution
```output
word is true
non-empty list is true
one is true
```


A non-empty string, non-empty list and non-zero variable all evaluate to True. An empty string, empty list and zero all evaluate to False.
:::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## That's Not Not What I Meant

Sometimes it is useful to check whether some condition is not true.
The Boolean operator `not` can do this explicitly.
After reading and running the code below,
write some `if` statements that use `not` to test the rule
that you formulated in the previous challenge.

```python
if not '':
    print("empty string is not true")
if not 'word':
    print("word is not true")
if not not True:
    print("not not True is true")
```


:::::::::::::::  solution
```output
empty string is not true
not not True is true
```

The not of an empty string evaluates to True. Evaluating not twice converts back to original value, so doing not twice on True is True.
:::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Close Enough

Write some conditions that print `True` if the variable `a` is within 10% of the variable `b`
and `False` otherwise.
Compare your implementation with your partner's:
do you get the same answer for all possible pairs of numbers?


#### Hint
There is a [built-in function `abs`][abs-function] that returns the absolute value of
a number:
```python
print(abs(-12))
```

```output
12
```

:::::::::::::::  solution
```python
a = 5
b = 5.1

if abs(a - b) <= 0.1 * abs(b):
    print("True")
else:
    print("False")
```

:::::::::::::::::::::::::

:::::::::::::::  solution
```python
print(abs(a - b) <= 0.1 * abs(b))
```


This works because the Booleans `True` and `False`
have string representations which can be printed.
:::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## In-Place Operators

Python (and most other languages in the C family) provides
[in-place operators](learners/reference.md#in-place-operators)
that work like this:

```python
x = 1  # original value
x += 1 # add one to x, assigning result back to x
x *= 3 # multiply x by 3
print(x)
```


```output
6
```


Write some code that sums the positive and negative numbers in a list separately,
using in-place operators.
Do you think the result is more or less readable
than writing the same without in-place operators?

:::::::::::::::  solution
```python
positive_sum = 0
negative_sum = 0
test_list = [3, 4, 6, 1, -1, -5, 0, 7, -8]
for num in test_list:
    if num 0:
        positive_sum += num
    elif num == 0:
        pass
    else:
        negative_sum += num
print(positive_sum, negative_sum)
```


Here `pass` means "don't do anything".
In this particular case, it's not actually needed, since if `num == 0` neither
sum needs to change, but it illustrates the use of `elif` and `pass`.
:::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Sorting a List Into Buckets

In our `data` folder, we have some CSV files (those with .csv file extensions), and one NetCDF file (with a .nc file extension).
We'd like to break these
files into two lists called `csv_files` and `nc_files`,
respectively.

Add code to the template below to do this. Note that the string method
[`startswith`](https://docs.python.org/3/library/stdtypes.html#str.endswith)
returns `True` if and only if the string it is called on ends with the string
passed as an argument, that is:

```python
'String'.endswith('ing')
```

```output
True
```

But
```python
'String'.endswith('ING')
```

```output
False
```

Use the following Python code as your starting point:
```python
filenames = ['wavesmonthly.csv',
         'waves_00s.csv',
         'waves_10s.csv',
         'waves_80s.csv',
         'waves_90s.csv',
         'multyear_hs_avg.nc']
csv_files = []
nc_files = []
other_files = []
```


Your solution should:

1.  loop over the names of the files
2.  figure out which group each filename belongs in
3.  append the filename to that list

In the end the two lists should be:

```python
csv_files = ['waves_00s.csv', 'waves_10s.csv', 'waves_80s.csv', 'waves_90s.csv', 'wavesmonthly.csv']
nc_files = ['multyear_hs_avg.nc']
```


:::::::::::::::  solution
```python
filenames = ['wavesmonthly.csv',
        'waves_00s.csv',
        'waves_10s.csv',
        'waves_80s.csv',
        'waves_90s.csv',
        'multyear_hs_avg.nc']
csv_files = []
nc_files = []
other_files = []

for filename in filenames:
    if filename.endswith('csv'):
        csv_files.append(filename)
    elif filename.endswith('nc'):
        nc_files.append(filename)
    else:
        other_files.append(filename)

print("csv_files:", csv_files)
print("nc_files:", nc_files)
print("other_files:", other_files)
```


```output
csv_files: ['wavesmonthly.csv', 'waves_00s.csv', 'waves_10s.csv', 'waves_80s.csv', 'waves_90s.csv']
nc_files: ['multyear_hs_avg.nc']
other_files: []
```

:::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Counting Vowels

1. Write a loop that counts the number of vowels in a character string.
2. Test it on a few individual words and full sentences.
3. Once you are done, compare your solution to your neighbor's.
   Did you make the same decisions about how to handle the letter 'y'
   (which some people think is a vowel, and some do not)?

:::::::::::::::  solution
```python
vowels = 'aeiouAEIOU'
sentence = 'Mary had a little lamb.'
count = 0
for char in sentence:
    if char in vowels:
        count += 1

print("The number of vowels in this string is " + str(count))
```

:::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::

[abs-function]: https://docs.python.org/3/library/functions.html#abs
