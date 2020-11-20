# C Code Style


## Purpose of the document


This document propose simple rules to follow in order to create readable and homogeneous code, easy to integrate and share with C++ code.


## Identifiers

- All names must be in English
- The identifier must be as descriptive as possible, trying not to use ambiguous abbreviations and without duplicating information that is already known or easily understood
- With the help of the various type case (upper case, lower case, camel case) and the use of underscores, will be intuitive and simple identifying what it is

	* Description Table

		| Lower case with separator (\_) |
		|:------------------------------:|
		| local variables                |
		| struct fields                  |
		| functions                      |
		
		**Example: `rx_buffer, function()`**
		
	
		| Camel case with separator (\_) |
		|:------------------------------:|
		| global variables               |
		
		**Example: `Global_Variable`**
		
	
		| Upper case with separator (\_) and prefix (\_) |
		|:----------------------------------------------:|
		| constants                                      |
		| enum type and enum fields                      |
		| macros                                         |
		| defines                                        |
		| struct                                         |
		| typedef                                        |
		
		**Example: `typedef struct {..} STRUCT_NAME, CONSTANT_VARIABLE, ENUM_FIELD, MACRO(x), GLOBALSTRUCT`**
		
		So, will be easy to infer:
		
		- **`generic_variable`**
			+ is local variable with limited scope (stack allocated)
			
		- **`Generic_Variable`** 
			+ is global variable with unlimited scope
		
		- **`GENERIC_VARIABLE`** 
			+ is unmutable/constant variable
			
		- **`generic_function()`** 
			+ is a function
			
		- **`GENERIC_FUNCTION()`** 
			+ is a preprocessor macro 
			
		- **`VARIABLE variable`**
			+ is a definition of local variable of type VARIABLE

		- **`VARIABLE Variable`**
			+ is a definition of global variable of type VARIABLE
			
## Code formatting

- Curly brackets are placed alone on new line
- Use tab and not space to indent from margin in order to allow different tab size (2,4,8)
- Use space and not tab to align statement, variable and assignment so different tab size will not affect this alignment
- Declare only **one** variable per line
- It's preferred initialize variables not in line, in order to divide declaration from initialization
- Use only one statement per line without mixing assignments and comparisons, or using multiple assignments 
- Always use round brackets in mathematical calculations and return statement

## Control flow

- Avoid as much as possible use multiple **return** within functions, especially if these are complex: concentrate them at the beginning and / or at the end
- Use the **break** only and exclusively in **switch/case** constructs
- Avoid using **continue** if not for very strong optimizations
- Use **goto** only if strictly necessary (like for multiple error handling, only if exceptions are not handled)
- No numeric constant should appear in the code unless it is absolutely obvious and / or commented out: use **const**, **sizeof**, **enum**, **define** instead
- Avoid using **!(not)** in the **if** condition if **else** exists
- Use **if** in compact form **only for bool** variables (not for pointers). → **if (bool)** or **if (! bool)**
- Use **for** only in the form with the same variable in initialization, control and increment and everything is always executed (ie without other possibilities of exit), otherwise use **while**
- All **switch** must have a default

## Function and Method

- Static C local function names is must consist of: **`[verb]_[subject]_[attributes]`**
	+ **Example: `set_addess, set_name`**
	
- Global C function names must consist of: **`[module]_[verb]_[subject]_[attributes]`**
	+ **Example: `network_set_addess, device_set_name`**

## Exception and Assert

- Always check the consistency and validity of the input variables and if there are no way to manage issue use **ASSERT()**




		
		

