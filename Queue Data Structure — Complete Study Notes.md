
> [!abstract] What you will learn  
> By the end of these notes, you should understand:
> 
> - What a Queue is and the FIFO principle
>     
> - Front and Rear
>     
> - Enqueue and Dequeue
>     
> - Linear Queue
>     
> - Problems with a Linear Queue
>     
> - Circular Queue and how wrapping works
>     
> - Priority Queue
>     
> - Deque (Double-Ended Queue)
>     
> - Input-restricted and Output-restricted Deques
>     
> - Array and Linked List implementations
>     
> - C/C++ implementation without STL
>     
> - Time complexity
>     
> - How to recognize queue problems in exams
>     

---

# 1. What is a Queue?

A **Queue** is a linear data structure that follows:

> **FIFO — First In, First Out**

This means:

> The element inserted first is removed first.

## Real-Life Example: A Line of People

Imagine people standing in a line:

```text
FRONT                                  REAR
  ↓                                      ↓
[Alice] ← [Bob] ← [Charlie] ← [David]
  ↑                                      ↑
Leaves first                         Joins here
```

Alice came first, so Alice will leave first.

If a new person arrives, they join at the **REAR**.

Therefore:

```text
First person enters → First person leaves
```

This is the fundamental concept of a queue.

---

# 2. The Most Important Queue Concept

Unlike a stack, a queue normally uses **two ends**.

```text
FRONT                              REAR
  ↓                                  ↓
[ 10 ] [ 20 ] [ 30 ] [ 40 ]
  ↑                                  ↑
DELETE HERE                     INSERT HERE
```

There are two important pointers/indexes:

## FRONT

The `front` points to the element that will be removed next.

## REAR

The `rear` points to the position where a new element is inserted.

> [!important]  
> Queue operations happen at different ends:
> 
> - **Insertion → REAR**
>     
> - **Deletion → FRONT**
>     

---

# 3. Basic Queue Operations

## 3.1 Enqueue

**Enqueue means inserting an element into the queue.**

Example:

Initially:

```text
Empty Queue
```

After:

```text
enqueue(10)
```

```text
FRONT
  ↓
[10]
  ↑
 REAR
```

Then:

```text
enqueue(20)
```

```text
FRONT          REAR
  ↓              ↓
[10] ← [20]
```

Then:

```text
enqueue(30)
```

```text
FRONT                 REAR
  ↓                     ↓
[10] ← [20] ← [30]
```

The elements enter from the rear.

---

## 3.2 Dequeue

**Dequeue means removing an element from the front of the queue.**

Before:

```text
FRONT                 REAR
  ↓                     ↓
[10] ← [20] ← [30]
```

After `dequeue()`:

```text
FRONT          REAR
  ↓              ↓
[20] ← [30]
```

The value `10` is removed because it was the first element inserted.

---

## 3.3 Peek / Front

This operation looks at the front element without removing it.

Example:

```text
FRONT
  ↓
[10] [20] [30]
```

```text
peek() = 10
```

The queue remains unchanged.

---

# 4. Queue vs Stack

|Stack|Queue|
|---|---|
|LIFO|FIFO|
|Last In, First Out|First In, First Out|
|Insert at Top|Insert at Rear|
|Delete from Top|Delete from Front|
|One main accessible end|Two ends are used|

### Remember

```text
STACK:   Last enters → First leaves
QUEUE:   First enters → First leaves
```

---

# 5. Linear Queue

A normal queue implemented using an array is called a **Linear Queue**.

Suppose:

```cpp
#define MAX 5

int queue[MAX];
int front = -1;
int rear = -1;
```

Initially:

```text
Index:     0    1    2    3    4
         ┌────┬────┬────┬────┬────┐
         │    │    │    │    │    │
         └────┴────┴────┴────┴────┘

front = -1
rear = -1
```

Both are `-1` because the queue is empty.

---

# 6. Enqueue in a Linear Queue

Suppose we want to insert `10`.

Initially:

```cpp
front = -1;
rear = -1;
```

Because this is the first element, both `front` and `rear` must point to it.

```cpp
front = 0;
rear = 0;
queue[rear] = 10;
```

Now:

```text
FRONT / REAR
     ↓
    [10]
```

---

## Adding Another Element

Suppose:

```text
enqueue(20)
```

Increase the rear:

```cpp
rear++;
queue[rear] = 20;
```

Result:

```text
FRONT        REAR
  ↓            ↓
[10] [20]
```

---

## General Enqueue Algorithm

```text
ENQUEUE(value)

IF queue is full
    Queue Overflow

ELSE IF queue is empty
    front = 0
    rear = 0
    queue[rear] = value

ELSE
    rear = rear + 1
    queue[rear] = value
END IF
```

---

# 7. Dequeue in a Linear Queue

Suppose:

```text
FRONT             REAR
  ↓                 ↓
[10] [20] [30]
```

The first element (`10`) must leave first.

We access:

```cpp
queue[front]
```

Then move the front:

```cpp
front++;
```

Now:

```text
FRONT        REAR
  ↓            ↓
[20] [30]
```

---

## General Dequeue Algorithm

```text
DEQUEUE()

IF queue is empty
    Queue Underflow

ELSE
    Get queue[front]
    front = front + 1
END IF
```

---

# 8. Queue Overflow and Underflow

## Queue Overflow

Queue overflow occurs when we try to insert an element into a full queue.

For a linear array queue:

```cpp
rear == MAX - 1
```

> [!danger] Queue Overflow  
> Trying to insert into a full queue causes overflow.

---

## Queue Underflow

Queue underflow occurs when we try to delete from an empty queue.

For a simple implementation:

```cpp
front == -1
```

or depending on implementation:

```cpp
front > rear
```

> [!danger] Queue Underflow  
> Trying to delete from an empty queue causes underflow.

---

# 9. Complete Linear Queue Implementation in C++

```cpp
#include <iostream>
using namespace std;

#define MAX 5

int queueArray[MAX];
int front = -1;
int rear = -1;

void enqueue(int value)
{
    if (rear == MAX - 1)
    {
        cout << "Queue Overflow" << endl;
    }
    else
    {
        if (front == -1)
        {
            front = 0;
        }

        rear++;
        queueArray[rear] = value;
    }
}

void dequeue()
{
    if (front == -1 || front > rear)
    {
        cout << "Queue Underflow" << endl;
    }
    else
    {
        cout << queueArray[front] << " removed" << endl;
        front++;
    }
}

void display()
{
    if (front == -1 || front > rear)
    {
        cout << "Queue is empty" << endl;
    }
    else
    {
        for (int i = front; i <= rear; i++)
        {
            cout << queueArray[i] << " ";
        }

        cout << endl;
    }
}

int main()
{
    enqueue(10);
    enqueue(20);
    enqueue(30);

    display();

    dequeue();

    display();

    return 0;
}
```

---

# 10. The Biggest Problem with a Linear Queue

This is one of the main reasons we need a **Circular Queue**.

Suppose `MAX = 5`.

The queue becomes full:

```text
Index:     0    1    2    3    4
         ┌────┬────┬────┬────┬────┐
         │ 10 │ 20 │ 30 │ 40 │ 50 │
         └────┴────┴────┴────┴────┘
          ↑                        ↑
        FRONT                    REAR
```

Now dequeue two elements:

```text
Index:     0    1    2    3    4
         ┌────┬────┬────┬────┬────┐
         │    │    │ 30 │ 40 │ 50 │
         └────┴────┴────┴────┴────┘
                    ↑              ↑
                  FRONT           REAR
```

Notice that positions `0` and `1` are now empty.

But `rear` is already at the last index:

```cpp
rear == MAX - 1
```

Therefore, the queue implementation may say it is **full**, even though there are empty spaces!

This is called:

> [!warning] Wasted Space Problem  
> In a linear queue, spaces freed at the beginning cannot easily be reused when the rear reaches the end.

## Solution: Circular Queue

---

# 11. Circular Queue 🔄

A **Circular Queue** connects the last position of the array back to the first position.

Instead of thinking of the array as:

```text
0 → 1 → 2 → 3 → 4 → END
```

Think:

```text
       ┌─────────────────┐
       ↓                 │
0 → 1 → 2 → 3 → 4 ───────┘
```

When the rear reaches the last position, it can go back to index `0`.

This is called **wrapping around**.

> [!important]  
> Circular queues solve the wasted-space problem of linear queues.

---

# 12. Circular Queue Movement

Suppose `MAX = 5`.

If:

```cpp
rear = 4;
```

and the next position is required, instead of:

```cpp
rear = 5;
```

which is outside the array, we calculate:

```cpp
rear = (rear + 1) % MAX;
```

So:

```text
(4 + 1) % 5
= 5 % 5
= 0
```

Therefore:

```text
4 → 0
```

This is the key idea of a circular queue.

---

# 13. Circular Queue Empty Condition

Initially:

```cpp
front = -1;
rear = -1;
```

This represents an empty queue.

After deleting the final element, we usually reset:

```cpp
front = -1;
rear = -1;
```

Therefore:

```cpp
front == -1
```

means the queue is empty.

---

# 14. Circular Queue Full Condition

A circular queue is full when moving `rear` forward would make it equal to `front`.

The condition is:

```cpp
(rear + 1) % MAX == front
```

## Why?

Suppose:

```text
MAX = 5
front = 1
rear = 0
```

The next position after `rear = 0` is:

```text
1
```

But `1` is occupied by `front`.

Therefore the queue is full.

> [!important]  
> Memorize this condition for exams:
> 
> ```cpp
> (rear + 1) % MAX == front
> ```

---

# 15. Circular Queue Enqueue

## Step 1: Check if Full

```cpp
(rear + 1) % MAX == front
```

If true:

```text
Queue Overflow
```

## Step 2: Check if Empty

If:

```cpp
front == -1
```

then:

```cpp
front = 0;
rear = 0;
```

## Step 3: Otherwise move Rear Circularly

```cpp
rear = (rear + 1) % MAX;
```

Then:

```cpp
queue[rear] = value;
```

---

# 16. Circular Queue Dequeue

## Step 1: Check if Empty

```cpp
front == -1
```

If true:

```text
Queue Underflow
```

## Step 2: Save the element

```cpp
value = queue[front];
```

## Step 3: Check if it was the last element

If:

```cpp
front == rear
```

then after removing it:

```cpp
front = -1;
rear = -1;
```

The queue is now empty.

## Step 4: Otherwise move Front Circularly

```cpp
front = (front + 1) % MAX;
```

---

# 17. Complete Circular Queue Implementation

```cpp
#include <iostream>
using namespace std;

#define MAX 5

int queueArray[MAX];
int front = -1;
int rear = -1;

void enqueue(int value)
{
    if ((rear + 1) % MAX == front)
    {
        cout << "Queue Overflow" << endl;
    }
    else if (front == -1)
    {
        front = 0;
        rear = 0;
        queueArray[rear] = value;
    }
    else
    {
        rear = (rear + 1) % MAX;
        queueArray[rear] = value;
    }
}

void dequeue()
{
    if (front == -1)
    {
        cout << "Queue Underflow" << endl;
    }
    else
    {
        cout << queueArray[front] << " removed" << endl;

        if (front == rear)
        {
            front = -1;
            rear = -1;
        }
        else
        {
            front = (front + 1) % MAX;
        }
    }
}

void display()
{
    if (front == -1)
    {
        cout << "Queue is empty" << endl;
        return;
    }

    int i = front;

    while (true)
    {
        cout << queueArray[i] << " ";

        if (i == rear)
        {
            break;
        }

        i = (i + 1) % MAX;
    }

    cout << endl;
}

int main()
{
    enqueue(10);
    enqueue(20);
    enqueue(30);
    enqueue(40);

    dequeue();
    dequeue();

    enqueue(50);
    enqueue(60);

    display();

    return 0;
}
```

---

# 18. Circular Queue Example and Dry Run

Suppose `MAX = 5`.

Initially:

```text
front = -1
rear = -1
```

## Insert 10, 20, 30, 40, 50

```text
Index:     0    1    2    3    4
         ┌────┬────┬────┬────┬────┐
         │ 10 │ 20 │ 30 │ 40 │ 50 │
         └────┴────┴────┴────┴────┘
          ↑                        ↑
        FRONT                    REAR
```

Remove 10 and 20:

```text
front = 2
rear = 4
```

```text
Index:     0    1    2    3    4
         ┌────┬────┬────┬────┬────┐
         │    │    │ 30 │ 40 │ 50 │
         └────┴────┴────┴────┴────┘
                    ↑              ↑
                  FRONT           REAR
```

Now insert `60`.

Rear moves:

```text
rear = (4 + 1) % 5 = 0
```

So:

```text
Index:     0    1    2    3    4
         ┌────┬────┬────┬────┬────┐
         │ 60 │    │ 30 │ 40 │ 50 │
         └────┴────┴────┴────┴────┘
          ↑              ↑
        REAR           FRONT
```

The logical queue order is:

```text
30 → 40 → 50 → 60
```

Even though the array positions are not in normal left-to-right order.

This is the most important thing to understand about circular queues.

---

# 19. Visual Comparison: Linear vs Circular Queue

A useful way to understand the difference is to compare how `FRONT` and `REAR` move and how circular queues reuse empty positions:

> [!tip]  
> In a **linear queue**, `REAR` reaching the end can waste earlier empty spaces.  
> In a **circular queue**, `REAR` wraps around and reuses them.

---

# 20. Priority Queue

A **Priority Queue** is a queue where elements are removed based on their **priority**, rather than only their arrival order.

Example:

```text
Patient A → Priority 1
Patient B → Priority 5
Patient C → Priority 3
```

If a higher number means higher priority:

```text
Patient B is served first.
```

Even if Patient A arrived before Patient B.

## Important Rule

Elements with higher priority are processed first.

If two elements have the same priority, FIFO is often used between them.

Example:

```text
Priority 5: A, B
Priority 3: C
Priority 1: D
```

The processing order may be:

```text
A → B → C → D
```

---

# 21. Priority Queue vs Normal Queue

|Normal Queue|Priority Queue|
|---|---|
|Strict FIFO|Priority determines removal|
|First arrival leaves first|Higher priority may leave first|
|Simple ordering|Priority-based ordering|

## Applications

- Hospital emergency systems
    
- CPU scheduling
    
- Printer systems
    
- Network packet processing
    
- Operating systems
    

---

# 22. Deque (Double-Ended Queue)

**Deque** is pronounced:

> **"Deck"**

Deque means:

> **Double-Ended Queue**

Unlike a normal queue, insertion and deletion can happen at **both ends**.

```text
FRONT                           REAR
  ↓                               ↓
[ 10 ] [ 20 ] [ 30 ] [ 40 ]
  ↑                               ↑
Insert/Delete                 Insert/Delete
```

A deque can perform four major operations:

```text
Insert Front
Insert Rear
Delete Front
Delete Rear
```

---

# 23. Deque Operations

## Insert at Front

```text
Before:

10 ← 20 ← 30

After InsertFront(5):

5 ← 10 ← 20 ← 30
```

## Insert at Rear

```text
Before:

10 ← 20 ← 30

After InsertRear(40):

10 ← 20 ← 30 ← 40
```

## Delete Front

```text
10 ← 20 ← 30

Remove 10

20 ← 30
```

## Delete Rear

```text
10 ← 20 ← 30

Remove 30

10 ← 20
```

---

# 24. Types of Deque

There are two restricted forms.

## 24.1 Input-Restricted Deque

Insertion is allowed only at one end.

Deletion is allowed at both ends.

```text
Insertion → REAR only

Deletion → FRONT or REAR
```

---

## 24.2 Output-Restricted Deque

Insertion is allowed at both ends.

Deletion is allowed only at one end.

```text
Insertion → FRONT or REAR

Deletion → FRONT only
```

---

# 25. Summary of Queue Types

|Type|Main Feature|
|---|---|
|Linear Queue|FIFO, moves normally from front to rear|
|Circular Queue|Last position connects back to first|
|Priority Queue|Priority determines removal order|
|Deque|Insert/delete from both ends|
|Input-Restricted Deque|Insert one end, delete both ends|
|Output-Restricted Deque|Insert both ends, delete one end|

---

# 26. Queue Using Linked List

A queue can also be implemented dynamically using a linked list.

```text
FRONT                               REAR
  ↓                                   ↓
[10|next] → [20|next] → [30|NULL]
```

We usually maintain two pointers:

```cpp
front
rear
```

## Enqueue

Insert a new node at the rear.

```text
Before:

10 → 20 → 30

After enqueue(40):

10 → 20 → 30 → 40
```

## Dequeue

Remove the node from the front.

```text
Before:

10 → 20 → 30

After dequeue():

20 → 30
```

Both operations can be performed in:

```text
O(1)
```

---

# 27. Array Queue vs Linked List Queue

|Feature|Array|Linked List|
|---|---|---|
|Size|Usually fixed|Dynamic|
|Memory allocation|Fixed|Dynamic|
|Overflow|When full|When memory unavailable|
|Implementation|Easier|More complex|
|Enqueue|O(1)|O(1)|
|Dequeue|O(1)|O(1)|

---

# 28. C++ STL Queue

C++ provides a ready-made queue:

```cpp
#include <queue>
using namespace std;

queue<int> q;
```

## Enqueue

```cpp
q.push(10);
```

## Dequeue

```cpp
q.pop();
```

## Access Front

```cpp
q.front();
```

## Access Rear

```cpp
q.back();
```

## Check Empty

```cpp
q.empty();
```

Example:

```cpp
#include <iostream>
#include <queue>
using namespace std;

int main()
{
    queue<int> q;

    q.push(10);
    q.push(20);
    q.push(30);

    cout << q.front() << endl;

    q.pop();

    cout << q.front() << endl;

    return 0;
}
```

> [!warning]  
> Just like `stack.pop()`, `queue.pop()` does not return the removed value.

To get the value:

```cpp
int value = q.front();
q.pop();
```

---

# 29. Time Complexity

## Normal Queue

|Operation|Complexity|
|---|---|
|Enqueue|O(1)|
|Dequeue|O(1)|
|Peek Front|O(1)|

## Circular Queue

|Operation|Complexity|
|---|---|
|Enqueue|O(1)|
|Dequeue|O(1)|
|Display|O(n)|

## Linked List Queue

|Operation|Complexity|
|---|---|
|Enqueue|O(1)|
|Dequeue|O(1)|

---

# 30. Applications of Queues

Queues are used when things must be processed in the same order in which they arrive.

## Common Applications

1. **Printer Queue**
    
2. **Customer Service Lines**
    
3. **CPU Scheduling**
    
4. **Task Scheduling**
    
5. **Network Data Packets**
    
6. **Breadth-First Search (BFS)**
    
7. **Buffering**
    
8. **Messaging Systems**
    
9. **Ticket Systems**
    

---

# 31. How to Recognize a Queue Problem

Ask yourself:

> **Should the first item that arrives be processed first?**

If yes, a queue may be appropriate.

### Common clues

- Waiting line
    
- Scheduling
    
- First come, first served
    
- Process requests in arrival order
    
- BFS / level-by-level traversal
    
- Buffer
    
- Tasks waiting for processing
    

---

# 32. Stack vs Queue — Final Comparison

```text
STACK

Push ↓
┌─────┐
│ 30  │ ← Pop
├─────┤
│ 20  │
├─────┤
│ 10  │
└─────┘

LIFO
```

```text
QUEUE

Delete ← [10] [20] [30] ← Insert

FIFO
```

---

# 33. Viva Questions and Quick Answers

## What is a Queue?

A queue is a linear data structure that follows the **FIFO (First In, First Out)** principle.

## What are the main queue operations?

Enqueue, Dequeue, Peek/Front, and checking whether the queue is empty or full.

## Where does insertion happen?

At the **REAR**.

## Where does deletion happen?

At the **FRONT**.

## What is Queue Overflow?

Trying to insert into a full queue.

## What is Queue Underflow?

Trying to delete from an empty queue.

## Why is a Circular Queue needed?

It solves the wasted-space problem of a linear queue by reusing empty positions.

## What is the Circular Queue full condition?

```cpp
(rear + 1) % MAX == front
```

## What is a Deque?

A Double-Ended Queue where operations can occur at both ends.

## What is a Priority Queue?

A queue in which elements are processed according to priority.

---

# 34. Final Cheat Sheet 🧠

## Queue

```text
FIFO
First In → First Out
```

```text
Insertion → REAR
Deletion  → FRONT
```

## Linear Queue

```cpp
front = -1;
rear = -1;
```

## Circular Queue

### Next position

```cpp
(rear + 1) % MAX
```

### Full condition

```cpp
(rear + 1) % MAX == front
```

### Empty condition

```cpp
front == -1
```

## Deque

```text
Insert Front
Insert Rear
Delete Front
Delete Rear
```

---

# 35. Revision Checklist

Before your test, make sure you can do these without looking:

-  Explain FIFO with a real-life example
    
-  Explain FRONT and REAR
    
-  Write enqueue from scratch
    
-  Write dequeue from scratch
    
-  Explain Queue Overflow and Underflow
    
-  Implement a Linear Queue using an array
    
-  Explain the wasted-space problem
    
-  Explain why Circular Queues are needed
    
-  Memorize the circular full condition
    
-  Dry-run a Circular Queue
    
-  Explain a Priority Queue
    
-  Explain a Deque
    
-  Explain input-restricted and output-restricted deque
    
-  Compare Stack and Queue
    

> [!success] The One-Sentence Concept  
> **A Queue is a linear data structure where the first element inserted is the first element removed. This is called FIFO — First In, First Out.**