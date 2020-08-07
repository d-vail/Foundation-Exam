# Spring 2017

## Data Structures

### A 1: Dynamic Memory Management in C

{% tabs %}
{% tab title="Question" %}
#### 10 points

A catalogue of _apps_ and their price is stored in a text file. Each line of the file contains the name of an app \(1-19 letters\) followed by its price with a space in between. Write a function called `makeAppArray` that reads the _app information_ from the file and stores it in an array of app pointers. Your function should take 2 parameters: a pointer to the file containing the app information and an integer indicating the number of _**apps**_ in the file. It should return a pointer to the array of _**apps**_. An _**app**_ is stored in a struct as follows:

```c
typedef struct app
{
  char name[20];
  float price;
} app;
```

Make sure to allocate memory dynamically. The function signature is:

```c
app** makeAppArray(FILE* fp, int numApps)
{
  // your code
}
```
{% endtab %}

{% tab title="Solution" %}
```c
app** makeAppArray(FILE* fp, int numApps)
{
  app** appArray = (app**)malloc(numApps * sizeof(app*)); // 3 pts
  int i;

  for(i=0; i < numApps; i++)
  {
    appArray[i] = (app*)malloc(sizeof(app));              // 2 pts
    fscanf(fp, "%s", appArray[i]->name);                  // 2 pts
    fscanf(fp, "%f", &(appArray[i]->price));              // 2 pts
  }

  return appArray;                                        // 1 pt
}
```

_**Grading notes: the casts aren't necessary, no points off for forgetting to declare i, no points off if only one percent code is wrong, 1 pt off if both percent codes are wrong, take only 1 pt off total if the syntax for reading from a file is incorrect, take off only 1 pt total if they use a dot instead of an array, they can order these statements differently - they can allocate ALL of the space before reading anything in.**_
{% endtab %}
{% endtabs %}

### A 2: Linked Lists

{% tabs %}
{% tab title="Question" %}
#### 5 points

Consider the following function that takes in as a parameter a pointer to the front of a linked list\(list\) and the number of items in the list\(size\). _**node**_ is defined as follows:

```c
typedef struct node
{
  int data;
  struct node* next;
} node;

int mystery(node* list, int size)
{
  node* prev = list;
  node* temp = list->next;

  while (temp != NULL)
  {
    if (list->data == temp->data)
    {
      prev->next = temp->next;
      free(temp);
      size--;
      temp = prev->next;
    }
    else
    {
      prev = prev->next;
      temp = temp->next;
    }
  }

  return size;
}
```

If `mystery(head, 7)`, is called, where head is shown below, what will the function return and draw a picture of the resulting list, right after the call completes?

![](../.gitbook/assets/spring-2017-ds-a-2.png)

Adjusted List:

Return Value: **\_**
{% endtab %}

{% tab title="Solution" %}
Adjusted List:

![](../.gitbook/assets/spring-2017-ds-a-2-sol.png)

Return Value: 5

_**Grading: 2 pts return value \(all or nothing\), 3 pts list, give partial for list as you see fit.**_
{% endtab %}
{% endtabs %}

### A 3: Queues

{% tabs %}
{% tab title="Question" %}
#### 10 points

A queue is implemented as an array. The queue has the 2 attributes, front and size. front is the index in the array where the next element to be removed from the queue can be found, if the queue is non-empty. \(If the queue is empty, front may be any valid array index from 0 to 19.\) size is the total number of elements currently in the queue. For efficient use of resources, elements can be added to the queue not just at the end of the array but also in the indices at the beginning of the array before front. Such a queue is called a circular queue. A circular queue has the following structure:

```c
typedef struct
{
  int values[20];
  int front, size;
} cQueue;
```

Write an enqueue function for this queue. If the queue is already full, return 0 and take no other action. If the queue isn't full, enqueue the integer item into the queue, make the necessary adjustments, and return 1. Since the array size is hard-coded to be 20 in the struct above, you may use this value in your code and assume that is the size of the array values inside the struct.

```c
int enqueue(cQueue* thisQ, int item)
{
  // your code
}
```
{% endtab %}

{% tab title="Solution" %}
```c
int enqueue(cQueue* thisQ, int item)
{
  if (thisQ->size == 20)                                  // 2 pts
    return 0;                                             // 1 pt

  // 5 pts: 1 values, 3 pts index, 1 pt item
  thisQ->values[(thisQ->front+thisQ->size)%20] = item;

  thisQ->size++;                                          // 1 pt
  return 1;                                               // 1 pt
}
```

_**Grading notes: If they forget thisQ-&gt; each time, take off 2 pts total.**_
{% endtab %}
{% endtabs %}

### B 1: Binary Trees

{% tabs %}
{% tab title="Question" %}
#### 10 points

Michael took CS 1 last semester. During the Winter break he thought that it would be cool to keep track of all of the new words that he learned while reading a novel. He has stored all of his words \(all 1-19 lowercase letters only\) in alphabetic order in a binary search tree \(BST\). The nodes of his BST are stored in the following structure:

```c
typedef struct
{
  struct node *left, *right;
  char word[20];
} bsNode;
```

Michael wants to count the number of words in his binary search tree that come before a specified word in alphabetical order. Write a _**recursive**_ function `countBefore` which takes in a pointer to the root of a binary search tree storing the words and a string `target` \(of 1-19 lowercase letters only\) and returns the number of words in the tree that _**come before**_ `target`, alphabetically.

```c
int countBefore(bsNode* root, char target[])
{
  // your code
}
```
{% endtab %}

{% tab title="Solution" %}
```c
int countBefore(bsNode* root, char target[])
{
  if (root == NULL) return 0;                                     // 2 pts
  if (strcmp(target, root->word) <= 0)                            // 2 pts
    return countBefore(root->left);                               // 2 pts

  // 1 pt return, 1 pt 1, 1 pt left, 1 pt right
  return 1 + countBefore(root->left) + countBefore(root->right);
}
```
{% endtab %}
{% endtabs %}

### B 2: Hash Maps

{% tabs %}
{% tab title="Question" %}
#### 5 points

**\(a\)** \(3 pts\) A set of students’ names are stored in a hash table implemented as an array of size 25. Their grades out of 100 are used as input to the hashing function. Suggest one hash function that can be used to store the names. Would your function cause clashes? Explain your answer.

**\(b\)** \(2 pts\) If the following students have the grades shown, and your hash function given in \(a\) is used, draw the state of the hash map after these 3 entries are inserted into the table. \(Note: No need to show all 25 array slots, just clearly label the index and contents of each of the non-empty array slots.\)

**Mary 60**

**Ben 75**

**Dona 13**
{% endtab %}

{% tab title="Solution" %}
**\(a\)**

Hash function stores the student’s name in the array index score%25. Hashmap\[score%25\] = name score

**Grading: 2 pts, note, MANY answers are valid here!!!**

This function can cause collisions since 2 distinct scores can has to the same index or because two different students can earn the exact same score!

**Grading: 1 pt**

**\(b\)**

**Mary 60** **Ben 75** **Dona 13**

![](../.gitbook/assets/spring-2017-ds-b-2-sol.png)

_**Grading: 2 pts for correct response \(BASED ON THEIR HASH FUNCTION\), 1 pt if some of their answer is correct**_
{% endtab %}
{% endtabs %}

### B 3: AVL Trees

{% tabs %}
{% tab title="Question" %}
#### 10 points

**\(a\)** \(8 pts\) Create an AVL tree by inserting the following values in the order given: 38, 72, 58, 16, 3, 24, 8, and 15. Show the state of the tree after each insertion.

**\(b\)** \(2 pts\) Draw the state of the tree after the deletion of the node containing the value 16.
{% endtab %}

{% tab title="Solution" %}
**\(a\)**

Note: it the solution below, rotations aren't shown, just the final answers after the appropriate rotations. Steps where rotations were necessary are marked with an astericks at the root of the rotation.

![](../.gitbook/assets/spring-2017-ds-b-3-sol.png)

_**Grading: 1 pt for each tree, as long as the insertion on step k was of equal difficulty to the correct insertion, give the point as long as the insertion is correct based on their answer for step k-1.**_

**\(b\)**

There are two possible answers here. One may replace the 16 with either the 15 or 24 and then delete the physical node where the 15 or 24 was stored, respectively. The answer on the left is what occurs when we replace 16 with 15 and the answer on the right is what occurs when we replace 16 with 24:

_**Grading: 2 pts**_
{% endtab %}
{% endtabs %}

## Algorithms and Analysis Tools

### A 1: Algorithm Analysis

{% tabs %}
{% tab title="Question" %}
#### 5 points
{% endtab %}

{% tab title="Solution" %}

{% endtab %}
{% endtabs %}

### A 2: Algorithm Analysis

{% tabs %}
{% tab title="Question" %}
#### 10 points
{% endtab %}

{% tab title="Solution" %}

{% endtab %}
{% endtabs %}

### A 3: Summations and Recurrence Relations

{% tabs %}
{% tab title="Question" %}
#### 10 points
{% endtab %}

{% tab title="Solution" %}

{% endtab %}
{% endtabs %}

### B 1: Recursive Coding

{% tabs %}
{% tab title="Question" %}
#### 10 points

Write a recursive function that returns 1 if an array of size n is in sorted order from smallest to largest with all values less than or equal to max, and 0 otherwise. Note: If array a stores 3, 6, 7, 7, 12, then `isSorted(a, 12, 5)` should return 1 but `isSorted(a, 11, 5)` should return 0. If array b stores 3, 4, 9, 8, then `isSorted(b, 20, 4)` should return 0, since 9 is bigger than 8 but appears before it.

```c
int isSorted(int* array, int max, int n)
{
  // your code
}
```
{% endtab %}

{% tab title="Solution" %}
```c
int isSorted(int* array, int max, int n)
{
  if (n == 0) return 1;                     // 3 pts
  if (array[n-1] > max) return 0;           // 3 pts
  return isSorted(array, array[n-1], n-1);  // 4 pts
}
```

Grading:

Lots of ways to solve this problem. Map their solution to the cases laid out here:

* 0/1 size case: 3 pts
* Checking last element too big: 3 pts
* Recursive call if last pair \(or first pair\) is valid: 4 pts

The points are mapped so that many items could be off by a tiny bit, so adjust the points as necessary. If there are two small errors in two different places each worth 2 pts, just take off 1 point for one of the two errors and let the other one go.

Note: If max was not a parameter to the function and we wanted to simply write a recursive function that determined if the array specified by the parameters was sorted or not, the following function would suffice:

```c
int isSortedAlt(int* array, int n) {
  if (n < 2) return 1;
  if (array[n-1] < array[n-2]) return 0;
  return isSortedAlt(array, n-1);
}
```
{% endtab %}
{% endtabs %}

### B 2: Sorting

{% tabs %}
{% tab title="Question" %}
#### 5 points

Consider running a Merge Sort on the array shown below. Show the state of the array **right before** the last Merge is performed. \(Note: due to the nature of this question, relatively little partial credit will be awarded for incorrect answers.\)

![](../.gitbook/assets/spring-2017-aa-b-2.png)
{% endtab %}

{% tab title="Solution" %}
![](../.gitbook/assets/spring-2017-aa-b-2-sol.png)

_**Grading: 5 pts for correct answer, 2 pts for sorted pairs \(8 13 2 9 1 17 5 6\), 2 pts for \(2 8 9 13 1 17 6 5\), 2 pts for \(1 2 8 9 13 17 6 5\), 0 pts for all others**_
{% endtab %}
{% endtabs %}

### B 3: Backtracking

{% tabs %}
{% tab title="Question" %}
#### 10 points

A D-digit divisible number is a positive integer of D digits \(with no leading digits zero\) such that each of its prefixes of k digits is a number divisible by k. For example, 52240 is a 5-digit divisble number because 5 is divisible by 1, 52 is divisible by 2, 522 is divisible by 3, 5224 is divisible by 4 and 52240 is divisible by 5. Assume that there exists a function as specified below:

`int kDigitPrefixValue(char* number, int k);`

such that if number is storing the string version of an integer that is at least k digits long, then the function will return the integer value of the first k digits represented in number. For example, `kDigitPrefixValue("52240", 4)` will return the integer 5224.

Complete the recursive function below so that it will print out all 6-digit divisible numbers. \(A complete wrapper function is provided for you, so just fill out the blanks in the recursive function.\)

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int kDigitPrefixValue(char* number, int k);
void printkDivisibleRec(char* number, int k);
void wrapper(int numdigits);

int main() {
  wrapper(6);
  return 0;
}

void wrapper(int numdigits) {
  char* tmp = malloc(sizeof(char)*(numdigits+1));
  int i;
  for (i=0; i<numdigits; i++) tmp[i] = '0';
  tmp[numdigits] = '\0';
  printkDivisibleRec(tmp, 0);
  free(tmp);
}

void printkDivisibleRec(char* number, int k) {
  if (k == strlen(number)) {
    printf("%s\n", number);
    return;
  }

  int i = k == 0 ? 1 : 0;

  for (; i < ____ ; i++) {
    number[ ___ ] = (char)( ____ +'0');
    int prefix = ___________________________(number, _______ );
    if ( __________ %( ________ ) == ____ )
      _____________________________(number, ________ );
  }
}
```
{% endtab %}

{% tab title="Solution" %}
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int kDigitPrefixValue(char* number, int k);
void printkDivisibleRec(char* number, int k);
void wrapper(int numdigits);

int main() {
  wrapper(6);
  return 0;
}

void wrapper(int numdigits) {
  char* tmp = malloc(sizeof(char)*(numdigits+1));
  int i;
  for (i=0; i<numdigits; i++) tmp[i] = '0';
  tmp[numdigits] = '\0';
  printkDivisibleRec(tmp, 0);
  free(tmp);
}

void printkDivisibleRec(char* number, int k) {
  if (k == strlen(number)) {
    printf("%s\n", number);
    return;
  }

  int i = k == 0 ? 1 : 0;

  for (; i < 10 ; i++) {
    number[ k ] = (char)( i +'0');
    int prefix = kDigitPrefixValue(number, k+1);
    if ( prefix %( k+1 ) == 0 )
      printDivisibleRec(number, k+1);
  }
}
```

_**Grading: 1 pt per blank**_
{% endtab %}
{% endtabs %}

## PDF Files

{% file src="../.gitbook/assets/FE-Jan17.pdf" caption="Summer 2017 Exam" %}

{% file src="../.gitbook/assets/FE-Jan17-Sol.pdf" caption="Summer 2017 Exam Solutions" %}

{% file src="../.gitbook/assets/FE-Jan17-Info.pdf" caption="Summer 2017 Exam Statistics" %}

