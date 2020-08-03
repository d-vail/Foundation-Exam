# Spring 2018

## Data Structures

### A 1: Dynamic Memory Management in C

{% tabs %}
{% tab title="Question" %}
#### 10 points

The struct, `dataTOD`, shown below, is used to collect data from different devices connected to the
CPU. Every time the data is updated a new buffer containing the structure’s data is created and
populated.

```c
typedef struct dataTOD
{
  int seconds;      // seconds since midnight
  double data;      // data sample
  char * dataName;  // data name (optional)
} dataTOD;
```

**(a)** (8 pts) Write the code necessary to create and initialize the members of `dataTOD` in a function named `init_dataTOD` that returns a pointer to the newly created buffer. Return NULL in the event a buffer cannot be created. Otherwise, set the seconds and data values according to the corresponding input parameters to `init_dataTOD`, dynamically allocate the proper space for dataName and then copy the contents of name into it (not a pointer copy) and a return a pointer to the newly created struct.

```c
dataTOD * init_dataTOD(int sec, double val, char* name)
{
  // your code
}
```

**(b)** (2 pts) Complete the function below so that it frees all the dynamically allocated memory pointed to by its formal parameter zapThis. You may assume that the pointer itself is pointing to a valid struct and its dataName pointer is pointing to a dynamically allocated character array.

```c
void free_dataTOD(dataTOD *zapThis)
{
  // your code
}
```

{% endtab %}

{% tab title="Solution" %}

**(a)**

```c
dataTOD * init_dataTOD(int sec, double val, char* name)
{
  dataTOD * tDta = malloc(sizeof(dataTOD));

  if (tDta == NULL)
    return NULL;

  tDta->seconds = sec;
  tDta->data = val;
  tDta->dataName = malloc((strlen(name)+1)*sizeof(char));
  strcpy(tDta->dataName, name);
  return tDta;
}
```

**_Grading: 1 point for each line shown above. Assign partial if necessary but assign a whole number of points._**

**(b)** (2 pts) Complete the function below so that it frees all the dynamically allocated memory pointed to by its formal parameter zapThis. You may assume that the pointer itself is pointing to a valid struct and its dataName pointer is pointing to a dynamically allocated character array.

```c
void free_dataTOD(dataTOD *zapThis)
{
  free(zapThis->dataName);
  free(zapThis);  
}
```

**_Grading: 1 pt each line_**

{% endtab %}
{% endtabs %}

### A 2: Linked Lists

{% tabs %}
{% tab title="Question" %}
#### 5 points

Given the linked list structure named node, defined in lines 1 through 4, and the function named `eFunction` defined in lines 6 through 14, answer the questions below.

```c
typedef struct node
{
  int data;
  struct node * next;
} node;

node* eFunction(node* aNode)
{
  if(aNode == NULL) return NULL;
  if(aNode->next == NULL) return aNode;

  node* rest = eFunction(aNode->next);
  aNode->next->next = aNode;
  aNode->next = NULL;
  return rest;
}
```

**(a)** (1 pt) Is this function recursive? (Circle the correct answer.) YES   NO

**(b)** (2 pts) What does the function eFunction do, in general to the list pointed to by its formal parameter, aNode?

**(c)** (2 pts) What important task does line 12 perform?

{% endtab %}

{% tab title="Solution" %}

**(a)** YES

**_Grading: 1 pt_**

**(b)** This function reverses the list originally pointed to by aNode and returns a pointer to the new
front of the list.

**_Grading: 1 pt for reverse, 1 pt for return pointer to reversed list._**

**(c)** The last node in a linked list must have its next pointer point to NULL. That is how most linked list functions detect the end of the list. Line 12 does this since aNode ends up point to the last node in the list. After the reversal is complete, it's necessary to make sure that the next pointer of the last node in the resulting list is pointing to NULL because before line 12 it's not. (It's pointing to the second node in the original list, which is the last node in the list pointed to by rest.)

**_Grading: Most of this detail is unnecessary. Full credit for noting that the line sets the last node's next pointer of the resulting list to NULL. Give partial as needed._**

{% endtab %}
{% endtabs %}

### A 3: Stacks

{% tabs %}
{% tab title="Question" %}
#### 10 points

Consider evaluating a postfix expression that only contained positive integer
operands and the addition and subtraction operators. (Thus, there are no issues with order of operations!)
Write a function that evalulates such an expression. To make this question easier, assume that your
function takes an array of integers, expr, storing the expression and the length of that array, len. In
the array of integers, all positive integers are operands while -1 represents an addition sign and -2
represents a subtraction sign. Assume that you have a stack at your disposal with the following function
signatures. Furthermore, assume that the input expression is a valid postfix expression, so you don't have
to ever check if you are attempting to pop an empty stack. Complete the evaluate function below.

```c
void init(stack* s);            // Initializes the stack pointed to by s.
void push(stack* s, int item);  // Pushes item onto the stack pointed to by s.
int pop(stack* s);              // Pops and returns the top value from the stack
                                // pointed to by s.

int eval(int* expr, int len)
{
  stack s;
  init(&s);
  int i;
}
```
{% endtab %}

{% tab title="Solution" %}

```c
void init(stack* s);            // Initializes the stack pointed to by s.
void push(stack* s, int item);  // Pushes item onto the stack pointed to by s.
int pop(stack* s);              // Pops and returns the top value from the stack
                                // pointed to by s.

int eval(int* expr, int len)
{
  stack s;
  init(&s);
  int i;

  for (i=0; i<len; i++)     // 1 pt
  {
    if (expr[i] > 0)        // 1 pt
      push(&s, expr[i]);    // 1 pt
    else
    {
      int op2 = pop(&s);    // 1 pt
      int op1 = pop(&s);    // 1 pt
      
      if (expr[i] == -1)    // 1 pt
        push(&s, op1+op2);  // 1 pt
      else
        push(&s, op1-op2);  // 2 pts (1 pt for order)
    }
  } 

  return pop(&s);           // 1 pt
}
```

{% endtab %}
{% endtabs %}

### B 1: Binary Search Trees

{% tabs %}
{% tab title="Question" %}
#### 10 points
{% endtab %}

{% tab title="Solution" %}

{% endtab %}
{% endtabs %}

### B 2: Binary Heaps

{% tabs %}
{% tab title="Question" %}
#### 5 points
{% endtab %}

{% tab title="Solution" %}

{% endtab %}
{% endtabs %}

### B 3: AVL Trees

{% tabs %}
{% tab title="Question" %}
#### 10 points
{% endtab %}

{% tab title="Solution" %}

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
#### 10 points
{% endtab %}

{% tab title="Solution" %}

{% endtab %}
{% endtabs %}

### B 2: Sorting

{% tabs %}
{% tab title="Question" %}
#### 5 points
{% endtab %}

{% tab title="Solution" %}

{% endtab %}
{% endtabs %}

### B 3: Backtracking

{% tabs %}
{% tab title="Question" %}
#### 10 points
{% endtab %}

{% tab title="Solution" %}

{% endtab %}
{% endtabs %}

## PDF Files

{% file src="../.gitbook/assets/FE-Jan18.pdf" caption="Spring 2018 Exam" %}

{% file src="../.gitbook/assets/FE-Jan18-Sol.pdf" caption="Spring 2018 Exam Solutions" %}

{% file src="../.gitbook/assets/FE-Jan18-Info.pdf" caption="Spring 2018 Exam Statistics" %}

