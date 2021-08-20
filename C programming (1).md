- Mac environment setup for VSCode
    - Official [Microsoft docs](https://code.visualstudio.com/docs/cpp/config-clang-mac)
    - VSCode debugger doesn't yet support Apple M1. Fix is to install [CodeLLDB extension](https://marketplace.visualstudio.com/items?itemName=vadimcn.vscode-lldb) and configure launch.json [as noted here](https://github.com/microsoft/vscode-cpptools/issues/7035#issuecomment-841614784) until open issue is resolved.
    - Launch.json file for this extension:
        - ```javascript
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
      {
        "name": "clang++ - Build and debug active file",
        "type": "lldb",
        "request": "launch",
        "program": "${fileDirname}/${fileBasenameNoExtension}",
        "args": [],
        "cwd": "${workspaceFolder}",
        "preLaunchTask": "clang++ build active file"
      }
    ]
  }```
- Why C?
    - Efficient 
        - Fast and compact
        - Can be fine-tuned because of direct access to memory, etc…
    - Portable 
        - Can run on nearly any hardware and operating system
        - Compliers available for just about any device
    - Powerful and flexible
        - UNIX/Linux kernel written in C
        - Can write nearly any program with it
        - Provides direct access to hardware (low level) and individual bits of memory (pointers)
    - Large library of useful C functions available
- Four tasks to create a C program
    - Editing
        - Base file name followed by .c extension
    - Compiling
        - Convert high level source code into machine code (assembly language)
        - Output is object code, same name as source but with .o extension
        - 2 stage process:
            - Pre-processing
            - Compilation
                - Check syntax
                - Check semantics (meaning)
                - Will not find logic errors
    - Linking
        - Get all dependencies / external libraries
    - Executing
        - a.out on CLI
        - runs in console
- Code structure in a C app
    - main() function is required for all programs. One and only one.
    - { and } brackets around the block of code for the function.
    - imported libraries are above the function name with an #include statement.
    - Semi-colons after each statement.
- The Preprocessor
    - Fairly unique to C
    - Makes programs easier to develop read, modify and port
    - Part of compilation that recognizes special statements before compiling
    - Preprocessor statements (aka directives) are identified by the # sign. Must be the first non-space character on a line.
    - Can be used for:
        - Creating constants and macros with the #define statement
        - Building library files with the #include statement
        - Use conditionals such as #ifdef, #endif, #else, and #ifndef statements.
- #include preprocessor directive
    - Similar to the import statement in Java
    - Angle brackets used to tell the compiler what library to import or include
    - Compiler is instructed to include the library file contents in my program
    - Called a header file because it's usually at the head of the source code and has a .h extension
    - stdio.h is the standard C library header for input and output, explains to the complier what printf() is, for example.
    - Header files should always be lowercase.
    - Can use angle brackets (typically for standard system directories) or double-quotes (usually a user-defined header file, tells the preprocessor to look in the current directory).
    - Should use #ifndef and #define to protect against multiple inclusions of a header file.
    - Header files can include many things:
        - #define directives
        - structure declarations
        - typedef statements
        - function prototypes
- Displaying output
    - printf(): standard library function
    - outputs to command line on the console/terminal (the standard output stream, by default)
    - Can display simple phrases, values of variables and results of computations
    - Useful for debugging
- Reading input from the keyboard / terminal
    - scanf() function is the most general method; part of the stdio.h library
    - stdin by default is the keyboard, scans input according to format provided
        - can be simple constant string but you can specify %s, %d, %c, %f to read strings, integers, characters or floats.
        - input from keyboard is text but you can convert via the format specifier (see above note)
    - scanf() uses a control string followed by a list of arguments
        - control string indicates destination data types for the input stream of characters
        - uses pointers to variables
    - 3 rules of scanf()
        - returns the number of items that it successfully reads
        - if used to read a value for one of the basic data types, precede the variable name with a &
        - no need to use & to read a string into a character array
    - scanf() uses whitespace (newlines, tabs and spaces) to divide input into separate fields
    - scanf() example:
        - ```c
#include <stdio.h>
	
	char myString[100];
	int myInt;

	int main() {
		printf("Enter some text and a value :");
		scanf("%s %d", myString, &myInt);

		printf("\nYou entered: %s %d ", myString, myInt);
  		return 0;
	}```
        - To get a double from scanf(), the format specifier is %lf
        - [Format specifiers for all scanf() data types in C](https://en.wikipedia.org/wiki/Scanf_format_string#Format_string_specifications)
- Variables and data types
    - [Format specifiers](https://en.wikipedia.org/wiki/Printf_format_string#Format_placeholder_specification) (display variable values as output)
        - They specify the type of data of the variable to be displayed ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FCompSciPrep%2FYmVRXCaIzD.jpg?alt=media&token=909094ec-4628-4125-b41a-da664c228988)
        - Arguments separated by commas
        - First argument is always the character string to be displayed
        - Width specifier used for precision
            - Example:
                - ```c
float x = 3.99932493;
printf("%.5f", f);  
// will output 3.99932```
    - Data types required for all variables.
        - [Strict typing](https://en.wikipedia.org/wiki/Strong_and_weak_typing) 
        - Corresponds to byte sizes; how much memory is allocated to store the variable value
    - Declaring variables (only allocates memory but does not assign values)
        - Data Type followed by variable name: __type-specifier variable-name__
        - `int Days;`
        - Multiple variables on a single line are separated by a comma; must all be same data type
        - `int x, y, z;`
    - Assigning variables: use equals sign
        - `int x = 50;`
        - Above is also an initialization
        - Can also be done for multiple variables
        - `int y = 21, z = 40;`
    - [C data types](https://en.wikipedia.org/wiki/C_data_types#Main_types) in [[C programming]]
        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FCompSciPrep%2FkzwGvL-u3K.png?alt=media&token=ee319113-1c67-4d35-bc6a-38f754eb199a)
        - int
            - No decimal places (integrals)
            - Minus sign means negative, can be zero
            - If integer starts with 0x, value is hexadecimal (base 16) notation
                - Example: `int rgbColor = 0xFFEF0D`
        - float
            - floating-point numbers and constants; values with decimals
            - can be in scientific notation
                - Example: 1.7e4 is 1.7 * 10 ^ 4
                - Floating-point constants are stored as doubles by the compiler
                - Add f or F to end of number for a constant
                    - Example: `12.5f`
            - double
                - same as float but with double the precision
                - can store twice as many significant digits
        - char
        - _Bool
            - Stores 0 or 1 to represent true/false, yes/no, on/off
            - 0 is false, 1 is truth
            - To use the bool data type (if not supported by compiler):
                - ```javascript
#include <stdbool.h>
  
  bool booleanVar = true;```
        - Type specifiers
            - Can save memory with by using short int (or just short)
            - Can store longer values by using long int / long double (or just long)
            - Even longer values can be created: long long int: Append L to end of an integer constant
        - Enums
            - [Enums](https://www.geeksforgeeks.org/enumeration-enum-c/): data type where you can define a variable and specify valid values for the variable
            - ```c
	enum primaryColor { red, green, blue };
	enum primaryColor myColor;
	myColor = red;```
            - Complier treats enum identifers as integer constants
                - first value in list is 0
                - in above example green = 1
                - Sounds like an array that references the index values but.....
                - You can specify an integer value associated with an enum indentifer:
                    - enum direction { up, down, left = 10, right};
                    - enum value of up is 0 but value of left is 10 and right is 11
                    - Could be useful to assign values to an enum list of of months: start with January = 1
        - Char
            - Represents a single character such as a letter, digit or semicolon
            - Character literals use single quotes
            - Can be declared as unsigned
            - Declaring: `char broiled;`
            - Remember: single quotes for values. Double quotes are for strings.
            - Can use ASCII codes to assign values but not typical style.
            - [Escape characters / sequences in C](https://en.wikipedia.org/wiki/Escape_sequences_in_C#Table_of_escape_sequences):
- [Format specifiers](https://en.wikipedia.org/wiki/Printf_format_string#Format_placeholder_specification) (display variable values as output)
    - They specify the type of data of the variable to be displayed ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FCompSciPrep%2FYmVRXCaIzD.jpg?alt=media&token=909094ec-4628-4125-b41a-da664c228988)
    - Arguments separated by commas
    - First argument is always the character string to be displayed
    - Width specifier used for precision
        - Example:
            - ```c
float x = 3.99932493;
printf("%.5f", f);  
// will output 3.99932```
- Command line arguments
    - Used to pass input data from the terminal when program is executed as an argument
    - Essentially, you're passing arguments to main()
        - argc is the number of arguments typed on the command line
        - argv is an array of character pointers, i.e. strings
    - First entry in argv array is the name of the program to executed
        - Example: `int main (int argc, char *argv[])`
    - Challenge problem using command line arguments ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FCompSciPrep%2Fdmj2A2Je6M.jpg?alt=media&token=460c0914-f980-458f-b87a-03a90346b419)
- Operators 
    - Functions that use a symbolic name
    - Three types: assignment, relational and bitwise
    - Expressions and Statements
        - Expressions have a combination of operators and operands
        - Every expression has a value
        - Statements end with a semicolon; a complete instruction to the computer
        - Code blocks enclosed in { } are compound statements
        - 
    - Basic operators in C (arithmetic, logical, assignment and logial)
        - Arithmetic: takes two operands and performs a calculation
            - + adds
            - - subtracts
            - * multiplies
            - / divides
            - % modulus ( returns remainder after integer division)
            - ++ increment 
            - -- decrement 
            - prefix increment/decrement happens first, then code statement is executed; happens after statement is executed with postfix
        - Logical: Boolean
            - && logical AND (if both operands are non-zero, condition is true)
            - || logical OR (if any operands are non-zero, condition is true)
            - ! logical NOT (reverses state of true or false)
        - Assignment: sets variables equal to values
            - = assignment
            - += add and assign
            - -= subtract and assign
            - *= multiply and assign
            - /= divide and assign
            - %= modulus and assign
        - Relational: compares variables against each other
            - == are operands equals
            - != are operands equal or not
    - [Bitwise operators](https://en.wikipedia.org/wiki/Bitwise_operations_in_C)
        - Operate on bits in integer values
    - [Binary math](https://en.wikipedia.org/wiki/Binary_number#Binary_arithmetic)
    - Cast and sizeof operators
        - Conversion of data types can happen automatically (implicitly)
            - When float is assigned to an int variable in C, the decimal portion is truncated
            - When int is assigned to float, no change in value
            - Arithmetic on two integers, any decimal portion is truncated
            - Arithmetic on integer and float is performed as a float
        - Cast is for explicit type conversions (has higher precendence over all other operators except for unary minus and plus)
            - Example: `(int) 26.43 //becomes 26`
        - sizeof operator (not a function)returns bytes used in memory by a given type; can be a variable, array name, primitive or derived data type or expression.
            - Example: `sizeof(int) // returns 4`
            - Used to allocate the correct amount of data for #pointers.
        - * operator represents a pointer to a variable; i.e. *argv[]
        - ? is the ternary operator; if isTrue ? then X : else Y
    - Operator precedence ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FCompSciPrep%2F11Me1atB68.jpg?alt=media&token=5cbf8798-6316-4167-b786-40550c87a141)
- For loops in [[C programming]]
    - Counter control loop repeats a set number of times
    - Sentinel loop repeats until a condition is met
    - Loop variables are only in scope of the loop and cease to exist after the loop ends.
    - Counter loop (pre-test loop) example:
        - ```c
for (int count = 0, count <= 10, count++)
{
  printf(" %d", count);
}```
- While and do-while loops
    - Runs until a certain condition is met
        - While condition is true, execute code block
    - While loop (pre-test) example:
        - ```c
while (count <= 5)
  {
    printf("%i\n", count);
    count++;
  }```
- Do-while loop is post-test or exit control loop
    - Executed while condition is true (will always execute at least one time)
        - ```c
int count = 0;
do 
	{
    	printf("%i\n", count);
    	count++;
	} while count <= 5;```
- Nested loops (loops inside of other loops)
    - Continue statement in body of loop skips current iteration. Anything below it will not be executed. Typically wrapped in an if statement.
    - Break statement causes program to immediately exit the loop.
    - Guess the number challenge: ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FCompSciPrep%2FrEyZHpXX-d.jpg?alt=media&token=17d5c489-cc2a-4392-adb7-28ef39066b4c) 
- Arrays in [[C programming]]
    - Used for storing a fixed number values of the same data type.
    - Can't change the size once an array is created. (Technically. You could create a larger array and copy the contents into it but it's a new array)
    - Data items in array are elements.
    - Declaring an array: Name and number between brackets (representing the number of possible elements, i.e. dimension of the array)
        - `long numbers[10]`;
    - Data items are accessed by the same name, i.e. numbers in the above example.
        - Subscript values represent particular elements in the array. Can be an expression but must result in an integer value that represents and element position.
        - Zero based, i.e. 0 through 9 in above example
    - Compiler can't check for array out of bounds errors
    - Assign value to an array: `grades[100] = 95; // can also assign variables to an array;` 
    - Initializing an array
        - Assign values to elements when defining the array
        - `int counters[5] = {0,0,0,0,0};`
        - `int integers[5] = {0,1,2,3,4};`
        - Not required to completely initialize an entire array. Any elements not initialized are set to zero
        - Designated initializers are new in C, can assign values to various elements in any order.
        - `int arr[6] = {[5] = 212};`
        - `int days[Months] = {31, 28, [4] = 31, 30, 31, [1] =29};`
    - Multidimensional arrays
        - Two dimension arrays the most common; visualize like rows and columns in a spreadsheet
        - Most natural application = matrix
        - Declared like a one-dimension array but with a pair of brackets: `int matrix[4][5];`
            - Above is 4 rows and 5 columns; 20 elements.
        - Initialization slightly different: initial values for each row in braces: `{10, 20, 30, 40, 50},` for above example.
        - Can use designated initializers:
            - `int matrix[4][3] = { [0][0] = 1, [1][1]= 5, [2][2]=9 };`
        - Three-dimensional array example: `int coordinates[10, 20, 30]; // maybe x, y, z values`
        - Use nested loops to process elements in an n-dimensional array
    - Variable length arrays (VLA)
        - Doesn't mean you can modify the length after creating the array
        - **A VLA keeps the same size after creation**, allows you to specify the array size with a variable.
        - Can't be initialized in the declaration
    - Challenge: Use an array to find all primes between 3-100.
    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FCompSciPrep%2FG8EIJ9FXLB.png?alt=media&token=8ca7fdfc-72f8-4541-a474-754f5bc7aea8)
- Functions in [[C programming]]
    - What are functions?
        - Self contained code designed to accomplish a particular task
        - Same as subroutine or procedure in other languages
    - What are the advantages?
        - Divide and conquer
        - Reduces complexity
        - Makes it easier to understand and debug code
        - Reduces code duplication and size of source code
        - Helps with readability
        - Functions are like a "black box": you send inputs you get outputs.
    - Data can be passed back as input to a stored address or a Return value
    - Defining functions
        - Function header is the first line, followed by curly braces and the executable code block(s) (aka: Function body)
        - Header defines name, parameters (number and types of data), type of data that's returned
        - Function body has access to any values passed as arguments
    - Function prototypes (function signature)
        - A statement that defines a function
            - Defines name, return value type, type of each parameter
            - Provides all external specifications for this function
                - Example: ```c
void printMessage(void);```
            - Header files define function prototypes
            - Lets you invoke a function before its defined in code (from top to bottom)
    - Arguments and parameters
        - A variable in a function declaration and in a function definition/implementation
        - Arguments are the data you pass in to the parameters
        - Parameters are placeholders for the arguments
        - Parameters are names and types, provide the means to pass data to a function
        - Names of parameters are local to the function and assume the values of the arguments
        - Function body may have additional local variables
        - When passing an array as a parameter, have to specify the size in an additional argument
    - Returning data from functions
        - Return types can be any data type including pointers or enums.
        - Return statement ends a function and returns data (in the form of the expected data type from the calling statement)
    - Invoking functions
        - Call by name with any arguments
        - Argument values get assigned to parameter variables
        - If a function is used as the right side of an assignment statement, the return value can be substituted, such as for storing the value
            - Example: ```c
int x = myFunctionCall();```
            - 
    - Function scope: Local and global variables
        - Variables defined in a function are automatic local variables
        - Access is limited to within the function
        - Initial values assigned within a function are always reset to that value every time the function is called.
        - Local variables are also created in code blocks, i.e.: loops, if statements, etc..
        - Global variables are the opposite. Available anywhere and to any function in the program. 
        - Globals life during the entirety of the program.
        - Any function can modify a global variable
        - Avoid using global variables. Use parameters in functions instead
        - 
    - Challenge: write some functions = absolute value, [greatest common denominator](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) and square root
    - Challenge: write a tic-tac-toe game
- 
