
> [!abstract] What you need to know  
> By the end of these notes, you should understand:
> 
> - What a stack is and why it follows LIFO
>     
> - Stack operations: Push, Pop, Peek
>     
> - Overflow and Underflow
>     
> - Implementation using arrays and linked lists
>     
> - C/C++ implementation without STL
>     
> - C++ STL stack
>     
> - Time complexity
>     
> - Common applications
>     
> - How to recognize and solve stack problems
>     

---

# 1. What is a Stack?

A **Stack** is a **linear data structure** that follows the principle:

> **LIFO — Last In, First Out**

This means:

> The element that is inserted last is removed first.

## Real-Life Example: Stack of Plates

Imagine plates arranged like this:

```text
        ┌─────┐
TOP →   │ 30  │  ← Last plate placed
        ├─────┤
        │ 20  │
        ├─────┤
        │ 10  │  ← First plate placed
        └─────┘
```

If you want to remove a plate, you remove `30` first.

You cannot directly remove `10` from the bottom without first removing the plates above it.

Therefore:

```text
Insert order:  10 → 20 → 30
Remove order:  30 → 20 → 10
```

This is **Last In, First Out**.

---

# 2. The Most Important Concept: TOP

A stack has one special position called **TOP**.

`TOP` represents the location of the element that was most recently inserted.

Example:

```text
Index:       0     1     2     3
           ┌─────┬─────┬─────┬─────┐
Stack:     │ 10  │ 20  │ 30  │     │
           └─────┴─────┴─────┴─────┘
                           ↑
                          TOP
```

Here:

```cpp
top = 2;
```

because the top element (`30`) is stored at index `2`.

> [!important]  
> In a stack, insertion and deletion both happen at the **TOP**.

---

# 3. Basic Stack Operations

A stack mainly has the following operations:

## 3.1 Push

**Push means inserting an element onto the top of the stack.**

Example:

```text
Before Push(40):

TOP → 30
       20
       10
```

After:

```text
TOP → 40
       30
       20
       10
```

---

## 3.2 Pop

**Pop means removing the top element from the stack.**

Example:

```text
Before Pop:

TOP → 40
       30
       20
       10
```

After Pop:

```text
TOP → 30
       20
       10
```

The value `40` is removed because it was the most recently inserted element.

---

## 3.3 Peek / Top

**Peek means looking at the top element without removing it.**

Example:

```text
TOP → 30
       20
       10
```

```text
peek() = 30
```

After `peek()`, the stack remains unchanged.

---

## 3.4 isEmpty

Checks whether the stack contains any elements.

---

## 3.5 isFull

Checks whether the stack is full.

This is mainly required when implementing a stack using a **fixed-size array**.

---

# 4. Stack Implementation Using an Array

The simplest way to implement a stack manually is using:

1. An array to store the elements.
    
2. A variable called `top` to track the top position.
    

Example:

```cpp
#define MAX 5

int stack[MAX];
int top = -1;
```

## Why is `top = -1` initially?

Initially, there are no elements in the stack.

```text
Index:      0    1    2    3    4
          ┌────┬────┬────┬────┬────┐
          │    │    │    │    │    │
          └────┴────┴────┴────┴────┘

top = -1
```

Since index `0` will contain the first element, `-1` represents an empty stack.

> [!tip]  
> Remember:
> 
> - `top = -1` → Stack is empty.
>     
> - `top = 0` → One element exists at index 0.
>     

---

# 5. PUSH Operation in Detail

Suppose:

```cpp
top = -1;
```

We want to insert:

```text
10
```

## Step 1: Increase TOP

```cpp
top++;
```

Now:

```cpp
top = 0;
```

## Step 2: Store the value

```cpp
stack[top] = 10;
```

The stack now becomes:

```text
Index:      0
          ┌────┐
TOP →     │ 10 │
          └────┘

top = 0
```

## Push Another Value

Suppose we push `20`.

```cpp
top++;
stack[top] = 20;
```

Now:

```text
          ┌────┐
TOP →     │ 20 │
          ├────┤
          │ 10 │
          └────┘
```

---

## General PUSH Algorithm

```text
PUSH(value)

IF stack is full
    Stack Overflow
ELSE
    Increase TOP
    Store value at stack[TOP]
END IF
```

In C++:

```cpp
void push(int value)
{
    if (top == MAX - 1)
    {
        cout << "Stack Overflow";
    }
    else
    {
        top++;
        stack[top] = value;
    }
}
```

---

# 6. Stack Overflow

Suppose the stack has a size of 5.

```cpp
#define MAX 5
```

Valid indexes are:

```text
0, 1, 2, 3, 4
```

If:

```cpp
top == MAX - 1
```

then:

```cpp
top == 4
```

The stack is full.

Trying to insert another element causes:

> [!danger] Stack Overflow  
> **Stack Overflow occurs when we try to insert (push) an element into a full stack.**

---

# 7. POP Operation in Detail

Suppose the stack is:

```text
          ┌────┐
TOP →     │ 30 │
          ├────┤
          │ 20 │
          ├────┤
          │ 10 │
          └────┘
```

Here:

```cpp
top = 2;
```

To pop an element:

## Step 1: Access the top value

```cpp
int value = stack[top];
```

Therefore:

```cpp
value = 30;
```

## Step 2: Decrease TOP

```cpp
top--;
```

Now:

```cpp
top = 1;
```

The logical stack becomes:

```text
TOP → 20
       10
```

> [!important]  
> In an array implementation, we usually don't need to physically erase the value. Decreasing `top` makes the old element no longer part of the stack.

---

## General POP Algorithm

```text
POP()

IF stack is empty
    Stack Underflow
ELSE
    Get value at TOP
    Decrease TOP
END IF
```

C++:

```cpp
void pop()
{
    if (top == -1)
    {
        cout << "Stack Underflow";
    }
    else
    {
        cout << stack[top];
        top--;
    }
}
```

---

# 8. Stack Underflow

If:

```cpp
top == -1;
```

the stack is empty.

Trying to execute:

```cpp
pop();
```

will cause:

> [!danger] Stack Underflow  
> **Stack Underflow occurs when we try to remove (pop) an element from an empty stack.**

---

# 9. Complete Stack Implementation Without STL

This is an important program to understand and practice.

```cpp
#include <iostream>
using namespace std;

#define MAX 5

int stackArray[MAX];
int top = -1;

void push(int value)
{
    if (top == MAX - 1)
    {
        cout << "Stack Overflow" << endl;
    }
    else
    {
        top++;
        stackArray[top] = value;
        cout << value << " pushed into stack" << endl;
    }
}

void pop()
{
    if (top == -1)
    {
        cout << "Stack Underflow" << endl;
    }
    else
    {
        cout << stackArray[top] << " popped from stack" << endl;
        top--;
    }
}

void peek()
{
    if (top == -1)
    {
        cout << "Stack is empty" << endl;
    }
    else
    {
        cout << "Top element: " << stackArray[top] << endl;
    }
}

void display()
{
    if (top == -1)
    {
        cout << "Stack is empty" << endl;
    }
    else
    {
        cout << "Stack elements:" << endl;

        for (int i = top; i >= 0; i--)
        {
            cout << stackArray[i] << endl;
        }
    }
}

int main()
{
    push(10);
    push(20);
    push(30);

    display();

    pop();

    peek();

    return 0;
}
```

---

# 10. Trace the Program

This is extremely important for tests.

Initially:

```text
top = -1
```

## After `push(10)`

```text
top++ → 0

stack[0] = 10
```

```text
TOP → 10
```

## After `push(20)`

```text
top++ → 1

stack[1] = 20
```

```text
TOP → 20
       10
```

## After `push(30)`

```text
TOP → 30
       20
       10
```

## After `pop()`

`30` is removed.

```text
TOP → 20
       10
```

The important change is:

```cpp
top = 1;
```

> [!tip]  
> For almost every basic stack question, if you can correctly track the value of `top`, you can solve the question.

---

# 11. Time Complexity

|Operation|Time Complexity|Reason|
|---|---|---|
|Push|O(1)|Only insert at TOP|
|Pop|O(1)|Only remove from TOP|
|Peek|O(1)|Directly access TOP|
|isEmpty|O(1)|Compare `top` with `-1`|
|isFull|O(1)|Compare `top` with `MAX - 1`|
|Display|O(n)|Must visit all elements|

> [!important]  
> The biggest advantage of a stack is that its main operations—**Push and Pop—take O(1) time**.

---

# 12. Stack Using a Linked List

Arrays have a limitation: their size is fixed.

A linked-list stack stores elements dynamically.

Example:

```text
TOP
 ↓
[30 | next] → [20 | next] → [10 | NULL]
```

The `top` pointer points to the first node.

## Push in Linked List

Create a new node:

```text
newNode = 40
```

Connect it to the existing stack:

```cpp
newNode->next = top;
top = newNode;
```

Result:

```text
TOP → 40 → 30 → 20 → 10 → NULL
```

## Pop in Linked List

Remove the node pointed to by `top`.

```text
TOP → 40 → 30 → 20

Remove 40

TOP → 30 → 20
```

> [!note]  
> A linked-list stack usually does not have a fixed capacity. It can continue growing until the system runs out of memory.

---

# 13. Array vs Linked List Stack

|Feature|Array Stack|Linked List Stack|
|---|---|---|
|Size|Fixed|Dynamic|
|Overflow|When array is full|When memory is unavailable|
|Memory|May waste unused space|Uses extra memory for pointers|
|Implementation|Easier|Slightly more difficult|
|Push/Pop|O(1)|O(1)|

For beginners and exams, **array implementation is usually the easiest to learn first**.

---

# 14. Stack Using C++ STL

C++ provides a ready-made stack container.

```cpp
#include <stack>
```

Create a stack:

```cpp
stack<int> s;
```

## Push

```cpp
s.push(10);
```

## Pop

```cpp
s.pop();
```

## Access the top element

```cpp
cout << s.top();
```

## Check if empty

```cpp
s.empty();
```

## Get size

```cpp
s.size();
```

Example:

```cpp
#include <iostream>
#include <stack>
using namespace std;

int main()
{
    stack<int> s;

    s.push(10);
    s.push(20);
    s.push(30);

    cout << s.top() << endl;

    s.pop();

    cout << s.top() << endl;

    return 0;
}
```

Output:

```text
30
20
```

> [!warning]  
> `s.pop()` does not return the removed value.

Correct way:

```cpp
int value = s.top();
s.pop();
```

---

# 15. Manual Implementation vs STL

## Manual Implementation

```cpp
int stack[100];
int top = -1;
```

You must manually handle:

- Overflow
    
- Underflow
    
- Increasing `top`
    
- Decreasing `top`
    

This teaches you **how stacks work internally**.

## STL

```cpp
stack<int> s;
```

The library handles the implementation for you.

> [!important]  
> For a Data Structures exam, learn manual implementation first.  
> For competitive programming and larger programs, STL is often more convenient.

### Best Learning Order

```text
1. Understand LIFO
        ↓
2. Implement using an array
        ↓
3. Implement using a linked list
        ↓
4. Learn C++ STL
        ↓
5. Solve applications and problems
```

---

# 16. How to Recognize a Stack Problem

Ask yourself:

> **Does the last thing added need to be processed first?**

If the answer is yes, think about a stack.

## Common Clues

- Reverse something
    
- Undo/Redo
    
- Balanced parentheses
    
- Nested structures
    
- Function calls
    
- Recursion
    
- Backtracking
    
- Expression evaluation
    
- Most recently visited/added item
    

---

# 17. Application: Reversing a String

Suppose:

```text
HELLO
```

Push every character:

```text
Push H
Push E
Push L
Push L
Push O
```

Stack:

```text
TOP → O
       L
       L
       E
       H
```

Now pop everything:

```text
O L L E H
```

Therefore:

```text
HELLO → OLLEH
```

> [!tip]  
> A stack naturally reverses data because of LIFO.

---

# 18. Application: Palindrome Checking

A palindrome reads the same forwards and backwards.

Examples:

```text
MADAM
LEVEL
RADAR
```

Algorithm:

1. Push every character into a stack.
    
2. Pop each character.
    
3. Compare it with the original string.
    

Example:

```text
Original: M A D A M
Popped:   M A D A M
```

If every character matches, the word is a palindrome.

---

# 19. Balanced Parentheses

This is one of the most important stack applications.

Example:

```text
{ [ ( ) ] }
```

## Algorithm

### When you see an opening bracket:

```text
(   {   [
```

Push it onto the stack.

### When you see a closing bracket:

```text
)   }   ]
```

Check whether the top of the stack contains the corresponding opening bracket.

Then pop it.

Example:

|Character|Action|Stack|
|---|---|---|
|`{`|Push|`{`|
|`[`|Push|`{ [`|
|`(`|Push|`{ [ (`|
|`)`|Match and Pop|`{ [`|
|`]`|Match and Pop|`{`|
|`}`|Match and Pop|Empty|

The expression is balanced because the stack is empty at the end.

## Three Rules to Remember

```text
Opening bracket → PUSH
Closing bracket → MATCH + POP
End → Stack must be EMPTY
```

---

# 20. Function Calls and the Call Stack

Stacks are also used internally by programs.

Suppose:

```cpp
main()
{
    functionA();
}
```

Then:

```cpp
functionA()
{
    functionB();
}
```

The calls are conceptually arranged like:

```text
TOP → functionB
       functionA
       main
```

`functionB` finishes first.

Then `functionA`.

Then `main`.

This is LIFO.

---

# 21. Recursion and Stack

Example:

```cpp
void countDown(int n)
{
    if (n == 0)
        return;

    countDown(n - 1);
}
```

Calling:

```cpp
countDown(3);
```

creates:

```text
countDown(3)
countDown(2)
countDown(1)
countDown(0)
```

These function calls are stored using the **call stack**.

After reaching the base case, the calls return in reverse order.

If too many recursive calls occur, the system can run out of stack memory, causing a **stack overflow**.

---

# 22. Infix, Prefix and Postfix Expressions

## Infix

Operator is between operands:

```text
A + B
```

## Prefix

Operator comes before operands:

```text
+ A B
```

## Postfix

Operator comes after operands:

```text
A B +
```

Example:

```text
Infix:   A + B * C
Prefix:  + A * B C
Postfix: A B C * +
```

Stacks are used to convert and evaluate these expressions.

---

# 23. Postfix Expression Evaluation

Consider:

```text
2 3 + 4 *
```

This means:

```text
(2 + 3) × 4
```

## Process

### Read `2`

Push:

```text
[2]
```

### Read `3`

Push:

```text
[2, 3]
```

### Read `+`

Pop two elements:

```text
3 and 2
```

Calculate:

```text
2 + 3 = 5
```

Push result:

```text
[5]
```

### Read `4`

Push:

```text
[5, 4]
```

### Read `*`

Pop and calculate:

```text
5 × 4 = 20
```

Final result:

```text
20
```

> [!warning]  
> For subtraction and division, operand order is important.

For:

```text
10 2 -
```

Do:

```cpp
b = stack.top();
stack.pop();

a = stack.top();
stack.pop();

result = a - b;
```

Result:

```text
10 - 2 = 8
```

Not `2 - 10`.

---

# 24. Major Applications of Stack

Memorize these for theory questions:

1. **Function calls**
    
2. **Recursion**
    
3. **Undo/Redo operations**
    
4. **Browser history**
    
5. **Balanced parentheses**
    
6. **Expression conversion**
    
7. **Expression evaluation**
    
8. **Reversing strings**
    
9. **Palindrome checking**
    
10. **Backtracking**
    

---

# 25. Stack vs Queue

|Stack|Queue|
|---|---|
|LIFO|FIFO|
|Last In, First Out|First In, First Out|
|One main accessible end|Two ends are normally used|
|Push and Pop at TOP|Insert at Rear, Delete from Front|

Example:

```text
STACK:
Last entered → First removed

QUEUE:
First entered → First removed
```

---

# 26. How to Solve a Stack Question

Whenever you see a question, follow these steps.

## Step 1: Identify LIFO

Ask:

> Does the last item need to be handled first?

If yes, use a stack.

## Step 2: Identify what is being stored

For example:

- Characters → `stack<char>`
    
- Numbers → `stack<int>`
    
- Operators → `stack<char>`
    

## Step 3: Identify the operation

Are you:

- Pushing?
    
- Popping?
    
- Comparing?
    
- Matching?
    
- Calculating?
    

## Step 4: Think about edge cases

- Is the stack empty?
    
- Is the stack full?
    
- Are brackets unmatched?
    
- Is an expression invalid?
    

## Step 5: Trace it manually

Draw the stack.

```text
TOP → ?
       ?
       ?
```

Track every push and pop.

---

# 27. Common Mistakes

> [!warning]  
> **Mistake 1:** Forgetting to check overflow before pushing.

> [!warning]  
> **Mistake 2:** Forgetting to check underflow before popping.

> [!warning]  
> **Mistake 3:** Confusing `top` with the number of elements.

> [!warning]  
> **Mistake 4:** Thinking `pop()` returns the removed value in C++ STL.

> [!warning]  
> **Mistake 5:** Reversing operands during postfix evaluation.

---

# 28. Viva Questions and Quick Answers

## What is a stack?

A stack is a linear data structure that follows the **LIFO (Last In, First Out)** principle.

## What are the basic operations?

Push, Pop, Peek/Top, isEmpty and isFull.

## What is Stack Overflow?

It occurs when we try to push an element into a full stack.

## What is Stack Underflow?

It occurs when we try to pop an element from an empty stack.

## Why is a stack called LIFO?

Because the last element inserted is the first element removed.

## What is the time complexity of Push and Pop?

Both are **O(1)**.

## Where are stacks used?

Recursion, function calls, undo/redo, expression evaluation, parentheses matching and reversing data.

---

# 29. Final Cheat Sheet 🧠

```text
STACK
↓
Linear Data Structure
↓
Follows LIFO
↓
Last In → First Out
```

## Array Implementation

```cpp
int stack[MAX];
int top = -1;
```

## Empty Condition

```cpp
top == -1
```

## Full Condition

```cpp
top == MAX - 1
```

## Push

```cpp
top++;
stack[top] = value;
```

## Pop

```cpp
value = stack[top];
top--;
```

## Peek

```cpp
stack[top]
```

## Main Complexities

```text
Push  → O(1)
Pop   → O(1)
Peek  → O(1)
Display → O(n)
```

---

> [!success] The One-Sentence Concept  
> **A stack stores elements so that the most recently inserted element is always the first one to be removed.**

# Revision Priority

Before your test, make sure you can do these **without looking at notes**:

-  Explain LIFO with an example
    
-  Draw a stack and track `top`
    
-  Write Push from scratch
    
-  Write Pop from scratch
    
-  Explain Overflow and Underflow
    
-  Implement a stack using an array
    
-  Explain array vs linked-list stack
    
-  Check balanced parentheses using a stack
    
-  Reverse a string using a stack
    
-  Evaluate a postfix expression
    
-  Explain at least 5 real applications of stacks
    

> [!tip] Best way to study  
> Don't just read the code. Take a piece of paper, draw the stack, and manually perform every Push and Pop. Once you can predict exactly where `TOP` goes after every operation, you have understood the foundation of stacks.