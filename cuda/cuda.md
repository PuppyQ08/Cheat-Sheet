# cudaMalloc format
why with 'cudaMalloc' you often write '(void**)&var', consider the following:

cudaMalloc allocates a memory on the GPU. The memory type it is referred is void* as it does not really care about the data type.

Once we have the address of that memory inside the 'cudaMalloc' we just allocated, we need to somehow return it to the caller. But all CUDA API functions are returning error codes (or success code) and any additional returned data has to be passed back by parameter reference.

C language has no pass-by-reference, so you actually need to pass a pointer to a variable where you want the function to store the result. Since you want to store a pointer value, you need to pass a pointer-to-pointer. Hence void** type.

If one wanted to encapsulate a malloc in similar way, one would write something like this:
'
void myMalloc(void** ret, size_t size) {
    void* mem = malloc(size);
    *ret = mem;
}
'
Now, if you pass '(void**)&var' to myMalloc, the function will be able to overwrite the value of the var --- as ret will be pointing to var variable.


# dynamic shared memory using extern
One possible reason that saving shared memory might be valuable, is because it can impact occupancy, and thus performance.

Suppose I had a parallel reduction code, and suppose that it used shared memory as the primary reduction medium. Typically the amount of shared memory I will need will be related to the number of threads I use in my threadblock. Now let's also suppose that depending on the exact problem I have, I may want to adjust the number of threads per threadblock, at runtime.

# Bank conflict
interleaved addressing has bank conflict but sequential addressing doesn't have.
Since:
Note that a bank is not the same thing as a word or location in shared memory. A bank refers collectively to all words in shared memory that satisfy a certain address pattern condition.

In general, shared memory bank conflicts can be avoided if all accesses from a warp (or half-warp in cc 1.x) go to separate banks. These accesses need not be in warp order, i.e. they can be scrambled, as long as the request from each thread targets a separate bank.

The above description covers every arrow in your diagram except those arrows pointing to bank 5.

If we had no other information, then multiple arrows targetting a single bank would indicate a potential bank conflict.

However, there is an exception, when not only are the accesses targetting the same bank, but they are targetting the same word in memory. When multiple shared memory requests target the same word in memory, then the shared memory system has a broadcast mechanism to take the data contained in that word, and service it to all the requesting threads, in a single cycle.

# Block size 
It would be better is 2**n threads per blocks, since you may want have stride/2 in the reduction.

# GPU structure 
[See details](https://docs.nvidia.com/cuda/parallel-thread-execution/index.html#ptx-machine-model)


# Coalesced memory access
Memory requests from a warp are handled together.
When memory requests from the threads of a warp are sequential,
the memory requests can be combined into fewer
transactions. These kind of accesses are called coalesced memory accesses.
