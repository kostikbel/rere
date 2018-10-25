This is the Realtek vendor driver for re(4)/FreeBSD with some modifications I had to make to allow the router to stay up more that 1 week.

Main issue is the unconditional use of the 9k jumbo clusters regardless of the configured MTU.  After sufficient fragmentation of the physical memory, new allocations are impossible and machine hangs in contigmalloc() looping for rx ring mbuf refill, and other processes stuck in lock cascade for the re driver lock.
