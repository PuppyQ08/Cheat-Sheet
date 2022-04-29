1. L-Value R-Value
left and right of the equal sign

2. &vector is the address of the std::vector object
but &array is the memory address of the first item.
So if you want to pass in by void* which should be the pointer to the first item,
then you need to pass in &vector.front() or array.
