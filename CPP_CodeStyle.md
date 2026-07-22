# 📄 C++ Code Style Guide (v2.0)

## 📚 Quick Reference
| Category | Convention | Example |
|---|---|---|
| **Local variables / struct fields / free functions (C-style)** | `lower_case_underscores` | `rx_buffer`, `my_function` |
| **Global variables** | `Upper_Camel_Case_Underscores` | `My_Global` |
| **Member variables** | (leading underscore)<br />`_Upper_Camel_Case_Underscores` | `_My_Member` |
| **Methods** | `UpperCamelCase` | `MyMethod` |
| **Constants / Macros** | `UPPER_CASE` | `MAX_SIZE` |
| **Classes** | `UpperCamelCase` | `MyClass` |
| **POD Structs** | `UPPER_CASE` | `MY_STRUCT` |
| **Enum class types** | `UPPER_CASE` | `MY_ENUM` |
| **Enum class values** | `UPPER_CASE` | `MY_VALUE` |
| **Interfaces** | `IUpperCamelCase` (prefix `I`) | `IMyInterface` |
| **Function pointer aliases** | `UPPER_CASE` | `MY_CALLBACK` |

---

## 🎯 Purpose
Defines a clear, consistent set of conventions for writing **readable**, **maintainable**, and **portable** C++ code that interoperates smoothly with embedded C.

---

## 🏷️ Identifiers
- Use **English** identifiers only.
- Be descriptive; avoid vague abbreviations.
- Follow the naming tables above to instantly convey scope, ownership, and purpose.
- **Hungarian notation is FORBIDDEN.**
- Use `enum class` ALWAYS. No plain `enum`.
- No `typedef` on structs, enums, or unions. Use plain `struct UPPER_CASE` for POD types.
- Every `enum class` MUST define an explicit `NUMBER` or `INVALID` sentinel as the last entry.
- Function pointer aliases use `UPPER_CASE` with `using` syntax (no raw function pointer syntax at declaration sites).

### 📌 Examples
```cpp
int rx_buffer;                            // local variable - lower case
struct DEVICE_CONFIG                      // POD struct - UPPER_CASE
{
    int baud_rate;                        // struct field - lower case
};

void my_function(void);                   // free function - lower case
int My_Global = 0;                        // global variable - PascalCase
class MyClass
{
    public:
    	void SetAddress(void);            // method name - PascalCase
    	void Set(uint8_t device_address); // parameter - lower case

    private:
    	int _Member_Variable;             // member variable - PascalCase with leading underscore
};

#define MAX_SIZE 1024                     // constant macro - UPPER_CASE

enum class LED_COLOR
{
    RED    = 0,
    GREEN  = 1,
    NUMBER
};                                        // enum class - UPPER_CASE

using MY_CALLBACK = void(*)(int);         // function pointer alias - UPPER_CASE
```
> **Note:** Opening `{` and closing `}` braces must always appear on their own line.

---

## 🧱 Type Definitions

### Struct
- Name: `UPPER_CASE`.
- Fields: `lower_case_underscores`.
- If the struct has methods, use `class` instead.

### Enum
- Use `enum class` ALWAYS. No plain `enum`.
- No `typedef`. Name: `UPPER_CASE`. Values: `UPPER_CASE`.
- ALWAYS define an explicit `NUMBER` or `INVALID` sentinel as the last entry.

### Union
- Name: `UPPER_CASE`.
- Fields: `lower_case_underscores`.
- Anonymous inner structs allowed for bitfield unions.

### Function Pointer
- Use `using UPPER_CASE = ...` alias. No raw function pointer syntax at declaration sites.
- `std::function<>` or plain pointer: both allowed depending on context.

---

## 📄 Files
| Extension | Ruleset | Separator Line |
| :--- | :--- | :--- |
| `.cpp` / `.cc` | This document | YES |
| `.h` / `.hpp` | This document | NO |

- All types may live in `.hpp` OR `.cpp`. Both are valid.
- Prefer `.hpp` when the type is shared across translation units.
- Prefer `.cpp` when the type is internal/private to that file.

---

## 🛠️ Code Formatting
- **Braces**: placed alone on a new line.
- **Indentation**: use **tabs** for block indentation; spaces only for intra‑line alignment.
- One declaration per line.
- Prefer separate declaration and initialization.
- One statement per line – no mixed assignments/comparisons.
- Enclose all arithmetic expressions and return values in parentheses.
- **Magic numbers**: FORBIDDEN. Use `const`, `constexpr`, or `enum`.
- **Null pointers**: `NULL` exclusively. Never use `nullptr`.

### Separator Lines
- `.cpp` / `.cc` files: include a separator line (`/****************************************************************************************************/`) before every function definition.
- `.h` / `.hpp` files: no separator lines.

### 📌 Example
```cpp
int main()
{
	int count;
	int result;

	count = 0;

    result = (count + 5) * 2;
	return (result);
}
```
---

## 🔀 Control Flow
- Use `struct` for plain‑old‑data aggregates (PODs) that have only public members and trivial constructors/destructors.
- Use `class` when you need encapsulation, behavior, or abstraction.
- Single exit point preferred. Early return allowed for errors only.
- Use `break` only inside `switch`/`case` blocks. `break` in `for` and `while` loops is FORBIDDEN.
- `continue` is FORBIDDEN. Restructure loop logic to avoid it.
- Reserve `goto` for error‑handling cleanup paths.
- Replace magic numbers with `const`, `constexpr`, `enum`, or `#define`.
- Prefer `if (condition)` over `if (!condition)` when an `else` follows.
- Use compact `if` only for boolean variables, not pointers.
- Favor `while` loops unless the loop variable is fully expressed in a single `for` header.
- Every `switch` must include a `default` case.
- Prefer bit‑field structures over manual bitwise operations for protocol/driver data.
- Every `enum class` MUST define an explicit `NUMBER` or `INVALID` sentinel as the last entry.
- Function pointer aliases use `UPPER_CASE` with `using` syntax. No raw function pointer syntax at declaration sites.

**Additional pointer/reference guidelines**

- Use a **pointer** when a function needs to return a value through an argument. The syntax `func(..., &out)` makes it immediately obvious at the call site that this parameter is meant to receive a result rather than provide input.
- Prefer passing arguments as a **`const` reference** whenever you need read‑only access to an object. A reference cannot be null, which eliminates the need for null checks, and `const` guarantees that the function will not modify the argument.

---

## 🧩 Functions & Methods
- **Class member**: `[verb]_[subject]_[attributes]`
  - Example: `SetAddress`, `ResetCounter`
- **Free functions (C-style)**: `[verb]_[subject]_[attributes]`
  - Example: `set_address`, `reset_counter`
- **Global C functions**: `[module]_[verb]_[subject]_[attributes]`
  - Example: `network_set_address`, `device_reset_counter`
- **Function pointer aliases**: `UPPER_CASE` with `using` syntax
  - Example: `using MY_CALLBACK = void(*)(int);`

---

## ⚠️ Exceptions & Assertions
- Use `try`/`catch` judiciously; for unrecoverable errors prefer `ASSERT_EXCEPTION()`.
- Validate all inputs; use `ASSERT()` when a violation cannot be recovered.

---

## 📑 Doxygen Comments

Consistent documentation is essential for maintainability and automatic API generation. Follow these rules when writing Doxygen comments:

| Rule                             | Description                                                  |
| -------------------------------- | ------------------------------------------------------------ |
| **Default**                      | Do NOT generate Doxygen unless explicitly asked.             |
| **Use the `/// @` form**         | Prefer triple‑slash (`///`) with an `@` tag (e.g., `/// @brief`). This keeps comments close to the code and works well with most IDEs. |
| **`@brief`**                     | Required.                                                      |
| **`@param [in]` / `@param [out]`** | Required.                                                    |
| **Return values**                | Even if a function returns `void`, include an `@retval` (or `@return`) line describing the effect or side‑effects. This clarifies intent for callers. |

> **Tip:** Keep comments up‑to‑date. Out‑of‑date documentation is more harmful than none.

---

## 🔄 Workflow

### Mode A — Code Generation
1. Apply naming + formatting rules immediately.
2. Run Pre‑Flight Checklist (Section 8) internally before output.
3. Output code only. No filler.

### Mode B — Review / Lint
1. Scan for violations.
2. Output Violation Report:
   ```
   [VIOLATION] Line N - <Rule>
     Found:    <original>
     Fixed:    <corrected>
   ```
3. Output corrected code immediately after.

---

## ✅ Pre‑Flight Checklist (Internal — run before every output)
- [ ] Braces on own lines?
- [ ] Tabs for indentation, no spaces?
- [ ] Naming matches Section 3?
- [ ] No magic numbers?
- [ ] Every `switch` has `default`?
- [ ] Member variables have leading `_`?
- [ ] Interfaces prefixed with `I`?
- [ ] `enum class` used, never plain `enum`?
- [ ] No `typedef` on structs/enums/unions?
- [ ] Function pointer aliases use `UPPER_CASE` and `using`?
- [ ] Separator line present in `.cpp`/`.cc`, absent in `.hpp`?
- [ ] No `continue` statements?
- [ ] No `break` in `for` loops?
- [ ] No `break` in `while` loops?
- [ ] Uses `NULL`, never `nullptr`?

---

## 📝 Examples

### `shapes.hpp`
```cpp
#ifndef SHAPES_HPP
#define SHAPES_HPP


#include <cstdint>
#include <functional>


// Enum class
enum class SHAPE_TYPE
{
	CIRCLE    = 0,
	RECTANGLE = 1,
	NUMBER
};


// POD struct
struct MY_DIMENSIONS
{
	float width;
	float height;
};


// Function pointer alias
using AREA_COMPUTE = std::function<float(const MY_DIMENSIONS &dims)>;


// Interface
class IShape
{
	public:
		virtual ~IShape(void) = default;
		virtual float      ComputeArea(void) const = 0;
		virtual SHAPE_TYPE GetType(void) const     = 0;
};


// Concrete class
class Circle : public IShape
{
	public:
		explicit Circle(float radius);


		float      ComputeArea(void) const override;
		SHAPE_TYPE GetType(void) const override;

	private:
		float _Radius_Value;
};


#endif
```


### `shapes.cpp`
```cpp
#include "shapes.hpp"

// Union - internal to this file
union MY_FLOAT_BITS
{
	float    value;
	uint32_t raw;
};

static constexpr float PI = 3.14159f;

/****************************************************************************************************/
Circle::Circle(float radius)
/****************************************************************************************************/
{
	_Radius_Value = radius;
}

/****************************************************************************************************/
float Circle::ComputeArea(void) const
/****************************************************************************************************/
{
	return (PI * _Radius_Value * _Radius_Value);
}

/****************************************************************************************************/
SHAPE_TYPE Circle::GetType(void) const
/****************************************************************************************************/
{
	return (SHAPE_TYPE::CIRCLE);
}
```

### `main.cpp`
```cpp
#include <iostream>
#include "shapes.hpp"

/****************************************************************************************************/
int main(void)
/****************************************************************************************************/
{
	Circle    circle(5.0f);
	IShape   *shape;
	float     area;

	shape = &circle;
	area  = shape->ComputeArea();

	std::cout << "Area: " << area << '\n';

	return (0);
}
```

### `control_flow_null.cpp`
```cpp
#include <cstdint>

static constexpr int MAX_ITER = 10;

/****************************************************************************************************/
void ProcessData(int32_t *data, int32_t count)
/****************************************************************************************************/
{
	// CORRECT: Invert condition, remove continue
	for (int32_t i = 0; i < count; i++) 
	{
		if (data[i] != NULL) 
		{
			ProcessElement(data[i]);
		}
	}

	// CORRECT: while loop with combined condition
	int32_t idx = 0;
	while ((idx < count) && (data[idx] != TARGET_VALUE)) 
	{
		idx++;
	}

	// CORRECT: NULL exclusively
	int32_t *ptr = NULL;
}
```
