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


