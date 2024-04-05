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
vector_int_t *vector_int_create(size_t initial_capacity);
void vector_int_destroy(vector_int_t *vector);
```
<details>
  <summary> HINT </summary>

  > Vectors are similar to arrays, what informations do you really need to store?
</details>

## Exercice 2 - Usage
Perfect, you can now initialize your int vectors! But... How to use it?

Create three functions: 
- Push an element to the end
- Remove an element at the end
- Get the x element
```c
? vector_int_pushback(vector_int_t *vector, int new_elem);
? vector_int_removeback(vector_int_t *vector);
int *vector_int_get_at(vector_int_t *vector, size_t index);
```

## Exercice 3 - Try your vector
Very good! Let's now check if your code is working fine :)

Try to execute this code, and check your output :
```c
int main(void)
{
    vector_int_t *my_vector = vector_int_create(5);

    vector_int_pushback(my_vector, 4);
    vector_int_pushback(my_vector, 2);
    vector_int_pushback(my_vector, -42);
    vector_int_removeback(my_vector);
    vector_int_pushback(my_vector, 84);
    for (size_t i = 0; i < my_vector->nb_elems; i++)
        printf("- [%ld] = %d\n", i, *vector_int_get_at(my_vector, i));
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

## Exercice 0 - Generic Initialization
You already created a **vector_int_t** structure, but let's now try to create a simple **vector_t** structure!

Here is the new constructor/destructor functions prototypes:
```c
vector_t *vector_create(size_t initial_capacity, size_t size_elems);
void vector_destroy(vector_t *vector);
```
<details>
  <summary> HINT </summary>

  > How can we store any type of data in our array? Hmm... Check the parameters
</details>
