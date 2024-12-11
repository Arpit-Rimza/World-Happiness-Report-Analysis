Section 2: Coding Questions[¶](#Section-2:-Coding-Questions)
============================================================

2.1 A) Write a function that takes in a string and returns the number of unique consonants[¶](#2.1---A)-Write-a-function-that-takes-in-a-string-and-returns-the-number-of-unique-consonants)
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

In \[1\]:

def count\_unique\_consonants(input\_string):
    """
    Counts the number of unique consonants in a given string.
    
    Parameters:
        input\_string (str): The input string to analyze.
        
    Returns:
        int: The number of unique consonants in the string.
    """
    \# Validate input
    if not isinstance(input\_string, str):
        raise ValueError("Input must be a string.")
    
    consonants \= set("bcdfghjklmnpqrstvwxyz")  \# Set of consonants
    seen \= set()  \# Set to track characters seen
    duplicates \= set()  \# Set to track duplicate characters
    
    \# Normalize string to lowercase for uniformity
    input\_string \= input\_string.lower()
    
    for char in input\_string:
        if char in consonants:
            if char in seen:
                duplicates.add(char)  \# Mark as duplicate
            else:
                seen.add(char)
    
    \# Unique consonants are those in 'seen' but which are not in 'duplicates'
    unique\_consonants \= seen \- duplicates
    return len(unique\_consonants)

\# Examples 
try:
    print(count\_unique\_consonants("cat"))        \# Output: 2
    print(count\_unique\_consonants("cataract"))  \# Output: 1
    print(count\_unique\_consonants(""))          \# Output: 0
    print(count\_unique\_consonants(123))         \# Raises ValueError
except ValueError as e:
    print(e)

2
1
0
Input must be a string.

2.1 B) What is the time and space complexity of your solution? If you are making any assumptions in your calculations, list them.[¶](#2.1-B)--What-is-the-time-and-space-complexity-of-your-solution?-If-you-are-making-any-assumptions-in-your-calculations,-list-them.)
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Time and Space Complexity Analysis[¶](#Time-and-Space-Complexity-Analysis)
--------------------------------------------------------------------------

### Assumptions[¶](#Assumptions)

*   The input string's length is **n**.
*   The set of consonants (`consonants`) has a fixed size (21 in the English alphabet), making its operations **O(1)**.
*   Python’s built-in set data structure is used, which provides **O(1)** average time complexity for insertions, deletions, and lookups.

* * *

### Time Complexity[¶](#Time-Complexity)

#### 1\. **Normalization (`input_string.lower()`)**[¶](#1.-Normalization-(input_string.lower()))

*   This operation traverses the entire string once, so its complexity is **O(n)**.

#### 2\. **Iterating Through Characters**[¶](#2.-Iterating-Through-Characters)

*   We loop through each character in the string, which has a time complexity of **O(n)**.

#### 3\. **Set Operations**[¶](#3.-Set-Operations)

For each character, we perform:

*   A membership check in the `consonants` set (**O(1)**).
*   Membership checks and insertions in the `seen` and `duplicates` sets (**O(1)** each on average).

Since each of these operations is **O(1)**, the total complexity of these operations for all characters is **O(n)**.

#### 4\. **Calculating Unique Consonants**[¶](#4.-Calculating-Unique-Consonants)

*   Subtracting one set from another (`seen - duplicates`) involves iterating over the smaller of the two sets, which is **O(1)** in terms of **n**, as the size of these sets is bounded by the number of unique consonants (at most 21).

### **Total Time Complexity**: **O(n)**.[¶](#Total-Time-Complexity:-O(n).)

* * *

### Space Complexity[¶](#Space-Complexity)

#### 1\. **Storage for the Input String**[¶](#1.-Storage-for-the-Input-String)

*   The input string itself requires **O(n)** space.

#### 2\. **Storage for Sets**[¶](#2.-Storage-for-Sets)

*   The `seen` and `duplicates` sets store unique consonants encountered, with a maximum size of 21 (the total number of English consonants). This is effectively **O(1)** space.
*   The `consonants` set is a constant-size set (**O(1)**).

#### 3\. **Temporary Storage During Subtraction**[¶](#3.-Temporary-Storage-During-Subtraction)

*   The set operation (`seen - duplicates`) involves a temporary result set, also of size at most 21 (**O(1)**).

### **Total Space Complexity**: **O(n)**, dominated by the storage of the input string.[¶](#Total-Space-Complexity:-O(n),-dominated-by-the-storage-of-the-input-string.)

* * *

2.2 Write a function that finds how many squares are in a X by X grid.[¶](#2.2-Write-a-function-that-finds-how-many-squares-are-in-a-X-by-X-grid.)
--------------------------------------------------------------------------------------------------------------------------------------------------

### Recursive Solution[¶](#Recursive-Solution)

In \[2\]:

def total\_squares\_recursive(X):
    """
    Calculate the total number of squares in an X x X grid using recursion.
    
    Parameters:
        X (int): The size of the grid (number of rows/columns).
        
    Returns:
        int: The total number of squares of all sizes in the grid.
        
    Raises:
        ValueError: If X is not a positive integer.
    """
    \# Input validation: ensure X is a positive integer
    if not isinstance(X, int) or X <= 0:
        raise ValueError("Input must be a positive integer.")
    
    \# Base case: A 1x1 grid has exactly 1 square
    if X \== 1:
        return 1
    
    \# Recursive case: Total squares in an X x X grid is X^2 + squares in smaller grids
    return X \*\* 2 + total\_squares\_recursive(X \- 1)

\# Example usage
print(total\_squares\_recursive(1))  \# Output: 1 (1x1 grid)
print(total\_squares\_recursive(2))  \# Output: 5 (2x2 grid)
print(total\_squares\_recursive(3))  \# Output: 14 (3x3 grid)
print(total\_squares\_recursive(4))  \# Output: 30 (4x4 grid)

1
5
14
30

### Non-Recursive Solution[¶](#Non-Recursive-Solution)

In \[3\]:

def total\_squares\_non\_recursive(X):
    """
    Calculate the total number of squares in an X x X grid using a non-recursive approach.
    
    Parameters:
        X (int): The size of the grid (number of rows/columns).
        
    Returns:
        int: The total number of squares of all sizes in the grid.
        
    Raises:
        ValueError: If X is not a positive integer.
    """
    \# Input validation: ensure X is a positive integer
    if not isinstance(X, int) or X <= 0:
        raise ValueError("Input must be a positive integer.")
    
    total \= 0  \# Initialize the total number of squares to 0
    
    \# Loop through each possible square size k x k, where k ranges from 1 to X
    for k in range(1, X + 1):
        total += k \*\* 2  \# Add the number of k x k squares to the total
    
    return total  \# Return the total number of squares

\# Example
print(total\_squares\_non\_recursive(1))  \# Output: 1 (1x1 grid)
print(total\_squares\_non\_recursive(2))  \# Output: 5 (2x2 grid)
print(total\_squares\_non\_recursive(3))  \# Output: 14 (3x3 grid)
print(total\_squares\_non\_recursive(4))  \# Output: 30 (4x4 grid)

1
5
14
30

Section 3: Theory Challenge - Hashing[¶](#Section-3:-Theory-Challenge---Hashing)
================================================================================

3.1 Design a Basic Hash Function[¶](#3.1-Design-a-Basic-Hash-Function)
----------------------------------------------------------------------

### **Design Principles**[¶](#Design-Principles)

1.  **Efficiency:** The hash function must be simple to compute, as efficiency is crucial.
2.  **Memory Constraints:** Ensure the function distributes values evenly over a fixed range of buckets, avoiding overuse of memory.
3.  **Collision Handling:** Collisions are inevitable, so a robust strategy must be used to manage them effectively.

### **Chosen Hash Function**[¶](#Chosen-Hash-Function)

We define the hash function as: \[ \\text{hash}(key) = \\left( \\sum\_{i=1}^{n} \\text{ASCII}(key\[i\]) \\times i \\right) \\mod N \]

*   **Explanation:**
    
    *   The function computes the sum of the ASCII values of the characters in the key.
    *   To add variability, each character's ASCII value is multiplied by its positional index (i).
    *   The result is reduced modulo (N) (the number of buckets) to fit within the hash table size.
*   **Advantages:**
    
    *   Simple to compute and memory efficient.
    *   The inclusion of the position index reduces clustering, distributing keys more uniformly.
    *   (N) (number of buckets) can be a prime number to further reduce collisions.

### **Collision Handling Mechanism**[¶](#Collision-Handling-Mechanism)

*   **Chaining:** Each bucket stores a linked list of keys. When a collision occurs, the new key is appended to the list.
*   **Open Addressing (Optional):** Use **linear probing**, which looks for the next available bucket sequentially.

### **Why this is a Good Design**[¶](#Why-this-is-a-Good-Design)

1.  **Uniform Distribution:** Using ASCII values and the position index ensures keys with similar characters map to different buckets.
2.  **Efficient Collision Resolution:** Both chaining and open addressing allow the table to handle collisions without failing.

* * *

3.2 Walkthrough Example Without Collision[¶](#3.2-Walkthrough-Example-Without-Collision)
----------------------------------------------------------------------------------------

### **Example Input**[¶](#Example-Input)

Key: `"DOG"`  
Hash table size: (N = 10)

### **Step-by-Step Calculation**[¶](#Step-by-Step-Calculation)

1.  Calculate ASCII values:
    *   ( D = 68, O = 79, G = 71 )
2.  Apply the hash function: \[ \\text{hash}("DOG") = (68 \\times 1 + 79 \\times 2 + 71 \\times 3) \\mod 10 \] \[ = (68 + 158 + 213) \\mod 10 = 439 \\mod 10 = 9 \]
3.  Result: `"DOG"` maps to bucket **9**.

### **Hash Table State**[¶](#Hash-Table-State)

*   Initially: Empty table: `[[], [], [], [], [], [], [], [], [], []]`
*   After insertion of `"DOG"`: `[[], [], [], [], [], [], [], [], [], [DOG]]`

### **Conclusion**[¶](#Conclusion)

*   The key `"DOG"` is stored in bucket **9** without any collision.

* * *

3.3 Walkthrough Example With Collision[¶](#3.3-Walkthrough-Example-With-Collision)
----------------------------------------------------------------------------------

### **Example Input**[¶](#Example-Input)

Keys: `"DOG"` and `"BAT"`  
Hash table size: (N = 10)

### **Step-by-Step Calculation**[¶](#Step-by-Step-Calculation)

1.  Calculate the hash value for `"DOG"`:
    
    *   ( D = 68, O = 79, G = 71 ) \[ \\text{hash}("DOG") = (68 \\times 1 + 79 \\times 2 + 71 \\times 3) \\mod 10 = 439 \\mod 10 = 9 \]
    *   `"DOG"` maps to bucket **9**.
2.  Calculate the hash value for `"BAT"`:
    
    *   ( B = 66, A = 65, T = 84 ) \[ \\text{hash}("BAT") = (66 \\times 1 + 65 \\times 2 + 84 \\times 3) \\mod 10 = 448 \\mod 10 = 8 \]
    *   `"BAT"` maps to bucket **8**.
3.  Simulate a collision scenario:
    
    *   Assume another key `"GOD"` produces the same hash as `"DOG"` due to similar character values.
    *   ( \\text{hash}("GOD") = 439 \\mod 10 = 9 ), creating a collision in bucket **9**.

### **Collision Handling with Chaining**[¶](#Collision-Handling-with-Chaining)

*   Bucket 9 before collision: `[DOG]`
*   Insert `"GOD"` into the linked list in bucket 9.
*   Bucket 9 after collision: `[DOG -> GOD]`

### **Collision Handling with Open Addressing**[¶](#Collision-Handling-with-Open-Addressing)

1.  Attempt to insert `"GOD"` in bucket **9** (occupied by `"DOG"`).
2.  Perform linear probing: Check bucket **0** (next sequential index), which is empty.
3.  Insert `"GOD"` into bucket **0**.

### **Hash Table State**[¶](#Hash-Table-State)

*   After `"DOG"` and `"BAT"`: `[[], [], [], [], [], [], [], [], [BAT], [DOG]]`
*   After resolving collision with chaining: `[[], [], [], [], [], [], [], [], [BAT], [DOG -> GOD]]`
*   After resolving collision with open addressing: `[[GOD], [], [], [], [], [], [], [], [BAT], [DOG]]`

Section 4: Coding Challenge - OOP[¶](#Section-4:-Coding-Challenge---OOP)
========================================================================

4.1 Design a parent class called Planet[¶](#4.1----Design-a-parent-class-called-Planet)
---------------------------------------------------------------------------------------

In \[4\]:

class Planet:
    """
    A class to represent a planet in the solar system.
    """

    def \_\_init\_\_(self, name, distance\_from\_sun, planet\_type):
        """
        Initialize the attributes of the Planet class.
        
        :param name: str - Name of the planet
        :param distance\_from\_sun: int or float - Distance of the planet from the Sun (in million km)
        :param planet\_type: str - Type of the planet (e.g., terrestrial, gas giant)
        """
        self.name \= name
        self.distance\_from\_sun \= distance\_from\_sun  \# Distance in million km
        self.planet\_type \= planet\_type

    def get\_distance\_to\_earth(self):
        """
        Calculate the absolute distance to Earth (in kilometres).
        
        :return: dict - {'distance to earth': distance (in km)}
        """
        \# Convert distances to kilometres
        earth\_distance\_from\_sun \= 147000000  \# Earth's distance from the Sun in km
        planet\_distance\_in\_km \= self.distance\_from\_sun \* 1000000

        \# Calculate the absolute distance to Earth
        distance\_to\_earth \= abs(planet\_distance\_in\_km \- earth\_distance\_from\_sun)

        \# Return as a dictionary
        return {'distance to earth': distance\_to\_earth}

\# Example 
if \_\_name\_\_ \== "\_\_main\_\_":
    \# Create a planet object
    mars \= Planet(name\="Mars", distance\_from\_sun\=228, planet\_type\="terrestrial")

    \# Get the distance to Earth
    print(mars.get\_distance\_to\_earth())  \# Output: {'distance to earth': 81000000}

{'distance to earth': 81000000}

4.2 Design a child class called Mercury, which inherits from the Planet class[¶](#4.2----Design-a-child-class-called-Mercury,-which-inherits-from-the-Planet-class)
-------------------------------------------------------------------------------------------------------------------------------------------------------------------

In \[5\]:

class Mercury(Planet):
    """
    A class to represent the planet Mercury, inheriting from Planet.
    """

    @staticmethod
    def happy\_new\_year():
        """
        Print information about how long a year lasts on Mercury.
        """
        print("Happy New Year! A year on Mercury lasts 88 Earth days.")

\# Example 
if \_\_name\_\_ \== "\_\_main\_\_":
    \# Create a Mercury object
    mercury \= Mercury(name\="Mercury", distance\_from\_sun\=58, planet\_type\="terrestrial")

    \# Print the attributes of Mercury
    print(f"Name: {mercury.name}")
    print(f"Distance from Sun: {mercury.distance\_from\_sun} million km")
    print(f"Planet Type: {mercury.planet\_type}")

    \# Print the distance to Earth
    print(mercury.get\_distance\_to\_earth())  \# Output: {'distance to earth': 89000000}

    \# Call the happy\_new\_year method
    mercury.happy\_new\_year()  \# Output: Happy New Year! A year on Mercury lasts 88 Earth days.

Name: Mercury
Distance from Sun: 58 million km
Planet Type: terrestrial
{'distance to earth': 89000000}
Happy New Year! A year on Mercury lasts 88 Earth days.

4.3 Design a child class called Jupiter, which inherits from the Planet class[¶](#4.3----Design-a-child-class-called-Jupiter,-which-inherits-from-the-Planet-class)
-------------------------------------------------------------------------------------------------------------------------------------------------------------------

In \[9\]:

class Jupiter(Planet):
    """
    A class to represent Jupiter, inheriting from Planet.
    """

    def \_\_init\_\_(self):
        """
        Initialize the attributes specific to Jupiter.
        Inherits the attributes from the Planet class.
        """
        \# Jupiter's real-life properties
        super().\_\_init\_\_(name\="Jupiter", distance\_from\_sun\=779, planet\_type\="gas giant")
        self.number\_of\_moons \= 80  \# Jupiter has 80 moons

    @staticmethod
    def happy\_new\_year():
        """
        Static method to print out how long a year lasts on Jupiter.
        """
        print("Happy New Year from Jupiter! A year on Jupiter lasts 4,383 Earth days!")

\# Example Usage
if \_\_name\_\_ \== "\_\_main\_\_":
    \# Create an object of Jupiter
    jupiter \= Jupiter()

    \# Print the attributes of Jupiter
    print("Planet Name:", jupiter.name)
    print("Distance from Sun (in million km):", jupiter.distance\_from\_sun)
    print("Planet Type:", jupiter.planet\_type)
    print("Number of Moons:", jupiter.number\_of\_moons)

    \# Get the distance to Earth
    print(jupiter.get\_distance\_to\_earth())

    \# Call the static method
    jupiter.happy\_new\_year()

Planet Name: Jupiter
Distance from Sun (in million km): 779
Planet Type: gas giant
Number of Moons: 80
{'distance to earth': 632000000}
Happy New Year from Jupiter! A year on Jupiter lasts 4,383 Earth days!

In \[ \]: