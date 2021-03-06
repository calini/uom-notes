How to build a cache
---

Prev lecture [TODO: Del this, move to lecture 1]

* Computing tech trends, challenges & some solutions
* Rapid increase of processing power
* Slow increase of memory access capability
* Memory wall
* Solution: **Caches**, out of order execution, prefetching, compiler optimisations, etc.
* No silver bullet...


Core concepts behind caches:



Test:

* Cache behaviour
* Parameters
* Limits

Learn:

* How the cache works
* How memory accesses are handled
* What inhibits the cache's behaviour

Understand:

* Importance of caches
* How to avoid inefficient patterns
* How to write, optimise programs
* How cache is structured
* How it operates (CPU reads, CPU writes0
* Key cache performance parameters
* Making cache more efficient

when CPU does a ```LDR R0 [0x01234567]``` there is a parallel check on the cache 

**Cache hit**: When the CPU requests some memory address and it's found in the cache

#### Temopral locality:

* Things recently used will likely be used again soon
* eg. instructions and data in loops

#### Spacial locality:

* Things close together in store are often used together
* eg. instructions or array elements

**Hit Rate**: Fraction of cache accesses which "hit" in cache

* Hit rates for instructions usually better than for data

**Cache misses**: Temporal locality tells us it's a good idea to cache it

* Put new value in cache (Spacial locality -> maybe store more)
* If cache is full we evict some of it

**LRU** (Least recently used)

* Makes sense
* Expensive to implement (in hardware)
* 

**Round robin** (or cyclic)

* Cycle round locations
* Least recently fetched from memory

**Random**

* Easy to implement
* Not as bad as it might seem



Writes are slightly more complex

* Must do an address comparison first to see if address is in cache
* Cache hit
	* Update value in cache
	* Update in RAM?

Write Through = Every cache write is also done to memory
Write Through with buffers
Copy back = Write to cache, only update to RAM when evicted

**Cache miss on write** 

* Allocate
	* Find a location
	* Assign cache location
	* Write through back to RAM

* Write around (???)

....


Fastest is Write Allocate / Copy Back

But cache & main memory are not "coherent"

Does it matter?

* I/O devices
* Exceptions
* Multi-processors

May need special handling (later)


We want fully associative achce!

* It's expensive
* Need to store full 32 bit addresses
* Hardware comparison is expensive (logic) and uses power

It is possible toacheive small and fast (usually static) RAM
memory in special ways

Few real processor caches are fully associative


### Set associative cache

* A compromise!
* A set associative cache is simply a small number (2 or 4) of direct mapped caches operating in parallel
* If one matches, we have a hit 