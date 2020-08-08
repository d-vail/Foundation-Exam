# Summer 2017

## Data Structures

### A 1: Dynamic Memory Management in C

{% tabs %}
{% tab title="Question" %}
#### 10 points

Suppose we would like to create an array to store our Must Watch TV list. Currently our list is stored in a text file with the name of each TV show on a line by itself. The name of each show consists of only letters and underscores and doesn't exceed 127 characters. Write a function called makeTVList that reads these names from a file, allocates memory dynamically to store the names, stores them in a two- dimensional character array and returns a pointer to that array. Your function should take 2 parameters: a pointer to the file and an integer indicating the number of TV shows in the file. It should return a pointer to the array of shows. Be sure to allocate memory for the array dynamically and only allocate as much space as is needed. Namely, do not allocate 128 characters to store each show name. Instead dynamically allocate an appropriate number of characters as necessary. Use any necessary functions from string.h.

```c
char ** makeTVList (FILE *ifp, int numShows)
{
  char buffer[128];
  char **TVList = NULL;
  int i;
}
```
{% endtab %}

{% tab title="Solution" %}
```c
char ** makeTVList (FILE *ifp, int numShows)
{
  char buffer[128];
  char **TVList = NULL;
  int i;

  TVList = malloc(numShows * sizeof(char *));               // 2 pts

  for(i=0; i<numShows; i++)                                 // 1 pt
  {
    fscanf(ifp, “%s”, buffer);                              // 1 pt
    TVList[i] = malloc((strlen(buffer)+1)*(sizeof(char)));  // 3 pts
    strcpy(TVList[i], buffer);                              // 2 pts
  }

  return TVList;                                            // 1 pt
}
```
{% endtab %}
{% endtabs %}

### A 2: Linked Lists

{% tabs %}
{% tab title="Question" %}
#### 10 points

Suppose we have a stack implemented as a linked list. The stack is considered “full” if it has 20 nodes and empty if the head pointer is NULL. The nodes of the stack have the following structure:

```c
typedef struct node
{
  int data;
  struct node* next;
} node;
```

Write a function to determine if the stack is full.

```c
int isFull(node *stack)
{
  // your code
}
```
{% endtab %}

{% tab title="Solution" %}
```c
int isFull(node *stack)
{
  int count = 0;            // 1 pt initializing a counter
  node *helper = stack;

  if (stack == NULL)        // 2 pts checking if stack is null
    return 0; 

  while(helper != NULL)     // 2 pts iter linked list
  {
    count++;                // 1 pt incrementing counter
    helper = helper->next;  // 1 pt advancing node
  }                         // Note: can stop at 20...

  if (count >= 20)          // 2 pts returning true iff 20 or more
    return 1; 

  return 0;                 // 1 pt returning false if no

  // Note: return count >= 20; takes care of both...
}
```

Alternate solution.

```c
int isFull(node *stack)
{
  int i;                          // 1 pt

  for (i=0; i<20; i++)            // 2 pts
  {
    if (stack == NULL) return 0;  // 3 pts
    stack = stack->next;          // 2 pts
  }

  return 1;                       // 2 pts
}
```
{% endtab %}
{% endtabs %}

### A 3: Stacks

{% tabs %}
{% tab title="Question" %}
#### 5 points

Convert the following infix expression to postfix using a stack. Show the contents of the stack at the indicated points \(1, 2, and 3\) in the infix expression.

![](../.gitbook/assets/summer-2017-ds-a-3.png)
{% endtab %}

{% tab title="Solution" %}
![](../.gitbook/assets/summer-2017-ds-a-3-sol.png)

_**Grading: 1 point for each stack, 2 points for the whole expression \(partial credit allowed.\)**_
{% endtab %}
{% endtabs %}

### B 1: Binary Search Trees

{% tabs %}
{% tab title="Question" %}
#### 10 points

**\(a\)** \(3 pts\) Given the following traversals, draw the Binary Search Tree they represent.

Pre-Order: 2, 0, 1, 10, 9, 12 Post-Order: 1, 0, 9, 12, 10, 2 In-Order: 0, 1, 2, 9, 10, 12

**\(b\)** If the nodes of the BST have the following structure, construct a recursive function to count the number of nodes in the tree.

```c
typedef struct bstNode
{
  struct bstNode *left, *right;
  char word[20];
} bstNode;

int count(bstNode *root)
{
  // your code
}
```

**\(c\)** \(2 pts\) Write a single line of code calling the count function that assigns the number of nodes in the left subtree of the tree pointed to by a pointer `myTreePtr` to the integer variable `leftCount`. You may assume that `myTreePtr` is not pointing to NULL and points to an actual `bstNode`.
{% endtab %}

{% tab title="Solution" %}
**\(a\)**

![](../.gitbook/assets/summer-2017-ds-b-1-sol.png)

_**Grading: 1 pt placing 2 at the root, 1 pt left subtree, 1 pt right subtree**_

**\(b\)**

```c
typedef struct bstNode
{
  struct bstNode *left, *right;
  char word[20];
} bstNode;

int count(bstNode *root)
{
  if (root == NULL) return 0;                         // 2 pts

  // 1 pt 1, 1 pt left, 1 pt right
  return 1 + count(root->left) + count(root->right);
}
```

**\(c\)**

```c
int leftCount = count(myTreePtr->left);   // 2 pts
```
{% endtab %}
{% endtabs %}

### B 2: Heaps

{% tabs %}
{% tab title="Question" %}
#### 5 points

**\(a\)** \(1 pts\) In her computer science courses, Maria has learned some interesting things about prime numbers and data structures. She has decided to store some prime numbers in a Max-Heap using the tree representation of heaps. If Maria has stored 125 prime numbers, how tall would the Heap be?

**\(b\)** \(2 pts\) Here is the Max-Heap after 5 insertions. Clearly draw a circle in the location where the next prime will initially be inserted. Also draw a pointer from the parent of this node initially and clearly indicate whether or not the pointer is a left or right pointer.

![](../.gitbook/assets/summer-2017-ds-b-2.png)

**\(c\)** \(2 pts\) Show each step of inserting 1609 into the Max-Heap from part \(b\). Please draw a different picture for each of the different positions 1609 will be in the heap.
{% endtab %}

{% tab title="Solution" %}
**\(a\)**

Height = 6

Heaps are complete binary trees, so the height is determined by ⌊log 2 125⌋. You can also add the “levels” of the tree: 1 + 2 + 4 + 8 + 16 + 32 + 62.

_**Grading: 1 pt all or nothing**_

**\(b\)**

![](../.gitbook/assets/summer-2017-ds-b-2-sol-a.png)

The next node must be added as the left child of 1291.

_**Grading: 2 pts all or nothing**_

**\(c\)**

![](../.gitbook/assets/summer-2017-ds-b-2-sol-b.png)

Students should show both percolate up steps for 1609. 1 point per step. If they don't show the middle step and just have the final picture with 1609 as the root, award 1 point out of 2.
{% endtab %}
{% endtabs %}

### B 3: AVL Trees

{% tabs %}
{% tab title="Question" %}
#### 10 points

**\(a\)** \(8 pts\) Create an AVL tree by inserting the following values in the order given: 42, 68, 35, 1, 70, 25, 79, and 59. Show the state of the tree after each insertion. Draw a box around each of these 8 trees.

**\(b\)** \(2 pts\) Draw the state of the tree after the deletion of the node containing the value 79 from the tree at the end of part \(a\).
{% endtab %}

{% tab title="Solution" %}
**\(a\)**

![](../.gitbook/assets/summer-2017-ds-b-3-sol-a.png)

_**Grading: Students should show each insertion step for 1 pt each. Imbalances should be detected and corrected for after inserting 25 and after inserting 79; detected at 35 and 68 respectively.**_

**\(b\)**

![](../.gitbook/assets/summer-2017-ds-b-3-sol-b.png)

_**Grading: Deleting 79 creates an imbalance at 70 that must be corrected.**_
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
#### 5 points

Write a recursive function that returns the product of the digits of its integer input parameter, n. You may assume that n is non-negative. For example, productDigits\(274\) should return 56, since 2 x 7 x 4 = 56.

```c
int productDigits(int n)
{
  // your code
}
```
{% endtab %}

{% tab title="Solution" %}
```c
int productDigits(int n)
{
  if (n < 10)                           // 1 pt
    return n;                           // 1 pt

  return (n%10)*productDigits(n/10);    // 1 pt return
                                        // 1 pts n%10
                                        // 1 pt *pD(n/10)
}
```
{% endtab %}
{% endtabs %}

### B 2: Sorting

{% tabs %}
{% tab title="Question" %}
#### 10 points

\(a\) \(5 pts\) Show the contents of the following array after each iteration of Bubble Sort. The result after both the first and last iteration have been included for convenience. \(Note: due to the nature of this question, relatively little partial credit will be awarded for incorrect answers.\)

![](../.gitbook/assets/summer-2017-aa-b-2-a.png)

\(b\) \(5 pts\) The array shown below has been partitioned exactly once \(first function call in a Quick Sort of an array.\) Which element was the partition element? Why?

![](../.gitbook/assets/summer-2017-aa-b-2-b.png)

Partition Element Index:

Partition Element Value:

Reason it was the Partition Element:
{% endtab %}

{% tab title="Solution" %}
\(a\)

![](../.gitbook/assets/summer-2017-aa-b-2-sol-a.png)

_**Grading: 1 pt per each row, to earn the point all values in the row have to be correct.**_

\(b\)

![](../.gitbook/assets/summer-2017-aa-b-2-sol-b.png)

Partition Element Index: 5 _**Grading: 1 pt**_ 

Partition Element Value: 27 _**Grading: 1 pt**_

Reason it was the Partition Element:

It is the only value for each everything to the left of it is less than it and everything to the right of it is greater than it. \(For 16, 19, 13 and 12, we have 9 to its right, so these four can't be the partition. 9 can't be the partition since 12 is to its left, 49 can't be the partition since 33 to is to its right, and 33 can't be the partition because 49 is to its left.\)

_**Grading: 3 pts for the reason, the details in the \(\)'s need not be in student responses, but a clear understanding that the partition element is the one where everything to its left is less than it and everything to its right is greater than it is necessary for full credit. Award partial credit as necessary.**_
{% endtab %}
{% endtabs %}

### B 3: Backtracking

{% tabs %}
{% tab title="Question" %}
#### 10 points

For the purposes of this question we define a Top Left Knight's Path to be a sequence of jumps taken by a single knight piece, starting at the top left corner of a R by C board, which visits each square exactly once. The knight may end on any square on the board. Recall that the way a knight jumps is by either moving 1 square left or right, followed by 2 squares up or down, OR by moving 2 squares left or right, followed by 1 square up or down. In this question you'll complete a recursive function that counts the total number of Top Left Knight's Paths for a particular R and C \(which will be constants in the code.\) Your code should use the constants R and C and should still work if the values of these constants were changed. Complete the recursive function below so that it correctly solves this task. Just fill out the blanks given to you in the recursive function.

```c
#include <stdio.h>
#include <stdlib.h>
#define R 6
#define C 6
#define NUMDIR 8
const int DR[] = {-2,-2,-1,-1,1,1,2,2};
const int DC[] = {-1,1,-2,2,-2,2,-1,1};

int main() {
  printf("There were %d Top Left Knight Paths.\n", countTours());
  return 0;
}

int countTours() {
  int used[R][C], i, j;

  for (i=0; i<R; i++)
    for (j=0; j<C; j++)
      used[i][j] = 0;

  return countToursRec(used, 0, 0, 0);
}

int countToursRec(int used[][C], int numMarked, int curR, int curC) {
  if (numMarked == __________________ )
    return ____;

  int i, res = 0;
  for (i=0; i<NUMDIR; i++) 
  {
    int nextR = _____________________________;
    int nextC = _____________________________;

    if (inbounds(nextR, nextC) && _____________________________________ )
    {
      used[nextR][nextC] = ____ ;
      res += countToursRec(used, _______________, ________ , ________ );
      used[nextR][nextC] = ____ ;
    }
  }
  return res;
}

int inbounds(int nextR, int nextC) {
  return nextR >= 0 && nextR < R && nextC >= 0 && nextC < C;
}
```
{% endtab %}

{% tab title="Solution" %}
```c
#include <stdio.h>
#include <stdlib.h>
#define R 6
#define C 6
#define NUMDIR 8
const int DR[] = {-2,-2,-1,-1,1,1,2,2};
const int DC[] = {-1,1,-2,2,-2,2,-1,1};

int main() {
  printf("There were %d Top Left Knight Paths.\n", countTours());
  return 0;
}

int countTours() {
  int used[R][C], i, j;

  for (i=0; i<R; i++)
    for (j=0; j<C; j++)
      used[i][j] = 0;

  return countToursRec(used, 0, 0, 0);
}

int countToursRec(int used[][C], int numMarked, int curR, int curC) {
  if (numMarked == R*C)
    return 1;

  int i, res = 0;
  for (i=0; i<NUMDIR; i++) 
  {
    int nextR = curR + DR[i];
    int nextC = curC + DC[i];

    if (inbounds(nextR, nextC) && !used[nextR][nextC] )
    {
      used[nextR][nextC] = 1 ;
      res += countToursRec(used, numMarked + 1, nextR , nextC );
      used[nextR][nextC] = 0 ;
    }
  }
  return res;
}

int inbounds(int nextR, int nextC) {
  return nextR >= 0 && nextR < R && nextC >= 0 && nextC < C;
}
```

_**Grading: 1 pt per slot, must be perfectly correct to earn the point.**_
{% endtab %}
{% endtabs %}

## PDF Files

{% file src="../.gitbook/assets/FE-May17.pdf" caption="Summer 2017 Exam" %}

{% file src="../.gitbook/assets/FE-May17-Sol.pdf" caption="Summer 2017 Exam Solutions" %}

{% file src="../.gitbook/assets/FE-May17-Info.pdf" caption="Summer 2017 Exam Statistics" %}

