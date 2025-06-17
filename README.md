# Unit 8: Collections

## Introduction
**Collections** allow us to store multiple values inside one object or variable. This helps us manage multiple pieces of data by grouping them together in organized structures. Formally, collections are also called data structures.

### Table of Contents
- [Introduction](#introduction)
    - [Table of Contents](#table-of-contents)
- [Arrays](#arrays)
    - [Declaring and Initializing Arrays](#declaring-and-initializing-arrays)
    - [Accessing Array Elements](#accessing-array-elements)
    - [Array Length](#array-length)
- [For-Each Loops](#for-each-loops)
    - [>Exercise: Volunteer Sign-Ups](#exercise-volunteer-sign-ups)
- [2D Arrays](#2d-arrays)
    - [>Exercise: Checkerboard](#exercise-checkerboard)
- [`ArrayList`s](#arraylists)
    - [`ArrayList` Methods](#arraylist-methods)
    - [>Exercise: Vending Machine](#exercise-vending-machine)
- [`HashSet`s](#hashsets)
    - [>Exercise: Astronomy](#exercise-astronomy)
- [`HashMap`s](#hashmaps)
    - [>Exercise: Locker Numbers](#exercise-locker-numbers)
- [Recap](#recap)
- [>>Project: Filesystem](#project-filesystem)

[Feedback](#feedback) \
[License](#license)

## Arrays
An **array** is a container that holds a fixed number of values (called **elements**) of one data type. \
If a typical variable is like a box, then an array is like a row of numbered boxes taped together into a single unit.

### Declaring And Initializing Arrays
Arrays are a bit unique, and Java has built-in syntax for them. They do not look similar to other Java collections. \
To write out an array type (e.g. for declaring an array variable), first put the element type (e.g. `int`) and then put a pair of square brackets `[]` immediately after. \

For example, to declare but not initialize a variable of an array of integers:
```java
int[] numbers;
```
To actually create the array object, use the following expression:
```java
new ELEMENT_TYPE[ARRAY_SIZE]
```
Where `ELEMENT_TYPE` is the array element type such as `int`, and `ARRAY_SIZE` is an integer representing how large the array is (how many elements it holds). \
Example:
```
int[] numbers = new int[10];
```
When creating an array like this, the array elements all start out as the default value of the element type. \
Recall from Unit 7 that the default value for primitives is a zero-like value, and for objects (reference types) it is `null`. \
So, an array of `int` would have all `0` elements, while an array of `Integer`, `String`, or `Employee` would have `null`.

In many cases though, we want the array to start with known initial values. \
We can use an array 'initializer' to list out all of the values manually. \
The expression looks like this for creating an array with initial values:
```java
new ELEMENT_TYPE[]{element1, element2, element3, ...}
```
Where `element1`, etc. are values of type `ELEMENT_TYPE`. Any number of elements can be used, including 0 elements. \
Note that since we listed out each element, we also didn't have to specify the array size between the square brackets; Java automatically figures out the length. \
Concrete example:
```java
int[] numbers;
numbers = new int[]{1, 2, 4, 8};
numbers = new int[]{-1};
```
When using this as the initial value of a variable or field declaration, we can omit the `new ELEMENT_TYPE[]` part (just put `{a, b, ...}`) because the type is already known from the declaration in the same statement:
```
int[] numbers = {0, 10, 100, 1000};
```
The length of a created array object cannot be changed, elements cannot be deleted nor extra elements added. \
Array variables can take a new array object of a different length though, the array size isn't included in the array type.

> **Note:** Array types are reference types, not primitive types. So `null` can be assigned to an array variable. \
> Also, the element type can be any type: primitive, reference, even other arrays.

### Accessing Array Elements
Now we have a variable that can store many values inside it! But how can we access these values, to use and modify them?

We can access an individual element of an array using its **index**. Each value inside an array has an index integer, which tells you its 'spot' (1st item, 2nd item, etc.)
```
array[index]
```
`index` is usually of type `int. \
This array indexing is like its own variable, the box in the array at the `index`: you can access it, assign to it, even use assignment operators like `+=` and `--`;

In almost all programming languages, arrays and other collections are **zero-indexed**, which means that the <u>index number for the first value is `0`</u> (NOT `1`). This means that the second element has index `1`, the third has index `2`, and so forth. **Be very careful about this!**

Example:
```java
int[] oddNumbers = {1, 3, 5, 7, 9}; // An array of the first 5 odd numbers
System.out.println(oddNumbers[0]); // Prints 1
System.out.println(oddNumbers[4]); // Prints 9
System.out.println(oddNumbers[5]); // ERROR! Index is out of bounds
```

We can assign array elements using the index:
```java
String[] messages = new String[3];
messages[1] = "I'm in the middle!";
System.out.println(messages[1]); // Output: I'm in the middle!
messages[1] = "I'm lonely :("
System.out.println(messages[1]); // Output: I'm lonely :(
```
Here, we create an empty `String` array, then assign the *second* value (at index `1`) to the sentence `I'm in the middle!`. We call this value in our print statement using the same name and index. We can then *reassign* this element of the array, and print its new value.

### Array Length
We can use the **length** field of arrays to find out how many elements they have (`int`).

For example:
```java
String[] animals = {"cat", "dog", "bird", "lizard"};
System.out.println(animals.length); // Outputs 4
```
Since arrays are of fixed size, this field is final (read-only).

For an array `arr`, an index must be between `0` and `arr.length - 1` inclusive to be valid (so `arr.length - 1` is the index of the last element). A **4**-element array has valid *indices* `0`, `1`, `2`, `3`.

## For-Each Loops
A **for-each loop** is a special kind of loop that iterates through each item of an array, or other collection.

For-each loops look like this:
```
for (<datatype> <variableName> : <array>) {
    // code to be executed in each iteration
}
```
In English, this construct can be interpreted as: "For each item <variableName> in <array>, execute the code block." The variable `<variableName>` is assigned an item in the collection, for every iteration. \
Collections are iterated through in first to last order.

Example:
```java
// Creates an array to iterate through
String[] emotions = {":)", ":|", ":(", ">:(", ">:)"};

// Prints every item in the emotions array
for (String emotion : emotions) {
    System.out.println(emotion);
}
```
Output:
```
:)
:|
:(
>:(
>:)
```
In this example, we are using a for-each loop to go through the `emotions` array and print every item (much more concise than doing it one at a time manually!). Note how inside the for-each loop, we use the name `emotion` to refer to the item being used in the current iteration.

If you want to print an array's contents, use a loop to access its elements. Trying to print the array object itself gives an irrelevant hash code representation.

In some cases though, a for loop has to be used instead of a for-each loop. \
Here are a few restrictions of for-each loops:
- Cannot write to the collection easily (setting elements)
- Index of element not available in loop
- Can only iterate in first-to-last order

Here's an example of using a regular for loop with an array:
```java
int[] numbers = {1, 2, 3, 4, 5};
for (int i = 0; i < numbers.length; i++) {
    // Square each number in the array
    numbers[i] *= numbers[i];
}
```

### >Exercise: Volunteer Sign-Ups
You're organizing a beach clean-up and posted 8 slots for people to sign up on a volunteer website.

[`Volunteer.java`](Volunteer.java)
1. Initialize something to store up to 8 volunteer names. `null` indicates no volunteer.
2. Two people named `Robert` and `Penelope` have signed up! Fill in the first two slots for them.
3. `Penelope` wants to go by `Penny`. Update her slot.
4. You have a large group of students willing to help out as well! For each element in the array, check if it is empty and fill empty slots with `Student`.
5. Print each item in your completed array.

<details><summary>Solution Code</summary>

```java
public class Volunteer {
    public static void main(String[] args) {
        String[] signups = new String[8];
        signups[0] = "Robert";
        signups[1] = "Penelope";
        signups[1] = "Penny";

        for (int i = 0; i < signups.length; i++) {
            if (signups[i] == null) {
            signups[i] = "Student";
            }
        }

        for (String signup : signups) {
            System.out.println(signup);
        }
    }
}
```

Output:
```
Robert
Penny
Student
Student
Student
Student
Student
Student
```
</details>

## 2D Arrays
A single value is like a point, 0-dimensional. An array is like a line, 1-dimensional. An array of arrays is like a grid, 2-dimensional.

The element type of an array can be other collections: such as an array of integers, which is useful for representing grids and other structures.

Example usage:
```java
int[][] grid = new int[3][4];
grid[1][2] = 10;
```
Here, we declare `grid` as an array of arrays of `int`. Then, we initialize it: the array has 3 `int` inner arrays, each with length 4. \
Another way to say this is that the grid has 3 **rows** and 4 **columns**. (By convention, rows correspond to the first index.) \
Then, the second array's third element is set to `10`.

> **Note:** The length of the inner arrays doesn't have to be consistent. \
> We could for example set `grid[0] = new int[7];`.

Initializer arrays also work:
```java
int[][] grid = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

One can iterate through the rows of the grid with a for loop. And you can then iterate through the values in each row with an nested inner for loop.

Example:
```java
int[][] grid = {
    {0, 1, 2},
    {1, 2, 3},
    {2, 3, 4}
};
// Print each value in the grid
for (int[] array : grid) {
    for (int value : array) {
        System.out.print(value + " ");
    }
    System.out.println();
}
// Update each value in the grid
for (int row = 0; row < grid.length; row++) {
    for (int col = 0; col < grid[row].length; col++) {
        grid[row][col] -= row * col;
    }
}
```
Output:
```
0 1 2 
1 2 3 
2 3 4 
```

### >Exercise: Checkerboard

[`Checkerboard.java`](Checkerboard.java)
1. Create an 8x8 `int` grid.
2. Use for loops to initialize each element as the sum of the row and column indices.
3. For each value in the grid, print out `#` for even values and `+` for odd values. Rows should be on their lines.

<details><summary>Solution Code</summary>

```java
public class Checkerboard {
    public static void main(String[] args) {
        int[][] checkerboard = new int[8][8];
        for (int i = 0; i < 8; i++) {
            for (int j = 0; j < 8; j++) {
                checkerboard[i][j] = i + j;
            }
        }

        for (int[] array : checkerboard) {
            for (int num : array) {
                if (num % 2 == 0) {
                    System.out.print("# ");
                } else {
                    System.out.print("+ ");
                }
            }
            System.out.println();
        }
    }
}
```
Output:
```
# + # + # + # + 
+ # + # + # + #
# + # + # + # +
+ # + # + # + #
# + # + # + # +
+ # + # + # + #
# + # + # + # +
+ # + # + # + #
```
</details>

## `ArrayList`s
**`ArrayList`s** are like *automatically-resizing arrays*, so elements can always be freely added and removed and we don't have to worry about the size. \
The `ArrayList` class needs to be imported from the `java.util` package.

We can declare `ArrayList`s like this:
```java
// Import the ArrayList class
import java.util.ArrayList;

public class Main {
    public void static main(String[] args) {
        ArrayList<String> list = new ArrayList<String>();
    }
}
```
The element type of the `ArrayList` values goes inside the `<>`. The angled brackets `<>` indicate a **generic** type: similar to arrays, the programmer decides what type of data the generic collection holds.

Unlike arrays which aren't generic, only reference types can be used as the element type, primitive types are illegal to use inside generic types. To use primitive data in ArrayLists, put the equivalent wrapper class instead, e.g. `Integer` for `int`, `Double` for `double`.

> **Note:** You can omit the type within the angled brackets when creating the `ArrayList` as an initial value for a variable or field declaration, e.g.:
> ```java
> ArrayList<String> list = new ArrayList<>();
> ```
> This works for other generic types too.

Unlike arrays, you can print out an `ArrayList` object and its contents will be shown.

### `ArrayList` methods
We can *add* and *remove* items from `ArrayList`s using methods.

We can add items to the end of the list using the `add()` method:
```java
ArrayList<Integer> primes = new ArrayList<Integer>();
primes.add(2);
primes.add(3);
primes.add(5);
primes.add(7);
System.out.println(primes); // Output: [2, 3, 5, 7]
```
We can add as many elements as we want to `primes` without having to worry about size.

We can also specify the index to add an element at, using a different overload of `add()` with 2 arguments:
```java
ArrayList<Integer> primes = new ArrayList<Integer>();
primes.add(3);
primes.add(5);
primes.add(7);
primes.add(0, 2); // add the value 2 at index 0 (first item)
System.out.println(primes); // Output: [2, 3, 5, 7]
```
Note how adding an element at a certain index does not *replace* the element already there; that element and the ones after the specified index are all shifted down 1 to add the new element. \
To replace the element instead, use the `set()` method.
```java
primes.set(0, -1) // Set the first element to -1
```

We can remove elements using the `remove()` method:
```java
ArrayList<Integer> primes = new ArrayList<Integer>();
primes.add(2);
primes.add(3);
primes.add(5);
primes.add(6); // 6 isn't prime!!
primes.add(7);
primes.remove(3); // primes only >:(
System.out.println(primes); // Output: [2, 3, 5, 7]
```
Note how for the `remove()` method, we specify the element to remove using its *index* rather than its *value*. 

Additionally, we can use `clear()` to get rid of all the elements in an `ArrayList`:
```java
ArrayList<Integer> primes = new ArrayList<Integer>();
primes.add(0); // What.
primes.add(3);
primes.add(8); // That's wrong
primes.add(12); // That's DEFINITELY wrong
primes.add(-6); // Okay, that's it.
primes.clear();
System.out.println(primes); // Output: []
```

To get the size of an ArrayList, we can use the `size()` method:
```java
ArrayList<Integer> primes = new ArrayList<Integer>();
primes.add(2);
primes.add(5);
primes.add(1, 3);
primes.remove(2);
System.out.println(primes); // Output: [2, 3]
System.out.println(primes.size()); // Output: 2
```

> **Note:** Unlike arrays, there is no nice syntax for manually initializing an `ArrayList` with starter values. You have to use `add()` repeatedly, or use a loop.

We can use the `get()` method to access an ArrayList element at a specified index:
```java
primes.get(0);
```

You can loop through ArrayLists using for-each loops the same way you can with arrays:
```java
ArrayList<Integer> primes = new ArrayList<Integer>();
primes.add(2);
primes.add(3);
primes.add(5);
for (int num : primes) {
    System.out.println(num);
}
```
Output:
```
2
3
5
```

### >Exercise: Vending Machine
You are a sentient vending machine. Somehow, you're more concerned with letting people know what snacks you have available to them than *how you are a sentient vending machine*.

[`VendingMachine.java`](VendingMachine.java)
1. Create a list of all the snacks you have. Currently, that consists of `Goldfish`, `Fritos`, `Skittles`, `Snickers`, and `Chex Mix`.
2. Print your list on one line to let everyone know what they can buy.
3. All the `Snickers` have been bought.
4. `Doritos` were just restocked, between the `Fritos` and `Skittles`.
5. Print the updated list on one line, as well as its size on another.
6. Because of your meticulously crafted lists, people discovered your sentience and called the police. The police promptly arrive on the scene and raid all your snacks. (That way, you can never take over the world.)
7. Print your final list of snacks on one line.

<details><summary>Solution Code</summary>

```java
import java.util.ArrayList;

public class VendingMachine {
    public static void main(String[] args) {
        ArrayList<String> snacks = new ArrayList<String>();
        snacks.add("Goldfish");
        snacks.add("Fritos");
        snacks.add("Skittles");
        snacks.add("Snickers");
        snacks.add("Chex Mix");
        System.out.println("Snacks: " + snacks);

        snacks.remove("Snickers");
        snacks.add(2, "Doritos");
        System.out.println("Updated snacks: " + snacks);
        System.out.println("Total snacks: " + snacks.size());

        snacks.clear();
        System.out.println("No snacks left: " + snacks);
    } 
}
```
Output:
```
Snacks: [Goldfish, Fritos, Skittles, Snickers, Chex Mix]
Updated snacks: [Goldfish, Fritos, Doritos, Skittles, Chex Mix]
Total snacks: 5
No snacks left: []
```
</details>

## `HashSet`s
A **HashSet** is a collection type that where *every item is unique*, but *items are not ordered nor indexed*. \
The `HashSet` class is also in the `java.util` package.

`HashSet`s look like this, quite similar to `ArrayList`:
```java
// Import the HashSet class
import java.util.HashSet;

public class Main {
    public void static main(String[] args) {
        HashSet<String> reptiles = new HashSet<String>();
    }
}
```
(Like `ArrayList`, `HashSet` is a generic type that uses angled brackets.)

We can add/remove items like this:
```java
HashSet<String> reptiles = new HashSet<String>();
reptiles.add("Bearded Dragon");
reptiles.add("Turtle");
reptiles.add("Frogs"); // Nope! Frogs are amphibians!
reptiles.remove("Frogs");
reptiles.add("Turtle"); // Turtle is not added twice
```
While the `add()` and `remove()` methods are similar to those on `ArrayList`, there are a few things to note. \
First of all, neither method involves indices because `HashSet`s do not have them. Instead, only the actual value is needed. \
Additionally, HashSets will not add duplicate items; when we try to add `Turtle` again in the example, it will simply be ignored.

We can also check if an item exists in a `HashSet` using the `contains()` method:
```java
HashSet<String> reptiles = new HashSet<String>();
reptiles.add("Bearded Dragon");
reptiles.add("Turtle");
System.out.println(reptiles.contains("Turtle")); // Output: true
System.out.println(reptiles.contains("Unicorn")); // Output: false
```

And check its size using the `size()` method:
```java
HashSet<String> reptiles = new HashSet<String>();
reptiles.add("Bearded Dragon");
reptiles.add("Turtle");
reptiles.add("Snake");
System.out.println(reptiles.size()); // Output: 3
```

Using for-each loops for `HashSet`s is the same as it is with arrays and `ArrayList`s, but for `HashSet`s there is no deterministic order:
```java
HashSet<String> reptiles = new HashSet<String>();
reptiles.add("Bearded Dragon");
reptiles.add("Turtle");
reptiles.add("Snake");
for (String reptile : reptiles) {
    System.out.println("I love " + reptile + "s!");
}
```
One possible output (order is arbitrary depending on Java implementation):
```
I love Bearded Dragons!
I love Turtles!
I love Snakes!
```

### >Exercise: Astronomy
You're looking through a telescope on a clear night, looking for the constellation Cassiopeia.

[`Astronomy.java`](Astronomy.java)
1. Create a collection to hold all the *unique* constellations you've seen so far.
2. As you look around, you see the constellations `Leo Minor`, `Lynx`, `Cepheus`, and `Ursa Minor`.
3. You realize that the group of stars you recorded as `Cepheus` are actually part of two separate constellations, `Lacerta` and `Camelopardalis`. (Remove `Cepheus` and add the other two.)
4. You just came across the constellation `Lynx`, but can't remember if you've already recorded it. Better add it again just in case.
5. In your head, make a prediction of the collection's size. Then print out the actual size.
6. Have you found `Cassiopeia` yet? Print whether or not it's in your collection.
7. You've finally found `Cassiopeia`, just between `Lacerta` and `Camelopardalis`! Add it to your collection and print all the constellations you discovered tonight.

<details><summary>Solution Code</summary>

```java
import java.util.HashSet;

public class Astronomy {
    public static void main(String[] args) {
        HashSet<String> constellations = new HashSet<String>();
        constellations.add("Leo Minor");
        constellations.add("Lynx");
        constellations.add("Cepheus");
        constellations.add("Ursa Minor");

        constellations.remove("Cepheus");
        constellations.add("Lacerta");
        constellations.add("Camelopardalis");
        constellations.add("Lynx");

        System.out.println("I've found " + constellations.size() + " constellations!");
        System.out.println("Have I found Cassiopeia? " + constellations.contains("Cassiopeia"));

        constellations.add("Cassiopeia");
        
        for (String constellation : constellations) {
            System.out.println("I found the constellation " + constellation);
        }
    } 
}
```
Output:
```
I've found 5 constellations!
Have I found Cassiopeia? false
I found the constellation Lynx
I found the constellation Cassiopeia
I found the constellation Ursa Minor
I found the constellation Lacerta
I found the constellation Leo Minor
I found the constellation Camelopardalis
```
</details>

## `HashMap`s
A **`HashMap`** looks a little different compared to `ArrayList`s and `HashSets`. `HashMap`s store items in **(key, value)** pairs. Each key is associated with a value, and you can access that value using the corresponding key. \
Keys are essentially arbitrary indices that can be objects instead of ordered integers. \
`HashMap`s are also imported from `java.util`.

As from the name, `HashMap`s are related to `HashSet`s: a `HashSet` is basically a `HashMap` but without the values for the pairs. This course will not discuss what hashing is and how these two collections work under the hood.

`HashMap`s look like this:
```java
// Import the HashMap class
import java.util.HashMap;

public class Main {
    public static void main(String[] args) {
        HashMap<String, String> stateCapitals = new HashMap<String,     String>();
    }
}
```
`HashMap` is also a generic type, like `ArrayList` and `HashSet`; the major difference in its declaration is that `HashMap`s have to declare *two* types within the `<>`, the first for the key type and the second for the value type.

We can add key-value pairs to `HashMap`s using the `put()` method, and remove them by key using `remove()`:
```java
// A mapping of states to their capitals
HashMap<String, String> stateCapitals = new HashMap<>();
stateCapitals.put("California", "Sacramento");
stateCapitals.put("Texas", "Austin");
stateCapitals.put("Massachusetts", "Boston");
stateCapitals.remove("Texas"); // Accessed using the pair's key only
System.out.println(stateCapitals);
// Output: {Massachusetts=Boston, California=Sacramento}
```

We can also use the `clear()` method to remove all items from a `HashMap`:
```java
HashMap<String, String> stateCapitals = new HashMap<>();
stateCapitals.put("California", "Sacramento");
stateCapitals.put("Texas", "Austin");
stateCapitals.put("Massachusetts", "Boston");
stateCapitals.clear();
System.out.println(stateCapitals);
// Output: {}
```

To access a value in a `HashMap`, use `get()` to get the value for a key:
```java
HashMap<String, String> stateCapitals = new HashMap<>();
stateCapitals.put("California", "Sacramento");
stateCapitals.put("Texas", "Austin");
stateCapitals.put("Massachusetts", "Boston");
System.out.println(stateCapitals.get("California"));
// Output: Sacramento
```

To access the size of a HashMap, use `size()`:
```java
HashMap<String, String> stateCapitals = new HashMap<>();
stateCapitals.put("California", "Sacramento");
stateCapitals.put("Texas", "Austin");
stateCapitals.put("Massachusetts", "Boston");
System.out.println(stateCapitals.size());
// Output: 3
```

Using for-each loops for HashMaps looks a little different, depending on whether you want to loop through the keys or values. \
To iterate through *keys*, use `.keySet()` method. (You can then also use the key to get the value too.) \
To iterate through *values*, use `.values()` method.
```java
HashMap<String, String> stateCapitals = new HashMap<>();
stateCapitals.put("California", "Sacramento");
stateCapitals.put("Texas", "Austin");
stateCapitals.put("Massachusetts", "Boston");

// Prints all states
for (String state : stateCapitals.keySet()) {
    System.out.println("State: " + state);
}
// Prints all capitals
for (String capital : stateCapitals.values()) {
    System.out.println("Capital: " + capital);
}
```
Output:
```
State: Texas
State: Massachusetts
State: California
Capital: Austin
Capital: Boston
Capital: Sacramento
```

### >Exercise: Locker Numbers
You're a school administrator and need a way to keep track of students' locker numbers.

[`LockerNumbers.java`](LockerNumbers.java)
1. Create a collection that allows you to access the name of the student using a given locker number.
2. Recently, three students have been assigned new lockers. `George` got locker `11`, `Anna` got locker `5`, and `Harper` got locker `43`. Record this in your collection.
3. `George` transferred to another school and is no longer using his locker.
4. Print the number of lockers currently in use.
5. Another student, `Mark`, transferred in and took locker `17`.
6. The lock on locker `11` is missing. Print out the name of the student assigned to that locker.
7. It's the end of the school year! Remove all student names and locker numbers from your collection.

Bonus challenge: \
`Anna` forgot which locker she got. Search for and find her locker number using her name.

<details><summary>Solution Code</summary>

```java
import java.util.HashMap;

public class LockerNumbers {
    public static void main(String[] args) {
        HashMap<Integer, String> lockers = new HashMap<Integer, String>();
        lockers.put(11, "George");
        lockers.put(5, "Anna");
        lockers.put(43, "Harper");

        lockers.remove(11);
        System.out.println("Currently using " + lockers.size() + " lockers.");
        lockers.put(17, "Mark");
        System.out.println(lockers.get(11) + " is using locker 11.");
        lockers.clear();
    } 
}
```
Output:
```
Currently using 2 lockers.
null is using locker 11.
```
</details>

## Recap
- Arrays hold a fixed number of elements of one type
- An array type is `TYPE[]`, and to create one use `new TYPE[SIZE]`
- Arrays can be initialized with `new TYPE[]{elem1, elem2, ...}`, where the `new TYPE[]` part can be omitted when there is enough context
- Access an array element with (`index` is an `int` with 1st element at index `0`): `array[index]`; it is like a variable
- Use `array.length` field to get the fixed array length
- A for-each loop is declared like `for (Item item : items) { ... }`, where `items` is an array or collection with `Item` elements
- `ArrayList` is an automatically-resizing array, the type is `ArrayList<TYPE>` (generic), instances created like normal objects with `new`
- `ArrayList` has methods `add(item)`, `add(index, item)`, `remove(index)`, `clear()`, `get(index)`, `size()`
- `HashSet` is a collection of unique, unordered (no index) items, declared and created similarly to `ArrayList`
- `HashSet` has methods `add(item)`, `remove(item)`, `contains(item)`, `size()`
- `HashMap` is a collection of key-value pairs, where the key acts like an index for the value; generic with both types in `<>`
- `HashMap` has methods `put(key, value)`, `remove(key)`, `clear()`, `get(key)`, `size()`
- `ArrayList`, `HashSet`, and `HashMap` are all classes in the `java.util` package

## >>Project: Filesystem
Create a program that simulates a hierarchical filesystem in memory. Users can navigate, create, delete, and manage files and directories. \
[`project/Filesystem.java`](project/Filesystem.java) (you will need to create more files)

A filesystem has multiple components, structured in a hierarchy.
- A **filesystem** is the overall entity. It contains multiple drives.
- A **drive** typically represents a physical storage device's data. It contains a single root directory.
- A **directory**, commonly known as a folder, contains multiple entries: files or directories.
- A **file** contains actual data.
- **Entry** is the general term for a file or directory.

This filesystem has many commands to navigate and modify data. \
The *current working directory* (CWD) is the 'selected' directory that acts as a workspace; other commands operate relative to this directory.

A **path** is a description of the location and name of an entry. \
If a path does not depend on the current working directory, it is an *absolute* path. \
Absolute paths start with the drive letter, e.g. `C`, followed by a colon `:`, then directories separated by `/`, until the specified entry. \
Example:
```
C:/Users/user/Documents/myfile.txt
```
(We will use forward slash `/` instead of the usual Windows backslash `\` as the separator.)

*Relative* paths depend on the current working directory. \
A dot `.` represents the path of the current working directory. Relative paths start with `./` so they start from the CWD. \
In practice, you can omit the `./` and just start with the entry names; the `./` is assumed. \
Examples:
```
./README.md
Unit-8/project/Filesystem.java
```
A `..` represents the parent directory of the CWD.

A useful method is `String`'s `.split(separator)` method. Example:
```java
String path = "Unit-8/project/Filesystem.java";
String[] parts = path.split("/"); // {"Unit-8", "project", "Filesystem.java"}
```
You will need this for parsing paths and commands.

Required features of the classes:
- File
    - Attributes:
        - Name (e.g. `README.md`)
        - Parent directory
        - Data (one large `String`); defaults to empty string
    - Operations (these might not be used in the program):
        - Get path: path of parent + name
        - Read (just gives the data)
        - Write (replaces the data with new data)
        - Append (concatenates new data to the end of existing data)
- Directory
    - Attributes:
        - Name (e.g. `Unit-8`); a root directory has an empty zero-length name
        - Parent directory
        - Entries: arbitrary number of files and directories
    - Operations:
        - Get path: path of parent (if self has one) + name
        - Add an entry
        - Remove an entry by name
        - Get an entry by name
        - Give all entries
- Drive
    - Attributes:
        - Letter (e.g. `C`, `D`): a single capital letter
        - Root directory: one directory with no parent, that contains all of the data of the drive
- Filesystem
    - Attributes:
        - Multiple drives (note that there can only be up to 26 because they are alphabetical)
        - Current working directory
    - Operations:
        - Put the `main` method in this class
        - Simulate a terminal: an input loop where the user can input commands and see output
        - All commands
        - Get an entry by absolute or relative path

You'll need to create an interface or base class for a filesystem *entry* too.

Commands are entered as a single line, after a `> `. \
The first word is the command name. \
If the command needs an input such as a path or name, it is the next thing in the command. \
Example:
```
> rm file.txt
```

Required commands:
- `touch path`: Create a new empty file in this directory, with the given path and name. (Does not fail if it already exists.) Fails if the parent directory of the path does not exist
- `mkdir path`: Create a new empty directory in this one, with the given path and name (last part of path). Fails if it already exists or if the parent directory of the path does not exist
- `rm path`: Remove a file or directory with a given path. Fails if it does not exist
- `ls`: List entries of the current working directory. Add `/` to the end of directory names, to distinguish them from files
- `cd path`: Change the current working directory. Fails if the given path does not exist or if the entry is a file instead of a directory
- `pwd`: Print the current working directory path, absolute
- `help`: List available commands (descriptions are not required)
- `exit`: Exit the terminal and the entire program

Optional commands:
- `echo data`: Prints `data` as-is
- `mv source dest`: Move a file or directory from the source path to the destination path (note: `dest` isn't the path of the parent directory, it is the actual entry path). Errors if source path does not exist or dest path's parent directory does not exist
- `cp source dest`: Same as `mv`, but copies the entry instead; file contents are copied, and directory entries are recursively copied
- `ls path`: Same as `ls` but applies to the given directory's path. Errors if it does not exist or is a file

If an invalid command or input is given or the command fails, tell the user, and continue receiving commands.

The initial state of the file system is that there are `C` and `D` drives with empty root directories, and the current working directory is the root directory of the `C` drive.

Example terminal input/output (output format, especially error messages, may differ):
```
> pwd
C:
> touch file.txt
> mkdir folder
> ls
file.txt
folder/
> cd folder
> mkdir C:/folder/sub
> pwd
C:/folder
> touch folder/file.txt
Error: cannot touch 'C:/folder/folder/file.txt': no such file or directory
> cd ..
> rm folder
> ls
file.txt
> mkdir ./file.txt
Error: cannot create directory 'C:/file.txt': file or directory exists
> rm D:/file.txt
Error: cannot remove 'D:/': no such file or directory
> exit 
```

## Feedback
Please provide feedback if you have any.
<details><summary>Possible feedback points</summary>

- Confusing explanations
- Knowledge, skills, or procedures that were required but weren't taught
- Too fast or too slow explanations; pacing
- Too hard or too easy exercises
- Step-by-step instructions that are not comprehensive/thorough enough, or didn't work
- Seemingly unnecessary or ineffective information or exercises
- Any improvements (e.g. wording) or more effective ways/formats to teach
</details>

___



## License
© 2025 @aatle, @spacepotatoes3, @gjgarson, @KaitoTLex

This work is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).
