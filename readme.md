## Rusty

## Table of Contents

- [Installation](#installation-of-rust)
- [Tools](#tools)
- [Setup](#setup)
- [References](#references)
- [Folder Structure](#folder-structure)
- [Hello World](#hello-world)
- [Data Types](#data-types)
- [Examples](#example)
- [Functions](#functions)
- [Ownership](#ownership)
- [Borrowing](#borrowing)
- [Struct](#struct)
- [Enum](#enum)
- [Option](#option)
- [Result](#result)
- [Loops](#loops)
- [Conditional Statements](#conditional-statements)

### Installation of Rust

1. Windows
   - Download the installer from the [official website](https://www.rust-lang.org/tools/install)
   - Run the installer
   - Open a new terminal and run `rustc --version` to check if the installation was successful
2. Linux
   ```bash
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
   ```
3. MacOS
   ```bash
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
   ```

### Tools

#### Rustup

Rustup is the recommended tool to install Rust. It manages Rust versions and associated tools.

#### Rustc

Rustc is the Rust compiler. It is used to compile Rust programs.

#### Cargo

Cargo is the Rust package manager. It is used to compile, test, and run Rust programs. It also manages dependencies.

### setup

1. Create a new project
   ```bash
   cargo new project_name
   ```
2. Change directory to the project
   ```bash
   cd project_name
   ```
3. Build the project
   ```bash
   cargo build
   ```
4. Run the project
   ```bash
   cargo run
   ```
5. Test the project
   ```bash
   cargo test
   ```
6. Check the project
   ```bash
   cargo check
   ```

### References

- [Rust Programming Language](https://www.rust-lang.org/)
- [Rustup](https://rustup.rs/)
- [Cargo](https://doc.rust-lang.org/cargo/)
- [Rust by Example](https://doc.rust-lang.org/rust-by-example/)

### Folder Structure

- `src`: Contains the source code of the project
- `target`: Contains the compiled code of the project
  - `debug`: Contains the debug build
  - `release`: Contains the release build
- `Cargo.toml`: Contains metadata about the project, like `package.json` in Node.js
- `Cargo.lock`: Contains information about the dependencies, like `package-lock.json` in Node.js

### Hello World

```rust
fn main() {  // main is the entry point of the program
    println!("Hello, world!");
}
```

### Data Types

1. Integer
   - `i8`, `i16`, `i32`, `i64`, `i128`, `isize` // Signed
   - `u8`, `u16`, `u32`, `u64`, `u128`, `usize` // Unsigned
2. Float
   - `f32`, `f64`
3. Boolean
   - `bool`
4. Character
   - `char`
5. String
   - `&str`, `String`
6. Tuple
   - `(T1, T2, T3, ..., Tn)`
7. Array
   - `[T; n]`
8. Slice
   - `&[T]`
9. Struct
   - `struct Name { field1: T1, field2: T2, ..., fieldn: Tn }`
10. Enum
    - `enum Name { Variant1, Variant2, ..., Variantn }`
11. Option
    - `Option<T>`
12. Result
    - `Result<T, E>`
13. Function
    - `fn name(arg1: T1, arg2: T2, ..., argn: Tn) -> T { ... }`

#### Example

```rust
fn main() {
    let x: i32 = 10;  // Integer
    let y: f64 = 10.5;  // Float
    let z: bool = true;  // Boolean
    let c: char = 'A';   // Character
    let s: &str = "Hello, world!";  // String
    let t: (i32, f64, bool) = (10, 10.5, true);  // Tuple
    let a: [i32; 3] = [10, 20, 30];  // Array
    let sl: &[i32] = &a;  // Slice
    let st: Name = Name { field1: 10, field2: 10.5, field3: true };  // Struct
    let e: Option<i32> = Some(10);  // Enum
    let r: Result<i32, &str> = Ok(10);  // Result
    let f: fn(i32, f64, bool) -> i32 = name;  // Function
}
```

```rust
fn main() {
  let num: u8 = 255;
  // Here u8 means unsigned--> only +ve; 8-bit --> 0 to 255 :(2^n - 1)
  // If we try to assign 256, it will throw an error
  println!("The number is: {}", num);
}
```

#### Mutable and Immutable Variables

Mutable variables can be changed, whereas immutable variables cannot be changed.

```rust
fn main() {
    let x = 10;  // Immutable variable
    // x = 20;  // Error
    let mut y = 20;  // Mutable variable
    y = 30;
    println!("x: {}, y: {}", x, y);
}
```

### String & string_literal(&str)

- `String` is a growable, heap-allocated data structure.
- `&str` is a fixed-size, immutable view into a string slice.

```rust
fn main() {
    let mut s1 = String::from("Hello, world!!!");  // String
    s1.push_str(" What's Up ?"); // mutable
    let s2: &str = "Hello, world!";  // &str
    s2 = "Adii";
    println!("s1: {}, s2: {}", s1, s2);
}
```

### Tuple

A tuple is a collection of values of different types.

```rust
fn main() {
    let emp_info: (&str, u8, bool) = ("Adii", 20, true);
    let _emp_name = emp_info.0;   // "_" prifix if unused
    let _emp_age = emp_info.1;
    let _emp_hired = emp_info.2;
    // Distructuring
    let (employee_name, employee_age, employee_hired) = emp_info;
    println!("Employee Name: {}\nEmployee Age: {}\nEmployee Hired: {}", employee_name, employee_age, employee_hired);
}
```

### Functions

Functions are a set of statements grouped together to perform a specific task.

```rust
fn main() {
    let n1 = 52;
    let n2 = 29;
    let result = add_num(n1, n2);
    println!("Sum of {} and {} = {}", n1, n2, result);
}

fn add_num(num1: u16, num2: u16) -> u16 {
    return num1 + num2;
}
```

### Ownership

##### Why ownership?

In C and C++, we have to manually manage memory allocation and deallocation using `calloc()`, `malloc()`, `relloc()`, `free()`. This can lead to memory leaks, dangling pointers, and double frees.

```C
#include <stdio.h>
#include <stdlib.h>
int main() {
   // Allocate memory
   int *ptr = (int *)malloc(sizeof(int));
   *ptr = 10;
   free(ptr);
   printf("%d\n", *ptr);  // Dangling pointer
   // This Dangling pointer will still point to the memory location
   free(ptr); // Double free
   // This will cause an error
   return 0;
}
```

In Python, Java, and JavaScript, the garbage collector automatically manages memory allocation and deallocation. This can lead to performance issues beacuse the garbage collector runs in the background.

```python
import gc
class Test:
    def __init__(self):
        print("Object created")
    def __del__(self):
        print("Object deleted")
t = Test()
del t
gc.collect()  # Explicitly call the garbage collector
```

Rust uses a concept called ownership to manage memory allocation and deallocation. Ownership is a set of rules that the compiler checks at compile time.

##### Heap and Stack memory

- Stack: Fixed size memory (eg. - `&str`)
  1.  Size of memory to be allocated is known at compile time.
  2.  Memory is allocated and deallocated are Faster.
- Heap: Dynamic size memory (eg. - `String`)
  1.  Size of memory to be allocated is known at runtime.
  2.  Memory is allocated and deallocated are slower.

##### Ownership Rules

1. Each value in Rust has a variable that's called its owner.
2. There can only be one owner at a time.
3. When the owner goes out of scope, the value will be dropped.

```rust
fn main() {
    let s1 = String::from("Hello, world!");  // s1 is the owner of the string
    let s2 = s1;  // s2 is the owner of the string
    // println!("{}", s1);  // Error
    println!("{}", s2);
}
```

##### Clone

To create a deep copy of the data on the heap, we can use the `clone()` method.

```rust
fn main() {
    let s1 = String::from("Hello, world!");
    let mut s2 = s1.clone();  // but this is an expensive operation beacuse it will create new memory
    println!("s1: {}, s2: {}", s1, s2); // output: s1: Hello, world!, s2: Hello, world!
    s2 = "Adii".to_string();
    println!("s1: {}, s2: {}", s1, s2); // output: s1: Hello, world!, s2: Adii
}

```

##### Copy

For stack-only data, the data is copied instead of moved.

```rust
fn main() {
    let x = 10;
    let y = x;
    println!("x: {}, y: {}", x, y);
}
```

##### Ownership and Functions

when we pass a heap memory variable (pointer) to a function, the ownership of the variable is moved to the function.

> Note: This only happens with heap memory variables.

```rust
fn main() {
    let s1 = String::from("Hello, world!");
    let s2 = take_ownership(s1);  // ownership of s1 is moved to the function take_ownership variable s
    // println!("{}", s1);  // Error
    println!("{}", s2); // take_ownership will return the ownership of s to s2
}

fn take_ownership(s: String) -> String {
    println!("{}", s);
    return s; // when the function returns, the ownership of s is moved to the calling function
}
```

Some Other Examples:

```rust
fn main() {
    let s1 = String::from("Hello, world!");
    let s2 = take_ownership(s1);
    println!("{}", s2);
    let x = 10;
    let y = add_num(x); // x is copied [ copy trait is implemented ]
    println!("x: {}, y: {}", x, y);
}

fn take_ownership(s: String) -> String {
    println!("{}", s);
    return s;
}

fn add_num(num: u16) -> u16 {
    return num + 10;
}
```

###### Problem with ownership transfer

Sometimes we need to use the variable after passing it to a function.

```rust
fn main() {
   let s1 = String::from("Hello, world!");
   let len = get_length(s1); // ownership gets transferred to the function
   println!("Length of the string '{}' is {}", s1, len); // Error
   // s1 is not available here because ownership is transferred to the function
}

fn get_length(s: String) -> usize {
    return s.len();
}
```

to solve this problem, their are three ways:

1. Using `Tuple` // not recommended
2. Using `clone()` // expensive operation
3. Using `Reference` // recommended

```rust
fn main() {
   let s1 = String::from("Hello, world!");
   let (s2, len) = get_length(s1); // Destructuring the tuple
   println!("Length of the string '{}' is {}", s2, len);
}

fn get_length(s: String) -> (String, usize) {
   let len = s.len();
   return (s,len); // Returning tuple
}
```

```rust
fn main() {
   let s1 = String::from("Hello, world!");
   let len = get_length(s1.clone()); // Cloning the string
   // But this is an expensive operation because it will create new memory
   println!("Length of the string '{}' is {}", s1, s2);
}

fn get_length(s: String) -> usize {
   return s.len();
}
```

##### Borrowing

Borrowing is a way to pass a reference, instead of transferring ownership.

```rust
fn main() {
   let s1 = String::from("Hello, world!");
   let len = get_length(&s1); // Passing reference
   //
   println!("Length of the string '{}' is {}", s1, len);
}

fn get_length(s: &String) -> usize {
   return s.len();
}
```

##### Mutable Reference

To modify the value of a reference, we need to pass a mutable reference.

```rust
fn main() {
   let mut s1 = String::from("Hello, world!");
   modify_string(&mut s1); // Passing mutable reference
   println!("Modified string: {}", s1);
}

fn modify_string(s: &mut String) {
   s.push_str(" What's Up?");
}
```

##### Rules of References

1. At any given time, you can have either one mutable reference or any number of immutable references.
2. References must always be valid.

```rust
fn main() {
    let mut s = String::from("Hello, world!");
    let r1 = &s;  // Immutable reference
    let r2 = &s;  // Immutable reference
    // let r3 = &mut s;  // Error
    println!("r1: {}, r2: {}", r1, r2);
}
```

```rust
fn main() {
    let mut x = 9;
    let r1 = &mut x;
    println!("r1: {}", r1);
    let r2 = &mut x;
    println!("r2: {}", r2);
    // println!("r1: {}\nr2 = {}", r1, r2); // Error
    // more than one mutable reference is not allowed at a time
}
```

#### Referencing and Derefencing

> Note: Don't get confused with pointer, reference and dereference.

- `&` is used to create a reference.
- `*` is used to dereference a reference.

```rust
fn main() {
    let x = 10;
    let r = &x;  // Creating a reference
    let y = *r;  // Dereferencing the reference
    println!("x: {}, y: {}", x, y);
}
```

##### Auto Derefencing

Rust automatically dereferences a reference when needed.
like in the below example, we are directly using the value of the reference.
Like when you are printing then rust automatically detect and directly print the value of x, But if you want to print the address or reference of x then you have to use `{:p}` to print the address of x.

```rust
fn main () {
    let x = 10;
    let y = &x; // Y is a reference to the value of x which is 10
    println!("x: {}, y: {}", x, y); // Here we are directly using the value of y instead of dereferencing it (*y)
    // If you want to see the address of x
    println!("Address of x: {:p}, Address of x: {:p}", &x, y);
}
```

```rust
fn main() {
    let st = String::from("Hello, world!");
    let len = get_length(&st);  // Passing reference
    println!("Length of the string '{}' is {}", st, len);
}

fn get_length(s: &String) -> usize {
    // return (*s).len(); // Dereferencing the reference
    return s.len(); // Auto dereferencing
}
```

But when not to use auto dereferencing. like in the below example, we are using the value of the reference. because we want to make changes in the value of x not in the address of x.

```rust
fn main() {
    let mut x = 10;
    x = x + 5;
    { // The mutable borrow starts here
        let y = &mut x;
        println!("Before change y: {}", *y);
        *y = *y + 10;  // Dereferencing the reference to modify the value of x
        println!("After change y: {}", *y);
    } // The mutable borrow ends here
    println!("After change - x: {}", x);
}
```

##### Reference vs Pointer

- A reference hold metadata about the reference, such as the type and lifetime and mutable or immutable.
- A pointer only holds the memory address.

```rust
fn main() {
    let x = 10;
    let r = &x;  // Reference
    let p = &x as *const i32;  // Pointer
    println!("r: {:p}, p: {:p}", r, p);
}
```

#### Dangling References

A dangling reference is a reference that points to an invalid memory location.

```rust
fn main() {
    let r = get_reference();
    println!("{}", r);
}

fn get_reference() -> &String {
    let s = String::from("Hello, world!");
    return &s;
}
```

#### Float, Boolean, Character

```rust
fn main() {
    let pi: f32 = 3.14;
    let g = 9.8; // by default f64
    println!("{}", pi);
    println!("{}", g);

    let me: bool = true;
    let you = false; // by default bool
    let us = me && you;
    println!("{}", me);
    println!("{}", you);
    println!("{}", us);

    let char: char = 'A';
    let emo = '😀'; // 4 bytes
    println!("{}", char);
    println!("{}", emo);
}
```

#### Array

An array is a fixed-size collection of elements of the same type.

```rust
fn main() {
    let _str_arr: [&str; 3] = ["Hello", "World", "!"];
    let mut arr: [i32; 5] = [1, 2, 3, 4, 5];
    println!("{:?}", arr); // [1,2,3,4,5]
    let _first = arr[0];
    arr[2] = 9;
    let len = arr.len();
    let mut i = 0;
    while i < len {
        println!("{}", arr[i]);
        i += 1;
    }
    for i in 0..=4 { // for(let i = 0; i <= 4; i++)
        println!("{}", arr[i]);
    }
    for i in 0..len { // for(let i = 0; i < len; i++))
        println!("{}", arr[i]);
    }
    for i in arr.iter() {
        println!("{}", i);
    }
    for i in &arr {
        println!("{}", i);
    }
    for i in arr.iter_mut() {
        *i += 1;
    }
    println!("{:?}", arr); // [2,3,4,5,6]
    let arr1;
    arr1 = [1, 2, 3, 4, 5];
    let arr3 = [3; 5]; // [3,3,3,3,3]
    println!("{:?}", arr3);
    let _arr5 = &arr1[1..4];   // [2,3,4]
    let _arr12 = &arr1[1..=4]; // [2,3,4,5]
    let _arr6 = &arr1[1..];    // [2,3,4,5]
    let _arr7 = &arr1[..4];    // [1,2,3,4]
    let _arr8 = &arr1[..];     // [1,2,3,4,5] // &arr1 == &arr1[..]
    let _arr9 = &arr; // [1,2,3,4,5]
    let arr10 = &arr as *const i32;
    println!("{:?}", arr10);
    let arr11 = &arr as *const [i32; 5];
    println!("{:?}", arr11);
}
```

```rust
fn main() {
    // let size = 5; // non-constant value // Error {E0435}
    const size: usize = 5; // Change the type of `size` to `usize`
    let arr: [i32; size] = [1, 2, 3, 4, 5];
    // [type, constant value]
    for i in 0..size {
        println!("{}", arr[i]);
    }
}
```

##### How to pass an Array to a function

1. By passing the array to a function

```rust
fn main() {
    let str_arr: [&str; 5] = ["Hello", "World", "from", "Rust", "Programming"];
    // Array is fixed size and assigned at compile time and Heap memory concept does not apply to it
    // So, we can pass it to a function without any issue and it will not transfer the ownership
    print_array(str_arr); // passing array to a function
    // By passing this way it will create an copy of this array and pass it to the function and it will be expensive task and it will not make any changes in the original array in the main function
    println!("\nmain fn arr = {:?}", str_arr);
}

fn print_array(mut arr: [&str; 5]) {
    arr[2] = "!,"; // making changes here will not affect the original array in main fn because it is passed by value which is a copy of the original array
    for &i in arr.iter() {
        print!("{} ", i);
    }
}
```

2. By passing the reference of the array to a function

```rust
fn main() {
    let mut str_arr: [&str; 5] = ["Hello", "World", "from", "Rust", "Programming"];
    print_array(& mut str_arr);
    println!("\nmain fn arr = {:?}", str_arr);
}

fn print_array(arr: & mut [&str; 5]) {
    arr[2] = "!,";
    for &i in arr.iter() {
        print!("{} ", i);
    }
}
```

#### Vector

A vector is a growable, heap-allocated collection of elements of the same type.

```rust
fn main() {
    // let mut vec: Vec<i32> = Vec::new();
    let mut vec = Vec::<i32>::new();
    vec.push(10);
    vec.push(20);
    vec.push(30);
    println!("{:?}", vec);
    let first = vec[0];
    let second = vec.get(1);
    println!("First: {}, Second: {:?}", first, second);
    for i in &vec {
        println!("{}", i);
    }
    for i in vec.iter() {
        println!("{}", i);
    }
    for i in vec.iter_mut() {
        *i += 1;
    }
    println!("{:?}", vec);
    let vec1 = vec![1, 2, 3, 4, 5];
    println!("{:?}", vec1);
    let vec2 = vec1.clone();
    println!("{:?}", vec2);
    let vec3 = &vec1[1..4];
    println!("{:?}", vec3);
}
```

##### How to pass a Vector to a function

1. By passing the vector to a function

```rust
fn main() {
    let vec: Vec<i32> = vec![1, 2, 3, 4, 5];
    // Its a Dyanamic size and Heap allocated memory
    print_vector(vec); // passing vector to a function
    // Here it will transfer the ownership of the vector to the function and it will not be available in the main function
    // println!("\nmain fn vec = {:?}", vec);  // Error
}

fn print_vector(mut vec: Vec<i32>) { // Now the ownership of the vector is transferred to this function
    vec[2] = 10; // Changing the value of the vector
    for &i in vec.iter() {
        print!("{} ", i);
    }
}
```

2. By passing the clone of the vector to a function

```rust
fn main() {
    let vec: Vec<i32> = vec![1, 2, 3, 4, 5];
    print_vector(vec.clone()); // passing clone of the vector to a function
    // its a expensive operation because it will create a new memory
    println!("\nmain fn vec = {:?}", vec);
}

fn print_vector(mut vec: Vec<i32>) {
    vec[2] = 10;
    for &i in vec.iter() {
        print!("{} ", i);
    }
}
```

3. By passing the reference of the vector to a function

```rust
fn main() {
    let mut vec: Vec<i32> = vec![1, 2, 3, 4, 5];
    print_vector(&mut vec);
    println!("\n{:?}", vec);
    let size: usize = vec.capacity(); // Getting the capacity of the vector
    // Capacity is the number of elements that the vector can hold without reallocation
    println!("Capacity of the vector: {}", size);
}

fn print_vector(vec: &mut Vec<i32>) {
    // Now the ownership of the vector is transferred to this function
    vec.push(10); // Changing the value of the vector
    for &i in vec.iter() {
        print!("{} ", i);
    }
}
```

#### Type Inference

Rust can infer the type of a variable based on the value assigned to it.
If you want to know the type of a variable, you can use the `type_of` function from the `std::any` module.

```rust
fn print_type_of<T>(_: &T) {
    println!("{}", std::any::type_name::<T>())
}

fn main() {
    let s = "Hello";
    let i = 42;

    print_type_of(&s); // &str
    print_type_of(&i); // i32
    print_type_of(&main); // playground::main
    print_type_of(&print_type_of::<i32>); // playground::print_type_of<i32>
    print_type_of(&{ || "Hi!" }); // playground::main::{{closure}}
}
```

#### Shadowing

Shadowing is a way to change the value of a variable without changing its type.

```rust
fn main() {
    let x = 32;
    let x = 9.8;      // Shadowing
    let x = "hello";  // Shadowing
    println!("{}",x); // hello


    let m = 10;
    let n = 3;
    let b = m / n; // 3
    let g : f32 = m as f32 / n as f32; // 3.3333333
    println!("{}",g);
}
```

#### Slices

Slices are a reference to a part of a string or an array.

```rust
fn main() {
    let s = String::from("Hello, world!");
    let slice = &s[0..5];  // Slicing the string
    println!("{}", slice);
}
```

#### Struct

A struct is a custom data type that groups together named fields.

```rust
struct Employee {
    name: String,
    age: u8,
    hired: bool,
}

fn main() {
    let emp = Employee {
        name: String::from("Adii"),
        age: 20,
        hired: true,
    };
    println!("Employee Name: {}\nEmployee Age: {}\nEmployee Hired: {}", emp.name, emp.age, emp.hired);
}
```

### Enum

An enum is a custom data type that can have multiple variants.

```rust
enum Color {
    Red,
    Green,
    Blue,
}

fn main() {
    let color = Color::Red;
    match color {
        Color::Red => println!("Red"),
        Color::Green => println!("Green"),
        Color::Blue => println!("Blue"),
    }
}
```

### Option

The `Option` enum is used to handle the absence of a value.

```rust
fn main() {
    let num: Option<i32> = Some(10);
    match num {
        Some(n) => println!("Number: {}", n),
        None => println!("No value"),
    }
}
```

### Result

The `Result` enum is used to handle errors.

```rust
fn main() {
    let result: Result<i32, &str> = Ok(10);
    match result {
        Ok(n) => println!("Number: {}", n),
        Err(e) => println!("Error: {}", e),
    }
}
```

### Loops

1. `loop`: Infinite loop
2. `while`: Conditional loop
3. `for`: Iterative loop

```rust
fn main() {
    let mut i = 0;
    // Infinite loop
    loop {
        if i == 5 {
            break;
        }
        println!("{}", i);
        i += 1;
    }
    i = 0;
    // Conditional loop
    while i < 5 {
        println!("{}", i);
        i += 1;
    }
    // Iterative loop
    for i in 0..5 {  // for(let i = 0; i < 5; i++)
        println!("{}", i);
    }
    // while let
    let mut stack = vec![1, 2, 3, 4, 5];
    while let Some(item) = stack.pop() {
        println!("Popped item: {}", item);
    }
}
```

### Conditional Statements

1. `if`: Single condition
2. `if-else`: Two conditions
3. `if-else if-else`: Multiple conditions
4. `match`: Multiple conditions

```rust
fn main() {
    let num = 10;
    if num > 5 {
        println!("Greater than 5");
    }
    if num > 5 {
        println!("Greater than 5");
    } else {
        println!("Less than or equal to 5");
    }
    if num > 5 {
        println!("Greater than 5");
    } else if num < 5 {
        println!("Less than 5");
    } else {
        println!("Equal to 5");
    }
    match num {
        1 => println!("One"),
        2 => println!("Two"),
        3 => println!("Three"),
        _ => println!("Other"),
    }
}
```

#### Some

Some is a variant of the Option enum that contains a value.

```rust
fn main() {
    let num = Some(10);
    match num {
        Some(n) => println!("Number: {}", n),
        None => println!("No value"),
    }
}
```

#### None

None is a variant of the Option enum that does not contain a value.

```rust
fn main() {
    let num: Option<i32> = None;
    match num {
        Some(n) => println!("Number: {}", n),
        None => println!("No value"),
    }
}
```

#### Ok

Ok is a variant of the Result enum that contains a value.

```rust
fn main() {
    let result: Result<i32, &str> = Ok(10);
    match result {
        Ok(n) => println!("Number: {}", n),
        Err(e) => println!("Error: {}", e),
    }
}
```

#### Err

Err is a variant of the Result enum that contains an error.

```rust
fn main() {
    let result: Result<i32, &str> = Err("Error");
    match result {
        Ok(n) => println!("Number: {}", n),
        Err(e) => println!("Error: {}", e),
    }
}
```

#### If Let

If let is a shorthand for matching an Option or Result.

```rust
fn main() {
    let num = Some(10);
    if let Some(n) = num {
        println!("Number: {}", n);
    }
}
```

```rust
fn main() {
    let result: Result<i32, &str> = Ok(10);
    if let Ok(n) = result {
        println!("Number: {}", n);
    }
}
```

#### While Let

While let is a shorthand for matching an Option or Result in a loop.

```rust
fn main() {
    let mut stack = vec![1, 2, 3, 4, 5];
    while let Some(item) = stack.pop() {
        println!("Popped item: {}", item);
    }
}
```

### Generics

Generics allow you to define functions, structs, and enums that can work with any data type.

```rust
fn main() {
    let num1 = 10;
    let num2 = 20;
    let result = add(num1, num2);
    println!("Sum: {}", result);
}

fn add<T>(num1: T, num2: T) -> T {
    return num1 + num2;
}
```

```rust
