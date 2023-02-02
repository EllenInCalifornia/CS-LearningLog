# Lead-in swap does not work
* the function can only operate on the copies of its own frame.
```C
void swap(int x, int y) {
int temp = x;
x = y;
y = temp;
}

int main(void) {
int a = 3;
int b = 4;
swap(a, b);
}
```

# pointer basics 
* a pointer's value is the location of another variable.
* Just like we can make variables that are integers, doubles, etc., we can make variables that are pointers. Such variables have a size (a number of bytes in memory), a name, and a value. They must be declared and initialized.
* declaring a pointer 
* * In C, "pointer" (by itself) is not a type. It is a type constructor—a language construct which, when applied to another type, gives us a new type. In particular, adding a star (*) after any type names the type, which is a pointer to that type. For example, the code char * my_char_pointer; (pronounced "char star my char pointer") declares a variable with the name my_char_pointer with the type pointer to a char (a variable that points to a character). The declaration of the pointer tells you the name of the variable and type of variable that this pointer will be pointing to.

* Assigning to a pointer
* * an lvalue is an expression that "names a box".The only kind of lvalue we have seen so far is a variable, which names its own box.
* * the address of a variable is not itself an lvalue, and thus not something that can be changed by the programmer. The code &x = 5; will not compile. A programmer can access the location of a variable, but it is not possible to change the location of a variable.
* *  &: address of operator.放在variable 前面， In the context of pointers, the & symbol is a unary operator—an operator that takes only one operand.

* Dereferencing a pointer
* * the star symbol *, a unary operator that dereferences a pointer.
* * the * operator (the dereference operator): get the value of the variable the pointer points to

*  the * sign 
* * When used in declaration (int* ptr), it creates a pointer variable.
* * When not used in declaration, it act as a dereference operator.

```C
int myAge = 43;     

// A pointer variable, with the name ptr, that stores the address of myAge
int* ptr = &myAge;  

// Output the memory address of myAge (0x7ffe5367e044)
printf("%p\n", &myAge);
printf("%p\n", ptr);
```


