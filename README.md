<h3 align="center">KV.JS</h3>
<p align="center">Advanced in-memory caching module for JavaScript. Inspired by Redis.</p>
<hr>

KV.JS is a fast, in-memory data store written in pure JavaScript, heavily inpired by Redis. It is capable of handling multiple data types, including strings, lists, sets, sorted sets, hashes, and geospatial indexes. Additionally, with more than 140 functions, KV.JS provides a vast variety of operations, ranging from `SET`, `GET`, `EXPIRE`, `DEL` to `INCR`, `DECR`, `LPUSH`, `RPUSH`, `SADD`, `SREM`, `HSET`, `HGET`, and many many more.

## Installation
```bash
npm install @heyputer/kv.js
```

## Usage
```javascript
const kvjs = require('@heyputer/kv.js');

// Create a new kv.js instance
const kv = new kvjs();

// Set a value
kv.set('foo', 'bar');

// Get a value
const value = kv.get('foo');

console.log(value); // "bar"

// Delete a value
kv.del('foo');
```
## API

<details>
  <summary><strong><code>set</code></strong></summary>

  ```javascript
  // Set a basic key-value pair
  kv.set('username', 'john_doe'); // Output: 'OK'

  // Set a key-value pair only if the key does not already exist (NX option)
  kv.set('username', 'jane_doe', ['NX']);

  // Set a key-value pair only if the key already exists (XX option)
  kv.set('email', 'jane@example.com', ['XX']);

  // Set a key-value pair with an expiration time in seconds (EX option)
  kv.set('session_token', 'abc123', ['EX', 3600]);

  // Get the existing value and set a new value for a key (GET option)
  kv.set('username', 'mary_smith', ['GET']);

  // Set a key-value pair with an expiration time in milliseconds (PX option)
  kv.set('temp_data', '42', ['PX', 1000]);

  // Set a key-value pair with an expiration time at a specific Unix timestamp in seconds (EXAT option)
  kv.set('event_data', 'event1', ['EXAT', 1677649420]);

  // Set a key-value pair with an expiration time at a specific Unix timestamp in milliseconds (PXAT option)
  kv.set('event_data2', 'event2', ['PXAT', 1677649420000]);

  // Set a key-value pair and keep the original TTL if the key already exists (KEEPTTL option)
  kv.set('username', 'alice_wonder', ['KEEPTTL']);

  // Set a key-value pair with multiple options (NX, EX, and GET options)
  kv.set('new_user', 'carol_baker', ['NX', 'EX', 7200, 'GET']);
  ```
</details>

<details>
  <summary><strong><code>get</code></strong></summary>
  
  ```javascript
  // Example 1: Get the value of an existing key
  kv.get('username'); // Returns the value associated with the key 'username'

  // Example 2: Get the value of a non-existent key
  kv.get('nonexistent'); // Returns null

  // Example 3: Get the value of an expired key (assuming 'expiredKey' was set with an expiration)
  kv.get('expiredKey'); // Returns null

  // Example 4: Get the value of a key after updating its value
  kv.set('color', 'red'); // Sets the key 'color' to the value 'red'
  kv.get('color'); // Returns 'red'

  // Example 5: Get the value of a key after deleting it (assuming 'deletedKey' was previously set)
  kv.delete('deletedKey'); // Deletes the key 'deletedKey'
  kv.get('deletedKey'); // Returns null
  ```
</details>

<details>
  <summary><strong><code>get</code></strong></summary>
  
  ```javascript
  // Example 1: Get the value of an existing key
  kv.get('username'); // Returns the value associated with the key 'username'

  // Example 2: Get the value of a non-existent key
  kv.get('nonexistent'); // Returns null

  // Example 3: Get the value of an expired key (assuming 'expiredKey' was set with an expiration)
  kv.get('expiredKey'); // Returns null

  // Example 4: Get the value of a key after updating its value
  kv.set('color', 'red'); // Sets the key 'color' to the value 'red'
  kv.get('color'); // Returns 'red'

  // Example 5: Get the value of a key after deleting it (assuming 'deletedKey' was previously set)
  kv.delete('deletedKey'); // Deletes the key 'deletedKey'
  kv.get('deletedKey'); // Returns null
  ```
</details>

<details>
  <summary><strong><code>get</code></strong></summary>

  ```javascript
  // Delete a single key ("key1"), returns 1 if the key was deleted, 0 if it did not exist or has expired.
  kv.del("key1");

  // Delete multiple keys ("key2" and "key3"), returns the number of keys deleted (0, 1, or 2) depending on which keys existed and were not expired.
  kv.del("key2", "key3");

  // Attempt to delete a non-existent key ("nonExistentKey"), returns 0 since the key does not exist.
  kv.del("nonExistentKey");

  // Attempt to delete an expired key ("expiredKey"), returns 0 if the key has expired.
  kv.del("expiredKey");

  // Delete multiple keys ("key4", "key5", "key6"), returns the number of keys deleted (0 to 3) depending on which keys existed and were not expired.
  kv.del("key4", "key5", "key6");
  ```
</details>

<details>
  <summary><strong><code>get</code></strong></summary>

  ```javascript
  // Check if a single key ("key1") exists, returns 1 if the key exists and is not expired, 0 otherwise.
  kv.exists("key1");

  // Check if multiple keys ("key2" and "key3") exist, returns the number of existing keys (0, 1, or 2) that are not expired.
  kv.exists("key2", "key3");

  // Check if a non-existent key ("nonExistentKey") exists, returns 0 since the key does not exist.
  kv.exists("nonExistentKey");

  // Check if an expired key ("expiredKey") exists, returns 0 if the key has expired.
  kv.exists("expiredKey");

  // Check if multiple keys ("key4", "key5", "key6") exist, returns the number of existing keys (0 to 3) that are not expired.
  kv.exists("key4", "key5", "key6");
  ```
</details>