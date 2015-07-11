primesieve-python
=================
[![Build Status](https://travis-ci.org/hickford/primesieve-python.svg?branch=master)](https://travis-ci.org/hickford/primesieve-python)

Python bindings for the [primesieve](http://primesieve.org/) C++ library. Generates primes orders of magnitude faster than any pure Python code. Features:

* Generate a list of primes
* Count primes and [prime k-tuplets](https://en.wikipedia.org/wiki/Prime_k-tuple)
* Print primes and prime k-tuplets
* Find the nth prime
* Iterate over primes using little memory

Motivation
----------

I enjoy algorithm problems such as those in [Google Code Jam](https://code.google.com/codejam) and [Project Euler](https://projecteuler.net/). Many pertain to number theory. It's important (and fun) to write your own prime finding code once, but it's also useful to have a fast, reliable library.

Two of my favourite problems: Google Code Jam [*Expensive Dinner*](https://code.google.com/codejam/contest/dashboard?c=1150486#s=p2) and Project Euler [Problem 500](https://projecteuler.net/problem=500)

Installation
------------

[![PyPI](https://img.shields.io/pypi/v/primesieve.svg)](https://pypi.python.org/pypi/primesieve)

From [PyPI](https://pypi.python.org/pypi/primesieve)

    pip install primesieve

Usage
-----

The syntax of the primesieve Python bindings is nearly identical to the
syntax of the primesieve C++ library.

```Python
>>> from primesieve import *

# Generate a list of the primes below 40
>>> generate_primes(40)
[2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37]

# Generate a list of the primes between 100 and 120
>>> generate_primes(100, 120)
[101, 103, 107, 109, 113]

# Generate a list of the first 10 primes
>>> generate_n_primes(10)
[2, 3, 5, 7, 11, 13, 17, 19, 23, 29]

# Generate a list of the first 10 starting at 1000
>>> generate_n_primes(10, 1000)
[1009, 1013, 1019, 1021, 1031, 1033, 1039, 1049, 1051, 1061]

# Get the 10th prime
>>> nth_prime(10)
29

# Count the primes below 10**9
>>> count_primes(10**9)
50847534
```

Here is a [list of all available functions](primesieve/cpp_primesieve.pxd).

Iterating over primes
---------------------

Instead of generating a large list of primes and then do something with
the primes it is also possible to simply iterate over the primes which uses
less memory.

```Python
>>> import primesieve
it = primesieve.Iterator()

# Iterate over the primes below 10000
while True:
    prime = it.next_prime()
    if prime > 10000:
        break
    print prime

# Set iterator start number to 100
it.skipto(100)

# Iterate backwards over the primes below 100
while prime > 2:
    prime = it.previous_prime()
    print prime
```

Multi-threading
---------------

Counting primes and prime k-tuplets and finding the nth prime can be done in parallel using multiple threads, just use the ```parallel_``` prefix and primesieve will use all your CPU cores.

```Python
>>> from primesieve import *

# Count the primes below 10**11 using all CPU cores
>>> parallel_count_primes(10**11)
4118054813

# Find the 10**10th prime using all CPU cores
>>> parallel_nth_prime(10**10)
252097800623
```

Development
-----------

1. Install Cython `pip install cython`
2. Clone this repo `git clone --recursive https://github.com/hickford/primesieve-python && cd primesieve-python`
3. Install `pip install . --upgrade` (builds primesieve C++ library and Python extension)
4. Test `py.test`

### Windows build

[![Build status](https://ci.appveyor.com/api/projects/status/4chekgdj7bqx4ivt/branch/master?svg=true)](https://ci.appveyor.com/project/hickford/primesieve-python/branch/master)
