# Workshop Generic Vectors - Easy

## Description
Hello everyone !

Today we will see how to create and use generic vectors in C.
For this first part, we'll implement simple vectors, but keep in mind that you can improve them every time!

To begin with, what is a vector?


# Part 1 - Introduction (Typed Vectors)

## Exercice 0 - Learning
Try to understand what is a vector basically, and it's differences with arrays or linked lists.

## Exercice 1 - Initialization
Create a **vector_int_t structure**, then a function that **initialize** and **return** a **new** vector_int_t.

Don't forget to also create the destroy function. Here are the prototypes:
```c
vector_int_t *vector_int_create(size_t capacity);
void vector_int_destroy(vector_int_t *vector);
```
<details>
  <summary> HINT </summary>

  > Vectors are similar to arrays, what informations do you really need to store?
</details>

## Exercice 2 - Data Management
Perfect, you can now initialize your int vectors! But... How to use it?

Create three functions: 
- Push an element to the end
- Remove an element at the end
- Get the x element
```c
? vector_int_pushback(vector_int_t *vector, int new_elem);
? vector_int_popback(vector_int_t *vector);
int vector_int_get_at(vector_int_t *vector, size_t index);
```

## Exercice 3 - Try your vector
Very good! Let's now check if your code is working fine :)

Try to execute this code, and check your output:
```c
int main(void)
{
    vector_int_t *my_vector = vector_int_create(5);

    vector_int_pushback(my_vector, 4);
    vector_int_pushback(my_vector, 2);
    vector_int_pushback(my_vector, -42);
    vector_int_popback(my_vector);
    vector_int_pushback(my_vector, 84);
    for (size_t i = 0; i < my_vector->nb_elems; i++)
        printf("- [%ld] = %d\n", i, vector_int_get_at(my_vector, i));
    vector_int_destroy(my_vector);
}
```
```
❯ ./vector_int 
- [0] = 4
- [1] = 2
- [2] = 84
```


# Part 2 - Improve your vectors (Generic Vectors)
Ok so now, you can use your int vectors, congratulations!

But... How can we improve them? 

It would be nice to be able to use this library to store any type of data, wouldn't it? :)

## Exercice 1 - Generic Initialization
You already created a **vector_int_t** structure, but let's now try to create a simple **vector_t** structure!

Here is the new constructor/destructor functions prototypes:
```c
vector_t *vector_create(size_t capacity, size_t size_elems);
void vector_destroy(vector_t *vector);
```
<details>
  <summary> HINT </summary>

  > How can we store any type of data in our array? Hmm... Check the parameters
</details>

## Exercice 2 - Generic Data Management
Let's now adapt our old data management functions for our new generic vectors!

Keep in mind : The goal is to create generic data encapsulation. Think about it.

Here is the new prototypes of the three functions:
```c
? vector_pushback(vector_t *vector, ? new_elem);
? vector_popback(vector_t *vector);
void *vector_get_at(vector_t const *vector, size_t index);
```
<details>
  <summary> HINT </summary>

  > Have you ever heard of `memcpy`?
</details>

## Exercice 3 - Try your generic vectors
Like as before, it's the moment to check if your functions works as expected!

Are you confident? Let's check that!

Try to execute this code, and check your output:
```c
int main(int ac, char const *const *av)
{
    vector_t *my_vector = vector_create(15, sizeof(char));
    char temp_char = ' ';

    for (int i = 0; av[1][i] != '\0'; i++)
        vector_pushback(my_vector, &av[1][i]);

    vector_pushback(my_vector, &temp_char);

    for (int i = 0; av[2][i] != '\0'; i++)
        vector_pushback(my_vector, &av[2][i]);

    temp_char = '\0';
    vector_pushback(my_vector, &temp_char);

    printf("result:\n\n%s\n", my_vector->data);
    vector_destroy(my_vector);
}
```
```
❯ ./vector "Hello" "World!" | cat -e 
result:$
$
Hello World!$
```

# Part 3 - Almost finished! (Dynamically Allocated)
Congratulations, you've successfully created generic vectors applicable in all situations! But, hold on... It seems we're missing something.

What happens if you try to push back more elements than the capacity allows? Let's address this.

## Exercise 1 - Dynamic Allocation
Enhance the `vector_pushback` function to dynamically resize the vector's maximum capacity if it's exceeded.

Here's the updated function prototype:
```c
? vector_pushback(vector_t **vector, ? new_elem);
```

## Exercice 2 - Try your dynamic vectors
Again, let's check your new vectors!

```c
int main(void)
{
    vector_t *my_vector = vector_create(5, sizeof(int));
    int temp_int = 10;

    for (int i = 0; i < 10; i++) {
        temp_int += i;
        vector_pushback(&my_vector, &temp_int);
    }

    for (size_t i = 0; i < my_vector->nb_elems; i++)
        printf("- [%ld] = %d\n", i, (?)vector_get_at(my_vector, i)));
    vector_destroy(my_vector);
}
```
*Replace the `(?)` with the correct casting*
```
❯ ./vector_int
- [0] = 10
- [1] = 11
- [2] = 13
- [3] = 16
- [4] = 20
- [5] = 25
- [6] = 31
- [7] = 38
- [8] = 46
- [9] = 55
```

## Part 4 - Go further
You have now seen the basics of vectors in C.

Let’s try something fun! You currently need to keep your structure everywhere, it's annoying...
Try adapting your generic vectors until they work with this main:
```c
#include <unistd.h>

void part4(void)
{
    char *vector = vector_create(1, sizeof(char));

    vector_npushback(&vector, "Yhfwruv#duh#wkh#ehvw#gdwd#vwrudjh#lq#F$#=G", 42);
    const size_t length = vector_getlength(vector);
    for (size_t i = 0; i < length; i++)
        vector[i] -= 3;
    write(STDOUT_FILENO, vector, length);
    write(STDOUT_FILENO, "\n", 1);
    vector_destroy(vector);
}

int main(const int ac, char *const *av)
{
    part4();
}
```
```
❯ ./final_vectors 
Vectors are the best data storage in C! :D
```
