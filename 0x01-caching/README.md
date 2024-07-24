# 0x01. Caching

This repository contains solutions for the caching project. The project explores various caching algorithms and their implementations in Python.

## Background Context

Caching is a technique used to store and manage data temporarily in a cache, allowing for faster access to frequently used data. Different caching algorithms determine how data is stored and replaced within the cache. This project covers several caching algorithms, including FIFO, LIFO, LRU, MRU, and LFU.

## Resources

- [Cache replacement policies - FIFO](https://en.wikipedia.org/wiki/Cache_replacement_policies#First-in,_first-out_(FIFO))
- [Cache replacement policies - LIFO](https://en.wikipedia.org/wiki/Cache_replacement_policies#Last_in_first_out_(LIFO))
- [Cache replacement policies - LRU](https://en.wikipedia.org/wiki/Cache_replacement_policies#Least_recently_used_(LRU))
- [Cache replacement policies - MRU](https://en.wikipedia.org/wiki/Cache_replacement_policies#Most_recently_used_(MRU))
- [Cache replacement policies - LFU](https://en.wikipedia.org/wiki/Cache_replacement_policies#Least_frequently_used_(LFU))

## Learning Objectives

By the end of this project, you should be able to explain the following concepts:

### General

- What a caching system is and how it works.
- The purpose of a caching system in computing.
- Different caching algorithms:
  - **FIFO (First In, First Out):** A cache replacement policy that removes the oldest items first.
  - **LIFO (Last In, First Out):** A cache replacement policy that removes the most recently added items first.
  - **LRU (Least Recently Used):** A cache replacement policy that removes the least recently used items.
  - **MRU (Most Recently Used):** A cache replacement policy that removes the most recently used items.
  - **LFU (Least Frequently Used):** A cache replacement policy that removes the least frequently used items.
- The limitations of a caching system, such as cache size and eviction policies.

## Requirements

### Python Scripts

- All files will be interpreted/compiled on Ubuntu 18.04 LTS using Python 3.7.
- All files should end with a new line.
- The first line of all files should be exactly `#!/usr/bin/env python3`.
- A `README.md` file, at the root of the folder of the project, is mandatory.
- Code should use the `pycodestyle` style (version 2.5).
- All files must be executable.
- The length of your files will be tested using `wc`.
- All modules should have documentation: `python3 -c 'print(__import__("my_module").__doc__)'`.
- All classes should have documentation: `python3 -c 'print(__import__("my_module").MyClass.__doc__)'`.
- All functions (inside and outside a class) should have documentation: `python3 -c 'print(__import__("my_module").my_function.__doc__)'` and `python3 -c 'print(__import__("my_module").MyClass.my_function.__doc__)'`.
- Documentation is required for all modules, classes, and functions, explaining their purpose.

## More Info

### Parent Class: `BaseCaching`

All custom caching classes must inherit from the `BaseCaching` class provided below:

```python
#!/usr/bin/python3
""" BaseCaching module
"""

class BaseCaching():
    """ BaseCaching defines:
      - constants of your caching system
      - where your data are stored (in a dictionary)
    """
    MAX_ITEMS = 4

    def __init__(self):
        """ Initialize
        """
        self.cache_data = {}

    def print_cache(self):
        """ Print the cache
        """
        print("Current cache:")
        for key in sorted(self.cache_data.keys()):
            print("{}: {}".format(key, self.cache_data.get(key)))

    def put(self, key, item):
        """ Add an item in the cache
        """
        raise NotImplementedError("put must be implemented in your cache class")

    def get(self, key):
        """ Get an item by key
        """
        raise NotImplementedError("get must be implemented in your cache class")

