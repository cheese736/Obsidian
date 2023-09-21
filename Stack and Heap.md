# Stack
The stack memory is a linear data structure, which means that it is stored sequentially. When we call a function, the function and the varaibles inside that function are stored in stack memory. Stack memory is allocated and deallowcated automatically for us. But what does that mean?

Well, our machine will assign it as needed and then remove it when it's no longer needed, and we don't have to worry about it. For instance, when we call a function, the variables in that function are automatically in scope. That is the memory being allocated. Then, when the function is complete, the variables in that funcion fall out of scope. That is the memory being deallocated. We don't need to tell the stack memory to add or remove these variables - it will take care of that for us.

Stack memeory is much faster than heap memory. One downside of stack memory, though, is that it's much smaller than heap memory, and if we're not careful, we can end up with a stack overflow, especially if we are calling functions recursively.

# Heap
On the other hand, heap memory is a hierarchical data structure. It's not store sequentially - instead, it's store in relation to other data. This is where dynamic variables such as global variables are stored.
Also, a low-level language like C can manually allocate variables to the heap. It's slower than stack memory because there's no easy way to just grab values from the heap, unlike with stack
