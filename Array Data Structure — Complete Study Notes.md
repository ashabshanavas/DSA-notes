
> [!abstract] What you will learn  
> By the end of these notes, you should understand:
> 
> - What an array is
>     
> - Why arrays are useful
>     
> - Indexing and memory concepts
>     
> - One-dimensional and two-dimensional arrays
>     
> - Traversal
>     
> - Insertion
>     
> - Deletion
>     
> - Searching
>     
> - Updating
>     
> - Sorting basics
>     
> - Static vs dynamic arrays
>     
> - Time complexity of array operations
>     
> - Arrays in C and C++
>     
> - Common exam questions and mistakes
>     
> - How arrays relate to other data structures
>     

---

# 1. What is an Array?

An **array** is a collection of elements of the **same data type**, stored in a sequence of memory locations.

For example:

```cpp
int numbers[5] = {10, 20, 30, 40, 50};
```

We can visualize it as:

```text
Index:       0      1      2      3      4
           ┌────┬────┬────┬────┬────┐
Array:     │ 10 │ 20 │ 30 │ 40 │ 50 │
           └────┴────┴────┴────┴────┘
```

The array has:

- **5 elements**
    
- Indexes from `0` to `4`
    

> [!important]  
> In C and C++, array indexing normally starts from **0**.

---

# 2. Why Do We Need Arrays?

Imagine you want to store marks of 5 students.

Without an array:

```cpp
int mark1 = 80;
int mark2 = 75;
int mark3 = 90;
int mark4 = 65;
int mark5 = 88;
```

This becomes difficult when there are many values.

With an array:

```cpp
int marks[5] = {80, 75, 90, 65, 88};
```

Now we can use loops to process all the values.

```cpp
for (int i = 0; i < 5; i++)
{
    cout << marks[i] << endl;
}
```

Arrays make it easy to store and process a large collection of similar data.

---

# 3. Important Property: Same Data Type

An array normally stores elements of the same type.

Examples:

```cpp
int numbers[5];
```

Stores integers.

```cpp
float prices[10];
```

Stores floating-point numbers.

```cpp
char letters[26];
```

Stores characters.

```cpp
string names[10];
```

Stores strings.

> [!note]  
> In a traditional C/C++ array, all elements have the same data type.

---

# 4. Indexing

Every element in an array has a position called an **index**.

Example:

```cpp
int arr[5] = {10, 20, 30, 40, 50};
```

```text
Index:       0      1      2      3      4
           ┌────┬────┬────┬────┬────┐
Array:     │ 10 │ 20 │ 30 │ 40 │ 50 │
           └────┴────┴────┴────┴────┘
```

Therefore:

```cpp
arr[0] = 10;
arr[1] = 20;
arr[2] = 30;
arr[3] = 40;
arr[4] = 50;
```

## Important Formula

For an array containing `n` elements:

```text
First Index = 0
Last Index = n - 1
```

For example, if:

```text
n = 10
```

indexes are:

```text
0 to 9
```

> [!warning]  
> A very common mistake is accessing an index outside the array.

For:

```cpp
int arr[5];
```

valid indexes are:

```text
0, 1, 2, 3, 4
```

Trying to access:

```cpp
arr[5]
```

is outside the valid array range.

---

# 5. Memory Concept of Arrays

One of the important characteristics of an array is that its elements are stored in **contiguous memory locations**.

Conceptually:

```text
Memory
┌─────────┬─────────┬─────────┬─────────┐
│   10    │   20    │   30    │   40    │
└─────────┴─────────┴─────────┴─────────┘
   arr[0]    arr[1]    arr[2]    arr[3]
```

The elements are placed next to each other.

This allows us to directly access any element using its index.

For example:

```cpp
arr[100]
```

can be accessed directly without checking elements `0` to `99`.

This is why array access is fast.

> [!important]  
> Accessing an array element by index takes **O(1)** time.

---

# 6. Creating an Array

## Method 1: Declare an Array

```cpp
int arr[5];
```

This creates space for 5 integers.

The values may not be initialized automatically.

---

## Method 2: Declare and Initialize

```cpp
int arr[5] = {10, 20, 30, 40, 50};
```

---

## Method 3: Let the Compiler Determine the Size

```cpp
int arr[] = {10, 20, 30, 40, 50};
```

The compiler counts the elements.

Size:

```text
5
```

---

## Partial Initialization

```cpp
int arr[5] = {10, 20};
```

Conceptually:

```text
Index:       0      1      2      3      4
           ┌────┬────┬────┬────┬────┐
Array:     │ 10 │ 20 │  0 │  0 │  0 │
           └────┴────┴────┴────┴────┘
```

---

# 7. Traversing an Array

**Traversal** means visiting every element in the array.

Example:

```cpp
int arr[5] = {10, 20, 30, 40, 50};
```

We use a loop:

```cpp
for (int i = 0; i < 5; i++)
{
    cout << arr[i] << " ";
}
```

Output:

```text
10 20 30 40 50
```

## How the Loop Works

Initially:

```text
i = 0 → arr[0] → 10
```

Then:

```text
i = 1 → arr[1] → 20
```

Then:

```text
i = 2 → arr[2] → 30
```

And so on.

### General Traversal

```cpp
for (int i = 0; i < n; i++)
{
    // Use arr[i]
}
```

> [!tip]  
> The condition is usually `i < n`, not `i <= n`.

---

# 8. Updating an Array Element

Updating means changing the value at a particular index.

Example:

```cpp
int arr[5] = {10, 20, 30, 40, 50};
```

Change `30` to `99`:

```cpp
arr[2] = 99;
```

Result:

```text
Index:       0      1      2      3      4
           ┌────┬────┬────┬────┬────┐
Array:     │ 10 │ 20 │ 99 │ 40 │ 50 │
           └────┴────┴────┴────┴────┘
```

Because arrays support direct access, updating also takes:

```text
O(1)
```

---

# 9. Inserting into an Array

This is an important Data Structures concept.

Suppose:

```text
Array:  [10] [20] [30] [40] [   ]
Index:    0    1    2    3    4
```

We want to insert `99` at index `2`.

The desired result is:

```text
[10] [20] [99] [30] [40]
```

But `30` is already at index `2`.

Therefore, we need to move elements to the right.

## Step-by-Step

Before:

```text
[10] [20] [30] [40] [   ]
```

Move `40` right:

```text
[10] [20] [30] [   ] [40]
```

Move `30` right:

```text
[10] [20] [   ] [30] [40]
```

Insert `99`:

```text
[10] [20] [99] [30] [40]
```

---

## Insertion Algorithm

```text
INSERT(value, position)

FOR i = n - 1 DOWN TO position
    arr[i + 1] = arr[i]

arr[position] = value
n = n + 1
```

## C++ Code

```cpp
void insert(int arr[], int &n, int position, int value)
{
    for (int i = n - 1; i >= position; i--)
    {
        arr[i + 1] = arr[i];
    }

    arr[position] = value;
    n++;
}
```

> [!important]  
> We move from **right to left** when inserting.

Why?

If we moved from left to right, we could overwrite values before moving them.

---

# 10. Time Complexity of Insertion

## Insert at the End

```text
[10] [20] [30] [40] [   ]
```

Insert `50`.

No shifting is required.

```text
O(1)
```

## Insert at the Beginning

```text
[10] [20] [30] [40]
```

Insert `5`.

Every element must shift.

```text
[5] [10] [20] [30] [40]
```

Time:

```text
O(n)
```

## Insert in the Middle

Some elements must shift.

Worst case:

```text
O(n)
```

---

# 11. Deleting from an Array

Suppose:

```text
Index:       0      1      2      3      4
           ┌────┬────┬────┬────┬────┐
Array:     │ 10 │ 20 │ 30 │ 40 │ 50 │
           └────┴────┴────┴────┴────┘
```

We want to delete the value at index `1`.

That is:

```text
20
```

The desired result is:

```text
[10] [30] [40] [50] [   ]
```

We need to shift elements left.

## Step-by-Step

Move `30`:

```text
[10] [30] [30] [40] [50]
```

Move `40`:

```text
[10] [30] [40] [40] [50]
```

Move `50`:

```text
[10] [30] [40] [50] [   ]
```

Then reduce the number of elements.

---

## Deletion Algorithm

```text
DELETE(position)

FOR i = position TO n - 2
    arr[i] = arr[i + 1]

n = n - 1
```

## C++ Code

```cpp
void deleteElement(int arr[], int &n, int position)
{
    for (int i = position; i < n - 1; i++)
    {
        arr[i] = arr[i + 1];
    }

    n--;
}
```

> [!important]  
> Insertion shifts elements to the **right**.  
> Deletion shifts elements to the **left**.

---

# 12. Searching in an Array

Searching means finding a particular element.

There are two important methods:

1. Linear Search
    
2. Binary Search
    

---

# 13. Linear Search

Linear search checks elements one by one.

Suppose:

```text
[10] [25] [30] [45] [60]
```

Search for:

```text
45
```

Process:

```text
10 → Not found
25 → Not found
30 → Not found
45 → Found!
```

## C++ Code

```cpp
int linearSearch(int arr[], int n, int value)
{
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == value)
        {
            return i;
        }
    }

    return -1;
}
```

## Time Complexity

Best case:

```text
O(1)
```

The element is at the beginning.

Worst case:

```text
O(n)
```

The element is at the end or does not exist.

---

# 14. Binary Search

Binary search is much faster than linear search, but it requires the array to be **sorted**.

Example:

```text
[10] [20] [30] [40] [50] [60] [70]
```

Search for `60`.

Instead of checking every element, check the middle.

Middle:

```text
40
```

Since:

```text
60 > 40
```

we ignore the left half.

Remaining:

```text
[50] [60] [70]
```

Check middle:

```text
60
```

Found!

---

## Binary Search Algorithm

```text
Set low = 0
Set high = n - 1

WHILE low <= high

    middle = (low + high) / 2

    IF arr[middle] == value
        Found

    ELSE IF value > arr[middle]
        Search right half

    ELSE
        Search left half
```

---

## Simple C++ Binary Search

```cpp
int binarySearch(int arr[], int n, int value)
{
    int low = 0;
    int high = n - 1;

    while (low <= high)
    {
        int middle = (low + high) / 2;

        if (arr[middle] == value)
        {
            return middle;
        }
        else if (arr[middle] < value)
        {
            low = middle + 1;
        }
        else
        {
            high = middle - 1;
        }
    }

    return -1;
}
```

## Time Complexity

```text
O(log n)
```

> [!warning]  
> Binary search only works correctly when the array is sorted.

---

# 15. One-Dimensional Array

A one-dimensional array is a simple list of values.

Example:

```cpp
int arr[5] = {10, 20, 30, 40, 50};
```

Visualization:

```text
[10] [20] [30] [40] [50]
```

Access:

```cpp
arr[index]
```

Example:

```cpp
arr[2]
```

gives:

```text
30
```

---

# 16. Two-Dimensional Array

A two-dimensional array looks like a table or matrix.

Example:

```cpp
int matrix[3][3];
```

Visualization:

```text
        Column
         0   1   2
       ┌───┬───┬───┐
Row 0  │ 1 │ 2 │ 3 │
       ├───┼───┼───┤
Row 1  │ 4 │ 5 │ 6 │
       ├───┼───┼───┤
Row 2  │ 7 │ 8 │ 9 │
       └───┴───┴───┘
```

We access elements using:

```cpp
matrix[row][column]
```

For example:

```cpp
matrix[1][2]
```

is:

```text
6
```

---

# 17. Initializing a 2D Array

```cpp
int matrix[3][3] =
{
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

Visualization:

```text
1 2 3
4 5 6
7 8 9
```

---

# 18. Traversing a 2D Array

We use nested loops.

```cpp
for (int i = 0; i < 3; i++)
{
    for (int j = 0; j < 3; j++)
    {
        cout << matrix[i][j] << " ";
    }

    cout << endl;
}
```

## How to Think About It

Outer loop:

```text
Changes the row
```

Inner loop:

```text
Changes the column
```

So:

```text
Row 0 → Visit all columns
Row 1 → Visit all columns
Row 2 → Visit all columns
```

---

# 19. Array Traversal vs Direct Access

Suppose:

```text
[10] [20] [30] [40] [50]
```

## Direct Access

To access:

```cpp
arr[3]
```

we directly get:

```text
40
```

Time:

```text
O(1)
```

## Traversal

To visit every element:

```text
10 → 20 → 30 → 40 → 50
```

Time:

```text
O(n)
```

This is an important difference.

---

# 20. Static Arrays vs Dynamic Arrays

## Static Array

A normal array has a fixed size.

```cpp
int arr[100];
```

It has space for 100 integers.

You cannot simply make it larger later.

---

## Dynamic Allocation in C++

Memory can be allocated dynamically.

```cpp
int n;
cin >> n;

int* arr = new int[n];
```

This creates an array based on the value of `n`.

When finished:

```cpp
delete[] arr;
```

> [!note]  
> For beginner Data Structures courses, you should understand the concept of dynamic memory, but basic array questions often use fixed-size arrays.

---

# 21. Arrays and Vectors

In modern C++, `vector` is often more flexible than a traditional array.

Example:

```cpp
#include <vector>

vector<int> numbers;
```

Vectors can grow dynamically.

However:

> [!important]  
> In a Data Structures exam, you should still understand traditional arrays because many data structures are implemented using arrays.

For example:

- Stack using an array
    
- Queue using an array
    
- Circular Queue using an array
    
- Heap using an array
    

---

# 22. Advantages of Arrays

## 1. Fast Access

Access any index directly.

```text
O(1)
```

## 2. Easy Traversal

Use loops.

## 3. Simple Implementation

Arrays are one of the easiest data structures to understand.

## 4. Memory Locality

Elements are stored close together in memory.

---

# 23. Disadvantages of Arrays

## 1. Fixed Size

Traditional arrays cannot easily change size.

## 2. Insertion is Expensive

Inserting in the middle requires shifting elements.

```text
O(n)
```

## 3. Deletion is Expensive

Deleting may require shifting elements.

```text
O(n)
```

## 4. Same Data Type

Traditional arrays normally store one type of data.

---

# 24. Array vs Linked List

|Feature|Array|Linked List|
|---|---|---|
|Memory|Contiguous|Nodes can be anywhere|
|Access by index|O(1)|O(n)|
|Insertion|O(n)|Can be O(1) at known position|
|Deletion|O(n)|Can be O(1) at known position|
|Size|Usually fixed|Dynamic|

The main tradeoff is:

```text
Array → Fast Access
Linked List → Easier Dynamic Insertion/Deletion
```

---

# 25. Time Complexity Cheat Sheet

|Operation|Best / Average / Worst|
|---|---|
|Access by index|O(1)|
|Update by index|O(1)|
|Traverse|O(n)|
|Linear Search|O(n)|
|Binary Search|O(log n)|
|Insert at end|O(1)*|
|Insert at beginning|O(n)|
|Insert in middle|O(n)|
|Delete at beginning|O(n)|
|Delete in middle|O(n)|
|Delete at end|O(1)|

> [!note]  
> Insertion at the end is O(1) when there is already unused space available.

---

# 26. Common Array Problems

Arrays are commonly used for:

1. Finding the maximum value
    
2. Finding the minimum value
    
3. Calculating sum
    
4. Calculating average
    
5. Searching for an element
    
6. Reversing an array
    
7. Sorting an array
    
8. Inserting an element
    
9. Deleting an element
    
10. Finding duplicate elements
    

---

# 27. Finding the Maximum Element

Example:

```text
[10] [45] [20] [90] [30]
```

We start by assuming the first element is the maximum.

```cpp
int maximum = arr[0];
```

Then compare every other element.

```cpp
for (int i = 1; i < n; i++)
{
    if (arr[i] > maximum)
    {
        maximum = arr[i];
    }
}
```

Final result:

```text
90
```

---

# 28. Finding the Sum of an Array

```cpp
int sum = 0;

for (int i = 0; i < n; i++)
{
    sum = sum + arr[i];
}
```

For:

```text
[10, 20, 30]
```

Result:

```text
10 + 20 + 30 = 60
```

---

# 29. Reversing an Array

Suppose:

```text
[10] [20] [30] [40] [50]
```

Reverse:

```text
[50] [40] [30] [20] [10]
```

We use two indexes:

```text
left  = 0
right = n - 1
```

Swap them and move inward.

```cpp
while (left < right)
{
    int temp = arr[left];
    arr[left] = arr[right];
    arr[right] = temp;

    left++;
    right--;
}
```

---

# 30. How to Solve Array Questions

When you see an array question, ask these questions:

## Step 1: What does the index represent?

Understand:

```text
0 → First element
n - 1 → Last element
```

## Step 2: Are you traversing or directly accessing?

If you need every element:

```cpp
for (...)
```

If you know the position:

```cpp
arr[index]
```

## Step 3: Are elements being shifted?

If yes, think about insertion or deletion.

### Insertion

```text
Shift Right
```

### Deletion

```text
Shift Left
```

## Step 4: Is the array sorted?

If yes, binary search may be possible.

---

# 31. Common Beginner Mistakes

> [!warning] Mistake 1: Using `i <= n`  
> If the array contains `n` elements, the last valid index is `n - 1`.
> 
> Correct:
> 
> ```cpp
> i < n
> ```

> [!warning] Mistake 2: Confusing Array Size and Last Index
> 
> ```text
> Size = 5
> Last Index = 4
> ```

> [!warning] Mistake 3: Inserting without checking available space
> 
> You cannot insert into a fixed-size full array without additional capacity.

> [!warning] Mistake 4: Shifting in the wrong direction
> 
> Insert → Shift Right  
> Delete → Shift Left

> [!warning] Mistake 5: Using Binary Search on an Unsorted Array
> 
> Binary Search requires sorted data.

---

# 32. Arrays and Other Data Structures

Arrays are the foundation of many data structures.

## Stack

```text
Array + TOP
```

## Queue

```text
Array + FRONT + REAR
```

## Circular Queue

```text
Array + FRONT + REAR + Wrap Around
```

## Heap

```text
Array arranged using parent/child index rules
```

> [!important]  
> If you understand arrays well, learning many other data structures becomes much easier.

---

# 33. Viva Questions and Quick Answers

## What is an array?

An array is a collection of elements of the same data type stored in contiguous memory locations.

## Why does array indexing usually start from 0?

The first element is stored at the base address, and the index represents an offset from that base location.

## What is the time complexity of accessing an array element?

```text
O(1)
```

## What is array traversal?

Visiting every element of an array.

## Why is insertion in the middle O(n)?

Because elements may need to be shifted.

## Why is deletion in the middle O(n)?

Because remaining elements may need to be shifted.

## What is Linear Search?

Checking elements one by one.

## What is Binary Search?

Repeatedly dividing a sorted search space into halves.

## Can Binary Search work on an unsorted array?

No.

## What is a 2D array?

An array arranged in rows and columns.

---

# 34. Final Cheat Sheet 🧠

```text
ARRAY
↓
Collection of Same-Type Elements
↓
Stored in Contiguous Memory
↓
Access Using Index
```

## Important Formula

```text
First Index = 0
Last Index = n - 1
```

## Access

```cpp
arr[i]
```

```text
O(1)
```

## Traversal

```cpp
for (int i = 0; i < n; i++)
```

```text
O(n)
```

## Insertion

```text
Shift Right → Insert
```

```text
O(n) worst case
```

## Deletion

```text
Shift Left → Delete
```

```text
O(n) worst case
```

## Searching

```text
Linear Search → O(n)
Binary Search → O(log n), sorted array required
```

---

# 35. Revision Checklist

Before your test, make sure you can:

-  Define an array
    
-  Explain indexing
    
-  Explain contiguous memory
    
-  Declare and initialize an array
    
-  Traverse an array using a loop
    
-  Update an element
    
-  Insert an element at a position
    
-  Delete an element at a position
    
-  Write Linear Search
    
-  Explain Binary Search
    
-  Explain why Binary Search needs a sorted array
    
-  Work with 2D arrays
    
-  Explain the time complexity of common operations
    
-  Compare arrays with linked lists
    
-  Explain how arrays are used to implement stacks and queues
    

> [!success] The One-Sentence Concept  
> **An array is a collection of elements of the same type stored in contiguous memory locations, allowing fast direct access using indexes.**

# 🎯 Final Study Advice

For array questions, always draw something like this:

```text
Index:    0    1    2    3    4
         ┌───┬───┬───┬───┬───┐
Array:   │   │   │   │   │   │
         └───┴───┴───┴───┴───┘
```

Then manually trace what happens.

For insertion, ask:

> **Which elements must move to the right?**

For deletion, ask:

> **Which elements must move to the left?**

For searching, ask:

> **Is the array sorted or unsorted?**

Once you can visually trace indexes and shifting, most beginner and intermediate array questions become much easier.