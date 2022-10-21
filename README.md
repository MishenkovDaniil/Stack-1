# Review on stack program

## ErrorBits stack_constructor(Stack *stack, StackSize capacity);

checked next items
- 1. capacity is zero
- 2. capacity is negative number
- 3. function is not used before calling stack_push or stack_pop
- 4. stack pointer is invalid
- 5. capacity is too big

In all cases program puts error info in log file ("invalid capacity" in last case and "wrong struct canary" in others).
FIND NO BUGS

## ErrorBits stack_push(Stack *stack, Object object);

- stack pointer is nullptr or invalid ptr

In first case prints next info (WITHOUT ERROR CODE): "ErrorBits stack_push(Stack*, Object) at another_stack_stack.cpp(193)";


## ErrorBits stack_pop(Stack *stack, Object *object);


- 1. stack pointer is nullptr or invalid ptr
- 2. stack_pop() is called when nothing is in stack
- 3.

ii. - stack_pop stops and returns error_code, the program works as stack_pop wasn't called at all;
