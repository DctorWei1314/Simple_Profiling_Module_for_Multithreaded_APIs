# Simple_Profiling_Module_for_Multithreaded_APIs
HI,this is a simple profiling module for analysis other programs by the following the rules to change your multithread api code,

take this famous allocator API [Doug Lea Malloc](http://g.oswego.edu/dl/html/malloc.html)   for a example:
```markdown
**#include <APIProfiler.hpp>**//code you should add here

**DEFINE_API_PROFILER(dlmalloc);**//code you should add here

void* dlmalloc(size_t bytes)
{

   **API_PROFILER(dlmalloc);**//code you should add here
#if USE_LOCKS
    ensure_initialization();
#endif

    if (!PREACTION(gm))
    {
        void* mem;
        size_t nb;
        if (bytes <= MAX_SMALL_REQUEST)
        {
            ...
 ```
 here is a console result for multithread to call the allocator API with such a profiling module:
 ```markdown
TID 0x13bc time spent in "dlmalloc": 7/1001 ms 0.7% 6481x
TID 0x1244 time spent in "dlmalloc": 6/1000 ms 0.6% 6166x
TID 0x198 time spent in "dlmalloc": 0/3072 ms 0.0% 2x
TID 0x11d0 time spent in "dlmalloc": 0/1113 ms 0.0% 6x
TID 0x12a4 time spent in "dlmalloc": 0/1000 ms 0.0% 20x
TID 0xc14 time spent in "dlmalloc": 4/1011 ms 0.4% 3243x
 ```
 you are pleased to change the related "QueryPerformanceFrequency" windows API to Migrate to another environment.
 or you can use the c++11 standard lib for a portable new one.
