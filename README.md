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

## ErrorBits stack_destructor(Stack *stack) 

- 1. stack pointer is nullptr or invalid ptr
- 2. stack_destructor() is called more than one time for one stack
- 3.

ii. doesn't call free more than one time, prints error info in log file ("Invalid data pointer");

## void stack_dump(Stack *stack, ErrorBits error, FILE *stream)

As stack_dump() is not static user can call it.
The program could stop working (by segfault) in case stack data is nullptr (stack_dump() refers to stack data elements).
```sh
int main() 
{
    open_log("nlog.txt");
    FILE *log_file = fopen ("nlog.txt", "w");
    Stack stk = {};
    
    stack_constructor (&stk, 10);
    stack_push (&stk, 2);
    
    stk.capacity  = 100000;
    stk.data = nullptr;
    stack_dump (&stk, 0, log_file); 
    putchar ('t');
    
    fclose (log_file);
    close_log();

    stack_destructor (&stk);

    return 0;
}
```

(the program is stopped by segfault, 't' is not printed)
