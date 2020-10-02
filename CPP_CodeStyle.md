# C++ Code Style


## Purpose of the document


This document propose simple rules to follow in order to create readable and homogeneous code and easy to integrate and share with embedded C code.


## Identifiers

- All names must be in English
- The identifier must be as descriptive as possible, trying not to use ambiguous abbreviations and without duplicating information that is already known or easily understood
- With the help of the various types of case (upper case, lower case, camel case) and the use of underscores, will be intuitive and simple identifying what it is

	* Description Table

		| Lower case with separator (\_) |
		|:------------------------------:|
		| local variables                |
		| struct fields                  |
		| pure c function                |
		
		**Example: `rx_buffer, stream, pre_c_function()`**
		
	
		| Camel case with separator (\_) |
		|:------------------------------:|
		| global variables               |
		
		**Example: `Global_Variable`**
		
		
		| Camel case with separator (\_) and prefix (\_) |
		|:----------------------------------------------:|
		| member class variables                         |
		
		**Example: `_Member_Class_Variable`**
				
	
		| Upper case with separator (\_) and prefix (\_) |
		|:----------------------------------------------:|
		| constants                                      |
		| enum and enum fields                           |
		| macros                                         |
		| defines                                        |
		| global_structs (not used as c++ class)                |
		
		**Example: `CONSTANT_VARIABLE, ENUM_FIELD, MACRO(x), GLOBALSTRUCT`**
		
	
		| Camel case without separator                   |
		|:----------------------------------------------:|
		| namespaces                                     |
		| classes                                        |
		| structs (used as class os class field)         |
		| template                                       |
		| methods                                        |
	
		**Example: `NameSpace, ClassName, StructAsClassOrClassField, ClassName::ClassMethos()`**
		
		So, will be easy to understand for example:
		
		- **`generic_variable`** 
			+ is local variable with limited scope and life
			
		- **`Generic_Variable`** 
			+ is global variable with unlimited scope and life
		
		- **`_Generic_Variable`** 
			+ is member of current class

		- **`GENERIC_VARIABLE`** 
			+ is unmutable/constant variable
			
		- **`generic_function()`** 
			+ is a c style function
			
		- **`GenericFunction()`**
			+ is a method of class

		- **`GENERIC_FUNCTION()`** 
			+ is a preprocessor macro 
			
## Code formatting

- Curly brackets are placed on new line
- Use tab and not space to indent from margin in order to allow tab resize (2,4,8)
- Use space and not tab to align statement, variable and assignment
- Declare only **one** variable per line
- It's preferred initialize variables not in line, in order to divide declaration from initialization
- Use only one statement per line without mixing assignments and comparisons, or using multiple assignments 
- Use always round brackets in mathematical calculations and return statement

## Control flow

- Avoid as much as possible to use multiple **return** within functions, especially if these are complex: concentrate them at the beginning and / or at the end
- Use the **break** only and exclusively in **switch/case** constructs
- Avoid using **continue** if not for very strong optimizations
- Use **goto** only if strictly necessary (like for multiple error handling, only if exceptions are not handled)
- No numeric constant should appear in the code unless it is absolutely obvious and / or commented out: use **const**, **constexp**, **sizeof**, **enum**, **define** instead
- Avoid using a **!(not)** in the **if** condition if **else** exists
- Use **if** in compact form **only for bool** variables (not for pointers). → **if (bool)** or **if (! bool)**
- Use **for** only in the form with the same variable in initialization, control and increment and everything is always executed (ie without other possibilities of exit), otherwise use **while**
- All **switch** must have a default

## Function and Method

- Member function names must consist of: **`[verb]_[subject]_[attributes]`**
	+ **Example: `SetAddess, SetName`**	
- Static C local function names is must consist of: **`[verb]_[subject]_[attributes]`**
	+ **Example: `set_addess, set_name`**
- Global C function names must consist of: **`[module]_[verb]_[subject]_[attributes]`**
	+ **Example: `network_set_addess, device_set_name`**	


## Exception and Assert

- When possible use **try/catch** in smart way or at least use **ASSERT_EXCEPTION()**
- Always check the consistency and validity of the input variables and if there are no way to manage issue use **ASSERT()**




		
		

