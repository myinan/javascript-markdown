# Hash Table / HashMap Data Structure
## `Hash Table`
A hash table is a data structure that allows for efficient insertion, deletion, and retrieval of values based on a key. It uses a hash function to map keys to indices in an array, allowing for constant-time average-case complexity for basic operations. Hash tables are widely used in computer science and programming due to their fast and efficient nature.

### Basic Components of a Hash Table:

1. **Hash Function:**
   - A hash function takes a key and produces a hash code, which is used as an index to store and retrieve the associated value. The goal is to distribute keys uniformly across the array.

2. **Array:**
   - The underlying data structure used to store key-value pairs. Each index in the array is often referred to as a "bucket."

### Hash Table Operations:

1. **Insert (or Set):**
   - The key and its associated value are hashed, and the value is stored in the corresponding bucket.

2. **Retrieve (or Get):**
   - The key is hashed, and the corresponding bucket is checked to retrieve the associated value.

3. **Delete:**
   - The key is hashed, and the value associated with that key is removed from the hash table.

### Collision Handling:

A collision occurs when two keys hash to the same index. Various techniques are used to handle collisions:

1. **Separate Chaining:**
   - Each bucket in the array contains a linked list or another data structure to handle multiple values that hash to the same index.

2. **Open Addressing:**
   - When a collision occurs, the algorithm searches for the next available slot in the array (probing). This can be done using techniques like linear probing, quadratic probing, or double hashing.

### Implementation in JavaScript:

Here's a basic example of a hash table implementation in JavaScript using separate chaining:

```javascript
class HashTable {
  constructor(size = 100) {
    this.size = size;
    this.buckets = new Array(size).fill(null).map(() => []);
  }

  hash(key) {
    let hash = 0;
    for (let i = 0; i < key.length; i++) {
      hash += key.charCodeAt(i);
    }
    return hash % this.size;
  }

  set(key, value) {
    const index = this.hash(key);
    const bucket = this.buckets[index];

    for (const pair of bucket) {
      if (pair[0] === key) {
        // Update value if key already exists
        pair[1] = value;
        return;
      }
    }

    // Insert a new key-value pair
    bucket.push([key, value]);
  }

  get(key) {
    const index = this.hash(key);
    const bucket = this.buckets[index];

    for (const pair of bucket) {
      if (pair[0] === key) {
        return pair[1];
      }
    }

    return null; // Key not found
  }

  delete(key) {
    const index = this.hash(key);
    const bucket = this.buckets[index];

    for (let i = 0; i < bucket.length; i++) {
      if (bucket[i][0] === key) {
        // Remove key-value pair from the bucket
        bucket.splice(i, 1);
        return;
      }
    }
  }
}
```

### Usage:

```javascript
let myHashTable = new HashTable();

myHashTable.set('name', 'John');
myHashTable.set('age', 25);
myHashTable.set('city', 'New York');

console.log(myHashTable.get('name')); // Output: John
console.log(myHashTable.get('age'));  // Output: 25

myHashTable.delete('age');
console.log(myHashTable.get('age'));  // Output: null (key not found)
```

Hash tables are commonly used in JavaScript for various purposes, including implementing object maps and sets, managing caches, and optimizing search and retrieval operations in applications. The native JavaScript `Map` and `Set` objects are examples of hash table implementations provided by the language.

### JS `Map` and `Set` objects
The `Map` and `Set` objects are native data structures introduced in ECMAScript 2015 (ES6) and later versions of JavaScript. They provide efficient ways to manage collections of values and keys, and under the hood, they are implemented using hash tables or similar structures.

### `Map` Object:

#### Usage:
```javascript
// Creating a Map
let myMap = new Map();

// Adding key-value pairs
myMap.set('name', 'John');
myMap.set('age', 25);

// Retrieving values
console.log(myMap.get('name')); // Output: John

// Checking if a key exists
console.log(myMap.has('age'));   // Output: true

// Deleting a key-value pair
myMap.delete('age');

// Iterating over key-value pairs
for (let [key, value] of myMap) {
  console.log(`${key}: ${value}`);
}
```

#### Key Features:
- **Any Data Type as Key:**
  - Unlike plain objects, `Map` allows you to use any data type (including objects and functions) as keys.

- **Order of Insertion Preserved:**
  - The order of key-value pairs is preserved, making it suitable for scenarios where the order of insertion matters.

- **Size Property:**
  - You can easily get the size of the `Map` using the `size` property.

### `Set` Object:

#### Usage:
```javascript
// Creating a Set
let mySet = new Set();

// Adding values
mySet.add(1);
mySet.add('apple');

// Checking if a value exists
console.log(mySet.has(1));       // Output: true

// Deleting a value
mySet.delete('apple');

// Iterating over values
for (let value of mySet) {
  console.log(value);
}
```

#### Key Features:
- **Uniqueness:**
  - A `Set` only allows unique values, making it useful for scenarios where you want to ensure a collection of distinct elements.

- **No Key-Value Pairs:**
  - Unlike `Map`, `Set` does not store key-value pairs; it only stores values.

- **Size Property:**
  - Similar to `Map`, you can get the size of the `Set` using the `size` property.

### Commonalities:

- Both `Map` and `Set` offer methods to clear all entries (`clear()`), check if they are empty (`size === 0`), and provide iterable methods (`forEach`, `entries`, `keys`, `values`).

- Both `Map` and `Set` are iterable, allowing you to use them with `for...of` loops.

- `Map` and `Set` objects are part of the ECMAScript standard, and they are widely supported in modern JavaScript environments.

In summary, `Map` is suitable for scenarios where you need to associate keys with values, while `Set` is useful when you want to maintain a collection of unique values. Their efficient implementations make them go-to choices for various tasks in JavaScript development.

## Hashing Algorithms (Hash functions (e.g., SHA-256, MD5))
Hashing algorithms are fundamental components of computer science and information security. They play a crucial role in various applications, including data integrity verification, password storage, digital signatures, and more. Here's a detailed explanation of hashing algorithms:

### 1. **Definition:**
A hashing algorithm is a mathematical function that takes an input (or 'message') and produces a fixed-size string of characters, which is typically a hash value or digest. The output, known as the hash code, is unique to the input data, meaning even a small change in the input should result in a significantly different hash.

### 2. **Key Characteristics:**
   - **Deterministic:** The same input will always produce the same hash.
   - **Efficient:** The hashing process should be fast and not computationally expensive.
   - **Irreversible:** It should be computationally infeasible to reverse the process and obtain the original input from the hash.
   - **Fixed Output Size:** Regardless of the input size, the hash function produces a fixed-size output.
   - **Avalanche Effect:** A small change in the input data should result in a significantly different hash value. This property ensures that similar inputs don't produce similar hash outputs.
   - **Collision Resistance:** It should be computationally infeasible to find two different inputs that produce the same hash value. Collisions weaken the security of hash functions.

### 3. **Common Hashing Algorithms:**
   - **MD5 (Message Digest Algorithm 5):**<br>
      + MD5 was popular in the past but is now considered insecure for cryptographic purposes due to vulnerabilities that allow for collision attacks.
      + It produces a fixed-size 128-bit (16-byte) hash value.
      + Despite its insecurity, MD5 is still used in non-cryptographic applications, such as checksums for file integrity.
   - **SHA-1 (Secure Hash Algorithm 1):** Deprecated due to vulnerabilities. It produces a 160-bit hash.
   - **SHA-256, SHA-384, SHA-512 (Secure Hash Algorithms):** Part of the SHA-2 family, widely used for security. They produce hash values of 256, 384, and 512 bits, respectively.
   - **bcrypt, scrypt, Argon2:** Specifically designed for password hashing, they incorporate techniques to slow down brute-force attacks.

### 4. **Applications:**
   - **Data Integrity:** Hashing is used to verify the integrity of data during transmission. If the received hash matches the computed hash, the data is likely intact.
   - **Digital Signatures:** Hash functions are an integral part of digital signatures, ensuring the authenticity and integrity of the signed data.
   - **Password Storage:** Hashing is used to store passwords securely. Instead of storing plain-text passwords, systems store the hash values, making it difficult for attackers to retrieve the original passwords.
   - **Hash Tables:** In computer science, hash functions are employed in hash tables to quickly locate a data record, given its search key.

### 5. **Collision and Security:**
   - **Collision:** When two different inputs produce the same hash output. Avoiding collisions is crucial for the effectiveness of hashing algorithms.
   - **Security:** A secure hash function should be resistant to collision attacks, pre-image attacks, and second pre-image attacks.

### 6. **Cryptographic Hash Functions:**
   - Cryptographic hash functions are a subset designed for use in security applications. They meet additional criteria, such as being resistant to various attacks.

### 7. **Example (SHA-256):**
   - If you input the string "Hello, World!" into a SHA-256 hash function, you'll get a fixed-size (256-bit) hexadecimal hash like `a591a6d40bf420404a011733cfb7b190d62c65bf0bcda32b57b277d9ad9f146e`.

### 8. **Secure Implementation:**
   - Always use established and well-reviewed hashing algorithms.
   - Utilize techniques like salting for password storage to add an extra layer of security.

It's important to choose the appropriate hashing algorithm based on the specific requirements of the application. For security-sensitive applications, SHA-256 or other members of the SHA-2 family are recommended due to their resistance to current cryptographic attacks.

### Knowledge Check

**Q1.** What does it mean to hash?

**A1.** Hashing involves taking an input in and generating a corresponding output. A hash function should be a pure function. Hashing the same input should always return the same hash code, and there should be no random generation component. For example, let’s look at a hashing function that takes a name and gives us the first letter of that name:

```js
function hash(name) {
  return name.charAt(0);
}
```

We created a basic hashing function.

There is a key difference between hashing and ciphering (encryption): reversibility. Hashing is a one-way process. Using the above example, you can make a hash code from a name, but you cannot take a hash code and revert it back to a name. If you have a name "Carlos", we can hash it to "C". But it’s impossible to reverse it from "C" back to its original form. You cannot know if it’s "Carlos", maybe it’s "Carla" or "Carrot". We don’t know.

You might have spotted a problem: what if our school is populated with many people whose names share the same first letter C? Then we will have a directory labeled C that holds too many names while other directories could be empty. To eliminate this duplication and better separate our students, we need to rework our hash function.

```js
function hash(name, surname) {
  return name.charAt(0) + surname.charAt(0);
}
```

Instead of just taking the first name letter, we take the first name and last name letters. "Carlos Smith" will have a hash code of "CS". This will spread our students among more directories and will eliminate many duplicate hash codes from being generated.

But it still doesn’t solve our problem. What if we have a common combination of first letters in students’ names? Then we will still have an imbalance in the size of the directories. We need to make it easier to find the person we’re looking for, so let’s rework our hash code.

```js
function stringToNumber(string) {
  let hashCode = 0;
  for (let i = 0; i < string.length; i++) {
    hashCode += string.charCodeAt(i);
  }

  return hashCode;
}

function hash(name, surname) {
  return stringToNumber(name) + stringToNumber(surname);
}
```

We not only consider the first letters with this technique. Instead, we take the entire name and convert it into numbers.

You might be thinking, wouldn’t it be just better to save the whole name as a hash code? That is true. This would make it unique for each name, but in the context of hash maps, we need the hash code to be a number. This number will serve as the index to the bucket that will store the key value pair.

**Q2.** What are buckets?

**A2.** Buckets are storage that we need to store our elements. Simply, it’s an array. For a specific key, we decide which bucket to use for storage through our hash function. The hash function returns a number that serves as the index of the array at which we store this specific key value pair.Let’s say we need to store a key “Fred”:

1. Pass “Fred” into the hash function to get the hash code which is 508.
2. Find the bucket at index 508.
3. Store the key value pair in that bucket.

This is an oversimplified explanation; we’ll discuss more internal mechanics later.

To get a value using a key, we put each entry inside a bucket as a Node item, which holds both the key and the value. To retrieve the value, we hash the key and calculate its bucket number. If the bucket is not empty, then we go to that bucket and compare if the Node’s key is the same key that is already in the bucket. If it is, then we can return the Node’s value. Otherwise, we return null.

Maybe you are wondering, why are we comparing the keys if we already found the index of that bucket? Remember, a hash code is just the location. Different keys might generate the same hash code. We need to make sure the key is the same by comparing both keys that are inside the bucket.

This is it, making this will result in a hash table with has, set and get.

What if we found the hash code, but also the key value is the same as what we already have in the bucket? We check if it’s the same item by comparing the keys, then we overwrite the value with our new value.

A hash map does not guarantee insertion order when you iterate over it. The translation of hash codes to indexes does not follow a linear progression from the first to the last index. Instead, it is more unpredictable, irrespective of the order in which items are inserted. That means if you are to retrieve the array of keys and values to iterate over them, then they will not be in order of when you inserted them.

Some libraries implement hash tables with insertion order in mind such as JavaScript’s own `Map`.

**Q3.** What is a collision?

**A3.**  A collision occurs when two different keys generate the exact same hash code. Because they have the same hash code, they will land in the same bucket.

Let’s take an example: hashing the name "Sara" and the name "raSa" will generate the same hash code. That is because the letters in both names are the same, just arranged differently. We can rework our stringToNumber function so that it can give us unique hash codes that depend on where the letters appear in the name using an algorithm.

```js
function stringToNumber(string) {
  let hashCode = 0;

  const primeNumber = 31;
  for (let i = 0; i < string.length; i++) {
    hashCode = primeNumber * hashCode + string.charCodeAt(i);
  }

  return hashCode;
}
```

With our new function we will have different hash codes for the names "Sara" and "raSa". This is because even if both names have the same letters, some of the letters appear in different locations. The hash code started to change because we are multiplying the old hash with every new iteration and then adding the letter code.

Notice the usage of a prime number. We could have chosen any number we wanted, but prime numbers are preferable. Multiplying by a prime number will reduce the likelihood of hash codes being evenly divisible by the bucket length, which helps minimize the occurrence of collisions.

Even though we reworked our hash function to avoid the "Sara"/"raSa" collision, there is always the possibility for collisions. Since we have a finite number of buckets, there is no way to eliminate collisions entirely. Let’s try to minimize them.

#### Dealing with collisions
Up until now, our hash map is a one-dimensional data structure. What if each Node inside the bucket can store more than one value? Enter Linked Lists. Now, each bucket will be a Linked List. When inserting into a bucket, if it’s empty, we insert the head of Linked List. If a head exists in a bucket, we follow that Linked List to add to the end of it.

**Q4.** When is it a good time to grow our table?

**A4.** We don’t have infinite memory, so we can’t have the infinite number of buckets. We need to start somewhere, but starting too big is also a waste of memory if we’re only going to have a hash map with a single value in it. So to deal with this issue, we should start with a small array for our buckets. We’ll use an array size 16.

Most programming languages start with the default size of 16 because it’s a power of 2, which helps with some techniques for performance that require bit manipulation for indexes.

How are we going to insert into those buckets when our hash function generates big numbers like 20353924? We make use of the modulo % operation, given any number modulo by 16 we will get a number between 0 and 15.

As we continue to add nodes into our buckets, collisions get more and more likely. Eventually, however, there will be more nodes than there are buckets, which guarantees a collision.

Remember we don’t want collisions. In a perfect world each bucket will either have 0 or 1 Node only, so we grow our buckets to have more chance that our Nodes will spread and not stack up in the same buckets. To grow our buckets, we create a new buckets list that is double the size of the old buckets list, then we copy all nodes over to the new buckets.

#### When do we know that it’s time to grow our buckets size?
To deal with this, our hash map class needs to keep track of two new fields, the capacity and the load factor.

+ The capacity is the total number of buckets we currently have. Keeping track of this will let us know if our map has reached a certain threshold aka load factor,

+ The load factor is a number that we can assign our hash map to at the start. It’s the factor that will determine when it is a good time to grow our buckets. For example, a load factor of 0.75 means our hash map will need to grow its buckets when the capacity reaches 75% full. Setting it too low will consume too much memory by having too many empty buckets, while setting it too high will allow our buckets to have many collisions before we grow them. Hash map implementations across various languages use a load factor between 0.75 and 1.
