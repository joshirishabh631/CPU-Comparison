# **CPU Performance Comparison of Various Loops in Python: Analysis and Best Use Cases**




## _Document created by- Rishabh Joshi_



## **Table of Content**  
<!-- TOC -->
1- [Objective](#objective)

2- [Understanding Loops](#understanding-loops)

- [While loop](#while-loop)

- [For loop](#for-loop)

3- [Uses of Loops](#uses-of-loops)

4- [CPU Comparison](#cpu-comparison)

- [time module](#Time-module)

- [psutil module](#psutil-module)

- [cprofile module](#cprofile-module)
  
- [Big O Notation for Python Loops](#Big-O-Notation-for-Python-Loops)

- [Concluding CPU Comparison](#Conclusion)

5- [Best Use Cases](#best-use-cases)

6- [Conclusion](#conclusion)

7- [References](#references)
<!-- /TOC -->

## **Objective**

This document aims to compare the CPU performance of for loops and while loops in Python. By evaluating their execution time and resource usage, we will identify which loop is more efficient and when to use each type effectively.

## **Understanding Loops**
 
Loops are used to repeatedly execute a block of code as long as a certain condition is met. This is useful for tasks that require repeating actions, such as iterating over a list, performing calculations multiple times, or automating repetitive processes.Loops provide a way to automate repetitive tasks, making code cleaner and more efficient.

There are basically two different Loops in Python. 

**1- While Loop**

**2- For Loop**

## While Loop 


A while loop is a way to repeat actions in your program until something changes. It keeps running a block of code as long as a certain condition remains true. Once that condition becomes false, the loop stops.

**Example code -**
```python
secret_number = 99
guess = 0

while guess != secret_number:
    guess = int(input("Guess the secret number (1-100): "))
    if guess == secret_number:
        print("Congrats! You guessed it right!")
    elif guess > 100 or guess < 1:
        print("Invalid input: Please enter a number between 1 and 100.")
    else:
        print("Try again!")

print("Game over.")
```
#### Output -

![Program Output](Untitled.png)


## For Loop 

In Python, a for loop is used to repeat a block of code a certain number of times or to go through items in a collection (like a list, string, or range of numbers). It's great for when you know exactly how many times you want to loop.

**Example code -**
```python

squares = [x**2 for x in range(11)]

print(squares)

```
#### Output
![Program Output](forloop.png)

## Uses of Loops 

* Repeating Actions: Run the same code multiple times.


* Counting Numbers: Generate sequences of numbers.


* Condition-Based Repetition: Continue running until a condition changes.


* Summing Values: Add up or calculate values.

  
## **CPU Comparison** 
CPU comparison means looking at how well the CPU (the brain of the computer) handles different pieces of code. This helps us see which parts of the code run faster or slower and which parts make the CPU work harder. By comparing, we can improve the code to make it run more efficiently

## **CPU Comparison: For loop VS While loop**

### time module

* **Firstly we are comparing For and While loop as per the time taken by both of them while execution. We have used **"Time"** Module for checking that how much time did For loop takes to be executed and same for while loop.**

**Example code-** 
```python
import time

# For Loop
start_time = time.time()
for i in range(100000000):
    pass
for_loop_time = time.time() - start_time

# While Loop
start_time = time.time()
i = 0
while i < 100000000:
    i += 1
while_loop_time = time.time() - start_time

print(f"For loop time: {for_loop_time}")
print(f"While loop time: {while_loop_time}")
```
#### Output-
![Program Output](timeit.png)

### psutil module 

* **Now, showing CPU usage of For and While Loop by using **"psutill" (process and system utilities)** module, which fetch cpu usage details from API's which are being use by any operating system . ex- (cat /proc/stat)- we can use this command for checking CPU usage. psutill module fetch data from /proc/stat and give usage details for execution of loops.**

**Example code**
```python
import psutil

iterations = 100000000

start_cpu_for = psutil.cpu_percent(interval=None)

for i in range(iterations):
    pass  

end_cpu_for = psutil.cpu_percent(interval=None)

start_cpu_while = psutil.cpu_percent(interval=None)

i = 0
while i < iterations:
    i += 1

end_cpu_while = psutil.cpu_percent(interval=None)

print(f"For loop CPU usage: {end_cpu_for - start_cpu_for}%")
print(f"While loop CPU usage: {end_cpu_while - start_cpu_while}%")
```


#### Output-
![Program Output](psutil.png)

### cprofile module

* **Now, we will use **"cproile"** module to see the CPU comparison between for and while loops. cprofile module helps to give various aspects as :**
    
    ncalls: Number of times a function was called ,
    
    tottime: Time spent exclusively in this function, excluding calls to other functions.
    
    cumtime: Time spent in this function, including calls to sub-functions.
    
    percall: Time per function call (tottime / ncalls or cumtime / ncalls).

Let us see it with an example to compare for and while loop:


```python
import cProfile


iterations = 10000000

# Function with a for loop
def run_for_loop():
    for i in range(iterations):
        pass  

# Function with a while loop
def run_while_loop():
    i = 0
    while i < iterations:
        i += 1 


print("Profiling the for loop:")
cProfile.run('run_for_loop()')


print("\nProfiling the while loop:")
cProfile.run('run_while_loop()')
```
#### Output-
![Program Output](cpro.png)

## **Big O Notation for Python Loops**

The Big O notation helps analyze how loops perform as input size increases. The time complexity of loops is determined by how many iterations they run and how this changes as the size of the input (n) grows.

- **for loop-**

  A for loop runs a specific number of times, usually based on the size of a list or range of numbers.

```python
list = ["Mohit","Rohit","Sobhit","Ram","Shyam","Priyank","Charan"]
for item in list:
    print(item)
```
* What happens?   The loop goes over each element in the list arr and prints it.
* How many times?   If the list has 7 elements, the loop runs 7 times.
* Big O notation:   O(7), because the loop runs once for each element in the list, and the number of operations grows with the size of the list.

- **While Loops-**
A while loop keeps running as long as a condition is True. It can stop based on certain conditions inside the loop.
```python
n = 0
while n < 10:
    print(n)
    n+=1
```
* What happens?   The loop prints the number n and add 1 from it each time until n reaches smaller than 0.
* How many times?   If n starts at 0, the loop runs 10 times.
* Big O notation:   O(10), because it depends on the starting value of 0, and the loop runs 10 times.

- **While Loop with Dividing (Logarithmic Time: O(log n))**

A while loop reduces the problem size by a certain factor each time, like dividing the value of n in half. This creates a logarithmic time complexity.

```python
n =200
while n > 1:
    n = n // 2
    print(n)
```

* What happens? The loop keeps dividing 200 by 2 until it reaches 1.
* Big O notation: O(log n), because the number of iterations depends on how many times 200 can be divided by 2. If n starts at 200, the loop runs 8 times (200 → 100 → 50 → 25 → 12.5 → 6.25 → 3.125 → 1.56 → 0.78).

## Concluding CPU Comparision-


| Aspect                   | For Loop               | While Loop              |
|--------------------------|------------------------|-------------------------|
| **Execution Time**       | 7.90 seconds              | 14.97 seconds               |
| **CPU Usage**            |38 %                     | 32%         |
| **Profiling - ncalls**   | 4 calls                | 4 calls                 |
| **Profiling - tottime**  | 0.32 seconds              | 0.70 seconds               |
| **Profiling - cumtime**   | 0.319 seconds              | 0.704 seconds               |
| **Profiling - percall**   | 0.319 seconds              | 0.704 seconds               |


- **Speed:**
The for loop is much faster (7.90 seconds) than the while loop (14.97 seconds).

- **CPU Usage:**
The for loop uses more CPU (38%) compared to the while loop (32%), but it completes the task quicker.

- **Efficiency:**
The for loop has lower total execution time (0.32 seconds) and time per call (0.319 seconds) compared to the while loop (0.70 seconds total, 0.704 seconds per call).

**For loops** are generally preferred for their efficiency and readability.**While loops** may require more resources in certain cases.


## **Best use cases**
#### **When we use while loops?**

* **Unknown Number of Iterations:** Use when you don't know in advance how many times the loop will run. It continues until a condition is met.

**Example:** Keep asking for user input until the correct password is entered.
```python
correct_password = "helloworld"

while True:
    
    password = input("Enter the password: ")
    
   
    if password == correct_password:
        print("Welcome")
        break
    else:
        print("Invalid password, try again")
```
#### Output-
![Program Output](password.png)

* **Condition-Based Repetition:** Use when you want to run the loop based on a condition that could change during the loop’s execution.

**Example**: Monitor a temperature sensor and stop the loop once a critical temperature is reached.
```python
import random
import time


temperature = random.randint(60, 80) 
critical_temperature = 85


while temperature < critical_temperature:
    print(f"Current temperature: {temperature}°F")
    
    time.sleep(2)  
    
    temperature = random.randint(60, 90)
print("Warning: Critical temperature reached!")
```
#### Output-
![Program Output](temp.png)


### **When to Use for Loop:**

* **Fixed Number of Iterations:** Use when you know exactly how many times you need to loop, such as iterating over a fixed range of numbers or items in a list.

**Example:** Printing numbers from 1 to 10.
```python
for i in range(1, 11):
    print(i)
```
#### Output-
![Program Output](printfor.png)

* **Iterating Over Collections:** Use when you want to iterate over elements in a list, tuple, set, or dictionary.

**Example:** Printing each item in a list of fruits.
```python
fruits = ['apple', 'banana', 'strawberry', 'watermelon', 'mango', 'cherry']
for fruit in fruits:
    print(fruit)
```
#### Output-
![Program Output](fruits.png)

### **Summary:**

**Use a while loop when the number of iterations is uncertain, and the loop depends on a condition that can change during execution.**

**Use a for loop when you know the number of iterations in advance or are working with collections (like lists or ranges).**

## Conclusion-

This analysis of for loops and while loops in Python reveals that:

* Performance: For loops are generally faster, executing in about 7.90 seconds, while while loops take around 14.97 seconds. This makes for loops more efficient for tasks with a known number of iterations.

* CPU Usage: For loops also use CPU resources more effectively, consuming approximately 38%, compared to the while loop's 32%.

* Best Use Cases: Use for loops when the number of iterations is fixed, such as iterating through a list. Choose while loops for scenarios where the number of iterations can change, like waiting for user input.

In summary, for loops are preferred for their speed and efficiency, while while loops offer flexibility. Choosing the right loop type can significantly improve the performance of your Python code.


## References-

1. **Python Official Documentation on Loops**:
   - [Python for Loops](https://docs.python.org/3/tutorial/controlflow.html#defining-functions)
   - [Python while Loops](https://docs.python.org/3/tutorial/controlflow.html#while-statements)

2. **Understanding Performance with cProfile**:
   - [cProfile Documentation](https://docs.python.org/3/library/profile.html#module-cProfile)

3. **Measuring CPU Usage with psutil**:
   - [psutil Documentation](https://psutil.readthedocs.io/en/latest/)

4. **Performance Comparison Articles**:
   - [Python Loop Performance Comparison](https://realpython.com/python-for-loop/)
   - [Understanding Time Complexity in Python](https://www.geeksforgeeks.org/analysis-of-algorithms-set-1-asymptotic-analysis/)

