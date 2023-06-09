# Functions and Flow

## Functions

Functions are operations we can perform on our various data structures to get some result. We typically like to make functions modular so they perform one specific task and not whole pipelines. Here is the general format for a function:

```R
functionName <- function(x){
  result <- operation(x)
  return(result)
}
```

So here we see that we assign some operation to a name, here it we just call it ```functionName```. Then the function takes an input, ```x```. Inside the function our result is obtained by doing some operation on our input. Finally we then use ```return()``` to return that result. Let's try making a function that will square the input:

```R
squareInput <- function(x){
  result <- x * x
  return(result)
}

squareInput(5)
```

!!! info "output"

    ```
    25
    ```

!!! note

    Without `return()` in the function, R will return the last variable in the function. So you can leave out `return()`, however it is best to specify what you are returning for clarity.
   
## Additional Arguements

Functions can have as little or as many arguements as needed. So in the example above we used one arguement, `x`. Let's try using more than one arguement:

```R
item_in_vector_func <- function(vector, item){
  item_in_vector <- item %in% vector
  return(item_in_vector)
}
item_in_vector_func(vector = c(1,2,3), item=2)
```

!!! info "output"

    ```
    [1] TRUE
    ```

Here we used a new operator, `%in%`, which does exactly what it sounds like - it checks whether some value is in another set of values. We should also note, you can specify values in functions:

```R
item_in_vector_func <- function(vector=1:10, item=NULL){
  item_in_vector <- item %in% vector
  return(item_in_vector)
}
```

Here we specify default values for the `item_in_vector()` function. Unless we change them when we call the function, these values will remain. So when you call a function from a package it's a good idea to check what the default values are.

## Control Flow

Now what if we don't want to perform an operation until a condition is met? For this we need an if/else statement:

```R
x <- 3

if (x == 10){
  print("x equals 10")
} else{
  print("x does not equal 10")
}
```

!!! info "output"

    ```
    [1] "x does not equal 10"
    ```

Now what if we wanted to include multiple conditions?

```R
x <- 3

if (x == 10){
  print("x equals 10")
} else if (x > 2){
  print("x is greater than 2")
} else if (x > 1){
  print("x is greater than 1")
} else{
  print("x does not equal  10")
}
```

!!! info "output"

    ```
    [1] "x is greater than 2"
    ```

Here notice that, x meets 2 of the conditions:

- `x > 2`
- `x > 1`

However, we note that the conditional statement is broken when `x` meets the first condition in the order above. 

## Loops

Operations can be repeated with a `for` loop:

```R
for (i in 1:5){
  print(i*i)
}
```

!!! info "output"

    ```
    [1] 1
    [1] 4
    [1] 9
    [1] 16
    [1] 25
    ```
    
Here we see that `i` is a substitute for some value in the sequence provided - in this case `1,2,3,4,5`. We can also nest a loop inside a loop like so:

```R
for (i in 1:3){
  for(j in 3:5){
    print(i*j)
  }
}
```

!!! info "output"

    ```
    [1] 3
    [1] 4
    [1] 5
    [1] 6
    [1] 8
    [1] 10
    [1] 9
    [1] 12
    [1] 15
    ```

You'll notice that for each value i was multiplied by each value j. So:


!!! example "Explanation"

    ```
    1*3
    1*4
    1*5
    2*3
    2*5
    2*6
    3*3
    3*4
    3*5
    ```
## Avoiding Loops

While we can use a loop to perform repetitive operations, R also offers a suite of `apply()` functions to apply some operation to different data structures in a more concise manner. For instance consider the following loop:

```R
for (i in 1:5){
  print(log(i))
}
```

!!! info "output"

    ```
    [1] 0
    [1] 0.6931472
    [1] 1.098612
    [1] 1.386294
    [1] 1.609438
    ```
   
We can replace this loop with the `sapply()` function which applies some operation to a vector with the following one line of code:

```R
sapply(1:5,log)
```

!!! info "output"

    ```
    [1] 0.0000000 0.6931472 1.0986123 1.3862944 1.6094379
    ```
    
Note, that we don't print the statement as the output is automatically printed to the console. If we wanted to perform an operation on a list we could use the `lapply()` function:

```R
lapply(list("a","b","c"),toupper)
```

!!! info "output"

    ```
    [[1]]
    [1] "A"
    
    [[2]]
    [1] "B"
    
    [[3]]
    [1] "C"
    ```
    
The `apply` familiy of functions can also be applied to data frames. Data frames have two axes, rows and columns. When using `apply()` on a data frame you specify `1` for rows and `2` for columns. Here is an example for calculating sums:

```R
df=data.frame(a=1:3,b=1:3,c=1:3,d=1:3)
df
```

!!! info "output"

    ```
      a b c d
    1 1 1 1 1
    2 2 2 2 2
    3 3 3 3 3
    ```

```R
# applying sums to rows
apply(df,1,sum)
```

!!! info "output"

    ```
    [1]  4  8 12
    ```
    
```R
# applying sums to rows
apply(df,2,sum)
```

!!! info "output"

    ```
    a b c d 
    6 6 6 6 
    ```

## References

1. [R for Reproducible Scientific Analysis](https://swcarpentry.github.io/r-novice-gapminder/)
2. [Base R Cheat Sheet](https://iqss.github.io/dss-workshops/R/Rintro/base-r-cheat-sheet.pdf)
