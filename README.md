# 0x1B. C - Sorting algorithms & Big O
  ## Sorting Algorithms

  1. `0-bubble_sort.c, 0-O` Function that sorts an array of integers in ascending order using the Bubble sort algorithm
  ```
      alex@/tmp/sort$ cat 0-main.c 
    #include <stdio.h>
    #include <stdlib.h>
    #include "sort.h"

    /**
    * main - Entry point
    *
    * Return: Always 0
    */
    int main(void)
    {
        int array[] = {19, 48, 99, 71, 13, 52, 96, 73, 86, 7};
        size_t n = sizeof(array) / sizeof(array[0]);

        print_array(array, n);
        printf("\n");
        bubble_sort(array, n);
        printf("\n");
        print_array(array, n);
        return (0);
    }
    alex@/tmp/sort$ gcc -Wall -Wextra -Werror -pedantic  -std=gnu89 0-bubble_sort.c 0-main.c print_array.c -o bubble
    alex@/tmp/sort$ ./bubble
    19, 48, 99, 71, 13, 52, 96, 73, 86, 7

    19, 48, 71, 99, 13, 52, 96, 73, 86, 7
    19, 48, 71, 13, 99, 52, 96, 73, 86, 7
    19, 48, 71, 13, 52, 99, 96, 73, 86, 7
    19, 48, 71, 13, 52, 96, 99, 73, 86, 7
    19, 48, 71, 13, 52, 96, 73, 99, 86, 7
    19, 48, 71, 13, 52, 96, 73, 86, 99, 7
    19, 48, 71, 13, 52, 96, 73, 86, 7, 99
    19, 48, 13, 71, 52, 96, 73, 86, 7, 99
    19, 48, 13, 52, 71, 96, 73, 86, 7, 99
    19, 48, 13, 52, 71, 73, 96, 86, 7, 99
    19, 48, 13, 52, 71, 73, 86, 96, 7, 99
    19, 48, 13, 52, 71, 73, 86, 7, 96, 99
    19, 13, 48, 52, 71, 73, 86, 7, 96, 99
    19, 13, 48, 52, 71, 73, 7, 86, 96, 99
    13, 19, 48, 52, 71, 73, 7, 86, 96, 99
    13, 19, 48, 52, 71, 7, 73, 86, 96, 99
    13, 19, 48, 52, 7, 71, 73, 86, 96, 99
    13, 19, 48, 7, 52, 71, 73, 86, 96, 99
    13, 19, 7, 48, 52, 71, 73, 86, 96, 99
    13, 7, 19, 48, 52, 71, 73, 86, 96, 99
    7, 13, 19, 48, 52, 71, 73, 86, 96, 99

    7, 13, 19, 48, 52, 71, 73, 86, 96, 99
    alex@/tmp/sort$ 
  ```

  2. `1-insertion_sort_list.c, 1-O` Function that sorts a doubly linked list of integers in ascending order using the Insertion sort algorithm
```
    alex@/tmp/sort$ cat 1-main.c
    #include <stdio.h>
    #include <stdlib.h>
    #include "sort.h"

    /**
    * create_listint - Creates a doubly linked list from an array of integers
    *
    * @array: Array to convert to a doubly linked list
    * @size: Size of the array
    *
    * Return: Pointer to the first element of the created list. NULL on failure
    */
    listint_t *create_listint(const int *array, size_t size)
    {
        listint_t *list;
        listint_t *node;
        int *tmp;

        list = NULL;
        while (size--)
        {
            node = malloc(sizeof(*node));
            if (!node)
                return (NULL);
            tmp = (int *)&node->n;
            *tmp = array[size];
            node->next = list;
            node->prev = NULL;
            list = node;
            if (list->next)
                list->next->prev = list;
        }
        return (list);
    }

    /**
    * main - Entry point
    *
    * Return: Always 0
    */
    int main(void)
    {
        listint_t *list;
        int array[] = {19, 48, 99, 71, 13, 52, 96, 73, 86, 7};
        size_t n = sizeof(array) / sizeof(array[0]);

        list = create_listint(array, n);
        if (!list)
            return (1);
        print_list(list);
        printf("\n");
        insertion_sort_list(&list);
        printf("\n");
        print_list(list);
        return (0);
    }
    alex@/tmp/sort$ gcc -Wall -Wextra -Werror -pedantic  -std=gnu89 1-main.c 1-insertion_sort_list.c print_list.c -o insertion
    alex@/tmp/sort$ ./insertion
    19, 48, 99, 71, 13, 52, 96, 73, 86, 7

    19, 48, 71, 99, 13, 52, 96, 73, 86, 7
    19, 48, 71, 13, 99, 52, 96, 73, 86, 7
    19, 48, 13, 71, 99, 52, 96, 73, 86, 7
    19, 13, 48, 71, 99, 52, 96, 73, 86, 7
    13, 19, 48, 71, 99, 52, 96, 73, 86, 7
    13, 19, 48, 71, 52, 99, 96, 73, 86, 7
    13, 19, 48, 52, 71, 99, 96, 73, 86, 7
    13, 19, 48, 52, 71, 96, 99, 73, 86, 7
    13, 19, 48, 52, 71, 96, 73, 99, 86, 7
    13, 19, 48, 52, 71, 73, 96, 99, 86, 7
    13, 19, 48, 52, 71, 73, 96, 86, 99, 7
    13, 19, 48, 52, 71, 73, 86, 96, 99, 7
    13, 19, 48, 52, 71, 73, 86, 96, 7, 99
    13, 19, 48, 52, 71, 73, 86, 7, 96, 99
    13, 19, 48, 52, 71, 73, 7, 86, 96, 99
    13, 19, 48, 52, 71, 7, 73, 86, 96, 99
    13, 19, 48, 52, 7, 71, 73, 86, 96, 99
    13, 19, 48, 7, 52, 71, 73, 86, 96, 99
    13, 19, 7, 48, 52, 71, 73, 86, 96, 99
    13, 7, 19, 48, 52, 71, 73, 86, 96, 99
    7, 13, 19, 48, 52, 71, 73, 86, 96, 99

    7, 13, 19, 48, 52, 71, 73, 86, 96, 99
    alex@/tmp/sort$
  ```
  3. `3-quick_sort.c, 3-O` Because we want to protect attributes of our class. With a setter, you are able to validate what a developer is trying to assign to a variable. So after, in your class you can “trust” these attributes.
  ```
      alex@/tmp/sort$ cat 3-main.c
    #include <stdio.h>
    #include <stdlib.h>
    #include "sort.h"

    /**
    * main - Entry point
    *
    * Return: Always 0
    */
    int main(void)
    {
        int array[] = {19, 48, 99, 71, 13, 52, 96, 73, 86, 7};
        size_t n = sizeof(array) / sizeof(array[0]);

        print_array(array, n);
        printf("\n");
        quick_sort(array, n);
        printf("\n");
        print_array(array, n);
        return (0);
    }
    alex@/tmp/sort$ gcc -Wall -Wextra -Werror -pedantic  -std=gnu89 3-main.c 3-quick_sort.c print_array.c -o quick
    alex@/tmp/sort$ ./quick
    19, 48, 99, 71, 13, 52, 96, 73, 86, 7

    7, 48, 99, 71, 13, 52, 96, 73, 86, 19
    7, 13, 99, 71, 48, 52, 96, 73, 86, 19
    7, 13, 19, 71, 48, 52, 96, 73, 86, 99
    7, 13, 19, 71, 48, 52, 73, 96, 86, 99
    7, 13, 19, 71, 48, 52, 73, 86, 96, 99
    7, 13, 19, 48, 71, 52, 73, 86, 96, 99
    7, 13, 19, 48, 52, 71, 73, 86, 96, 99

    7, 13, 19, 48, 52, 71, 73, 86, 96, 99
    alex@/tmp/sort$
  ```
> # Descriptions

    - Header `sort.h`
    - Data Struct 
    ``` 
        typedef struct listint_s
    {
      const int n;
      struct listint_s *prev;
      struct listint_s *next;
    } listint_t;
    ```
    - Tests in the `tests/` directory
    - `print_array.c`is a C function that prints an array of integers.
    - `print_list.c`: is a c function that prints a listint_t doubly-linked list.
    
> # Prototype

  - `1-insertion_sort_list.c`	void insertion_sort_list(listint_t **list);

  - `2-selection-sort.c`	void selection_sort(int *array, size_t size);

  - `3-quick_sort.c`	void quick_sort(int *array, size_t size);

