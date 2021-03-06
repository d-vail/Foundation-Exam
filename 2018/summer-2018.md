# Summer 2018

## Data Structures

### A 1: Dynamic Memory Management in C

{% tabs %}
{% tab title="Question" %}
#### 5 points

Suppose we have an array of structures containing information about our group for a group project. Each index should contain a group member’s name and phone number. The structure is shown below: names are stored as dynamically allocated strings and phone numbers are stored as integers. When the semester is over, we will delete this array. Write a function called deleteGroup that will take in this array and delete all the information, freeing all the memory space that the array previously took up. Your function should take 2 parameters: a pointer to the beginning of the array and an integer indicating the number of group members. It should return a null pointer representing the now empty array.

```c
typedef struct GroupMember
{
  char *name;
  int phoneNumber;
} GroupMember;

GroupMember* deleteGroup (GroupMember *group, int numMembers)
{
  int i;

  // your code
}
```
{% endtab %}

{% tab title="Solution" %}
```c
typedef struct GroupMember
{
  char *name;
  int phoneNumber;
} GroupMember;

GroupMember* deleteGroup (GroupMember *group, int numMembers)
{
  int i;

  for(i=0; i<numMembers; i++) // 1 pt
    free(group[i].name);      // 2 pts

  free(group);                // 1 pt

  return NULL;                // 1 pt
}
```
{% endtab %}
{% endtabs %}

### A 2: Linked Lists

{% tabs %}
{% tab title="Question" %}
#### 10 points

Suppose we have a linked list implemented with the structure below. Write a function that will take in a pointer to the head of a list and inserts a node storing -1 _**after**_ each even value in the list. If the list is empty or there are no even values in the list, no modifications should be made to the list. \(For example, if the initial list had 2, 6, 7, 1, 3, and 8, the resulting list would have 2, -1, 6, -1, 7, 1, 8, -1.\)

```c
typedef struct node
{
  int data;
  struct node* next;
} node;

void markEven(node *head)
{
  // your code
}
```
{% endtab %}

{% tab title="Solution" %}
```c
typedef struct node
{
  int data;
  struct node* next;
} node;

void markEven(node *head)
{
  node* tmp = head;

  while (tmp != NULL)                         // 2 pts iter whole list
  {
    while (tmp != NULL && tmp->data%2 != 0)   // 3 pts find next even
      tmp = tmp->next;

    if (tmp != NULL)                          // 1 pt no null error
    {
      node* newnode = malloc(sizeof(node));
      newnode->data = -1;                     // 2 pts make new node
      newnode->next = tmp->next;              // 2 pts patch it into list
      tmp->next = newnode;
      tmp = newnode;
    }
  }
}
```
{% endtab %}
{% endtabs %}

### A 3: Stacks

{% tabs %}
{% tab title="Question" %}
#### 10 points

**\(a\)** \(6 pts\) Convert the following infix expression to postfix using a stack. Show the contents of the stack at the indicated points \(1, 2, and 3\) in the infix expression.

![](../.gitbook/assets/summer-2018-ds-a-3.png)

**\(b\)** \(4 pts\) Whenever a recursive function is called, the function calls go onto a call stack. The depth of the call stack is the number of different recursive calls on the stack at a particular point in time, which indicates the number of different recursive calls that have started, but have not completed. What is the maximum stack depth of the call stack when the function fib\(10\) is executed? Is this maximum stack depth equal to the number of times the recursive function, fib, is called? Assume the implementation of the Fibonacci function shown below:

```c
int fib(int n)
{
  if (n < 2) return n;
  return fib(n-1) + fib(n-2);
}
```

Maximum Stack Depth: _\*\*\_\_\*\*\_

Is Max Stack Depth equal to the \# of recursive calls? YES NO \(Circle the correct answer.\)
{% endtab %}

{% tab title="Solution" %}
**\(a\)**

![](../.gitbook/assets/summer-2018-ds-a-3-sol.png)

_**Grading: 1 point for each stack, 3 points for the whole expression \(partial credit allowed.\)**_

**\(b\)**

```c
int fib(int n)
{
  if (n < 2) return n;
  return fib(n-1) + fib(n-2);
}
```

Maximum Stack Depth: 10

_**Grading: 2 pts for 10 or 9, 1 pt to be within 3, 0 pts otherwise**_

Is Max Stack Depth equal to the \# of recursive calls?: NO

_**Grading: 2 pts correct, 0 otherwise**_
{% endtab %}
{% endtabs %}

### B 1: Binary Search Trees

{% tabs %}
{% tab title="Question" %}
#### 10 points

Complete writing function shown below _**recursively**_, so that it takes in a pointer to the root of a binary search tree, _root_, and an integer, _value_, and returns the number of nodes in the tree that are divisible by _value_. The struct used to store a node is shown below.

```c
typedef struct bstNode
{
  struct bstNode *left, *right;
  int data;
} bstNode;

int countDiv(bstNode *root, int value)
{
  // your code
}
```
{% endtab %}

{% tab title="Solution" %}
```c
typedef struct bstNode
{
  struct bstNode *left, *right;
  int data;
} bstNode;

int countDiv(bstNode *root, int value)
{
  if (root == NULL) return 0;               // 2 pts

  // 4 pts, 2 pts for each recursive call.
  int res = countDiv(root->left, value) + countDiv(root->right, value);

  // 2 pts for checking divisibility, 1 pt for adding 1
  if (root->data % value == 0)
    res++;

  // 1 pt for returning.
  return res;
}
```
{% endtab %}
{% endtabs %}

### B 2: Heaps

{% tabs %}
{% tab title="Question" %}
#### 5 points

Suppose we are storing integers in a **Max-Heap** using the tree representation of heaps. The following tree shows the Max-Heap after 5 insertions. Show the result of inserting 109 into this heap, showing each step of the process. \(Hint: You should draw 3 separate tree pictures.\) Then, place each value from the resulting heap of 6 values into the array in the appropriate indexes corresponding to how a heap is typically stored in an array.

![](../.gitbook/assets/summer-2018-ds-b-2.png)

Insert 109 Step 1:

Insert 109 Step 2:

Insert 109 Step 3:

![](../.gitbook/assets/summer-2018-ds-b-2-b.png)
{% endtab %}

{% tab title="Solution" %}
![](../.gitbook/assets/summer-2018-ds-b-2-sol.png)

_**Grading: 1 pt for each drawing, 2 pts for correct array, 1 pt for minor error in the array, 0 pt for major error in array.**_
{% endtab %}
{% endtabs %}

### B 3: AVL Trees

{% tabs %}
{% tab title="Question" %}
#### 10 points

\(a\) \(8 pts\) Create an AVL tree by inserting the following values into an initially empty AVL Tree in the order given: 7, 8, 54, 13, 35, 66, 50, and 12. Show the state of the tree after each insertion.

\(b\) \(2 pts\) Draw the state of the tree after the deletion of the node containing the value 7.
{% endtab %}

{% tab title="Solution" %}
#### 10 points

**\(a\)**

![](../.gitbook/assets/summer-2018-ds-b-3-sol-a.png)

_**Grading: Students should show each insertion step for 1 pt each. Imbalances should be detected and corrected for after inserting 54, 35, and 66; detected at 7, 54, and 8 respectively.**_

**\(b\)**

![](../.gitbook/assets/summer-2018-ds-b-3-sol-b.png)

Deleting 7 creates an imbalance at 8 that must be corrected.

_**Grading: 1 pt for a valid BST without 7, 1 pt for it being the correct BST without 7 \(0 pts if either 7 is still in it or it's not a valid BST.\)**_
{% endtab %}
{% endtabs %}

## Algorithms and Analysis Tools

### A 1: Algorithm Analysis

{% tabs %}
{% tab title="Question" %}
#### 10 points
{% endtab %}

{% tab title="Solution" %}

{% endtab %}
{% endtabs %}

### A 2: Algorithm Analysis

{% tabs %}
{% tab title="Question" %}
#### 5 points
{% endtab %}

{% tab title="Solution" %}

{% endtab %}
{% endtabs %}

### A 3: Summations

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

Consider writing a recursive method that raises a polynomial to an exponent, calculating each of its coefficients mod a given integer. One way this method could work is checking to see if the exponent is even. If so, raise the polynomial to half of the original power. Then, take that result \(a polynomial\) and multiply it by itself for the result. If the original exponent, exp, was odd, then we could simply first raise the polynomial to exp-1, and then take that result and multiply it by the original polynomial. Implement this algorithm recursively below. You are given the code for the multiply function and should call it accordingly. A polynomial is stored as an array of integers, where poly\[i\] is the coefficient to x i . In the function signature, len is the length of the array poly, so poly is of degree len-1, exp is the exponent to which we are raising the polynomial and mod is the modulus by which we are calculating each coefficient.

```c
int* power(int* poly, int len, int exp, int mod) {
  if (exp == 0) {
    int* res = malloc(sizeof(int));
    res[0] = 1;
    return res;
  }

  if (exp == 1) {
    int* res = malloc(len*sizeof(int));
    int i;
    for (i=0; i<len; i++) res[i] = poly[i]%mod;
    return res;
  }

  if (exp%2 == 0) {
    int* tmp = power(poly, _______, _______, mod);
    int* prod = multiply(___________, ______________,
                         ___________, ____________, mod)
    free(tmp);
    return prod;
  }

  int* tmp = power(poly, ________, __________, mod);
  int* prod = multiply(_____, _________________________________,
                       poly, len, mod);

  free(tmp);
  return prod;
}

int* multiply(int* poly1, int len1, int* poly2, int len2, int mod) {
  int* res = calloc(len1+len2-1, sizeof(int));
  int i, j;
  for (i=0; i<len1; i++)
    for (j=0; j<len2; j++)
      res[i+j] = (res[i+j] + poly1[i]*poly2[j])%mod;
  return res;
}
```
{% endtab %}

{% tab title="Solution" %}
```c
int* power(int* poly, int len, int exp, int mod) {
  if (exp == 0) {
    int* res = malloc(sizeof(int));
    res[0] = 1;
    return res;
  }

  if (exp == 1) {
    int* res = malloc(len*sizeof(int));
    int i;
    for (i=0; i<len; i++) res[i] = poly[i]%mod;
    return res;
  }

  if (exp%2 == 0) {
    int* tmp = power(poly, len, exp/2, mod);
    int* prod = multiply(tmp, (len-1)*exp/2+1, tmp, (len-1)*exp/2+1, mod)
    free(tmp);
    return prod;
  }

  int* tmp = power(poly, len, exp-1, mod);
  int* prod = multiply(tmp, (len-1)*(exp-1)+1, poly, len, mod);

  free(tmp);
  return prod;
}

int* multiply(int* poly1, int len1, int* poly2, int len2, int mod) {
  int* res = calloc(len1+len2-1, sizeof(int));
  int i, j;
  for (i=0; i<len1; i++)
    for (j=0; j<len2; j++)
      res[i+j] = (res[i+j] + poly1[i]*poly2[j])%mod;
  return res;
}
```

_**Grading: 1 pt per slot, all or nothing per slot.**_
{% endtab %}
{% endtabs %}

### B 2: Sorting

{% tabs %}
{% tab title="Question" %}
#### 10 points

Consider sorting students, where each student has a first name, last name and a unique ID number. Assume all names contain uppercase letters only, so that strcmp does an alphabetic comparison for the purposes of this problem. Complete the code below so that it sorts students by last name \(A to Z\), breaking ties by first name \(A to Z\), and finally breaking ties between students with identical first and last names by ID number \(smallest to largest\). For example, if we have the students \(EMILIO SANCHEZ 17\), \(ANDREA SANCHEZ 22\), and \(EMILIO SANCHEZ 10\), the correct ordering would be ANDREA SANCHEZ, followed by EMILIO SANCHEZ 10, with EMILIO SANCHEZ 17 last.

```c
typedef struct student {
  char first[20];
  char last[20];
  int ID;
} student;

void sort(student** list, int len) {
  int i,j;

  for (i=len-1; i>0; i--) {
    for (j=0; j<i; j++) {
      if (cmp(list[j], list[j+1]) > 0) {
        student* tmp = list[j];
        list[j] = list[j+1];
        list[j+1] = tmp;
      }
    }
  }
}

int cmp(student* a, student* b)
{
  // your code
}
```
{% endtab %}

{% tab title="Solution" %}
```c
int cmp(student* a, student* b)
{
  if (strcmp(a->last, b->last) != 0)
    return strcmp(a->last, b->last);

  if (strcmp(a->first, b->first) != 0)
    return strcmp(a->first, b->first);

  return a->ID - b->ID;
}
```

_**Grading: 3 pts for breaking ties properly by last name, 3 pts for breaking ties properly by first name, 4 pts for breaking ties by ID. If no string functions are used but the logic is correct via regular relational operators, then take off 4 pts total for not properly calling the functions.**_
{% endtab %}
{% endtabs %}

### B 3: Bitwise Operators

{% tabs %}
{% tab title="Question" %}
#### 5 points

What is the output of the following program?

```c
#include <stdio.h>
int main() {
  int n = 182, i = 0;

  while (n > 0) {
    if ((n & (1<<i)) > 0) {
      printf("%d\n", (1<<i));
      n ^=(1<<i);
    }
    i++;
  }
  return 0;
}
```
{% endtab %}

{% tab title="Solution" %}
2 4 16 32 128

_**Grading: 1 pt per correct number listed. 1 pt off per extra number listed, cap at 0.**_
{% endtab %}
{% endtabs %}

## PDF Files

{% file src="../.gitbook/assets/FE-May18.pdf" caption="Summer 2018 Exam" %}

{% file src="../.gitbook/assets/FE-May18-Sol.pdf" caption="Summer 2018 Exam Solutions" %}

{% file src="../.gitbook/assets/FE-May18-Info.pdf" caption="Summer 2018 Exam Statistics" %}

