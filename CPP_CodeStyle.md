# 📄 C++ Code Style Guide (v2.0)

## 📚 Quick Reference
| Category | Convention | Example |
|---|---|---|
| **Local variables / struct fields / pure‑C functions** | `lower_case_with_underscores` | `rx_buffer`, `pure_c_function()` |
| **Global variables** | `Upper_Camel_Case_With_Underscores`<br />`Pascale_Case_With_Underscore` | `Global_Variable` |
| **Member class variables** | (leading underscore)<br />`_Upper_Camel_Case_With_Underscores` <br />`_Pascale_Case_With_Underscore` | `_Member_Variable`                                          |
| **Constants, enums, enums class, macros, typedefs, structs** | `UPPER_CASE` | `MAX_BUFFER_SIZE` |
| **Namespaces, classes, templates, methods** | `UpperCamelCase`<br />`PascalCase` | `MyNamespace`, `ClassName`,  `TemplateType`, `MethodName()` |
| **Interface classes** | `IUpperCamelCase` (prefix `I`) | `IShape` |

---

## 🎯 Purpose
Defines a clear, consistent set of conventions for writing **readable**, **maintainable**, and **portable** C++ code that interoperates smoothly with embedded C.

---

## 🏷️ Identifiers
- Use **English** identifiers only.  
- Be descriptive; avoid vague abbreviations.  
- Follow the naming tables above to instantly convey scope, ownership, and purpose.

### 📌 Examples
```cpp
int rx_buffer;                            // local variable - lower case
typedef struct
{
    int baud_rate;                        // struct field - lower case
} DEVICE_CONFIG;                          // struct name - UPPER_CASE

struct I2C                                // struct name - UPPER_CASE
{
    I2C(void)                             // contructor - UPPER_CASE
    {
        address = 0;
    }
    
    uint8_t address;                      // struct field - lower case
};                                        // struct - UPPER_CASE
void pure_c_function();                   // C‑style function - lower case
int Global_Variable = 0;                  // global variable – PascalCase
class MyClass 
{
	private:
    	int _Member_Variable;             // member variable with leading underscore – PascalCase

    public:
    	void SetAddress();                // method name – PascalCase
    	void Set(uint8_t device_address); // parameter - lower_case
};

#define MAX_BUFFER_SIZE 1024              // constant macro - UPPER CASE

enum class LED_COLOR { RED, GREEN };      // enum class - UPPER_CASE
```
> **Note:** Opening `{` and closing `}` braces must always appear on their own line.

---

## 🛠️ Code Formatting
- **Braces**: placed alone on a new line.
- **Indentation**: use **tabs** for block indentation; spaces only for intra‑line alignment.
- One declaration per line.
- Prefer separate declaration and initialization.
- One statement per line – no mixed assignments/comparisons.
- Enclose all arithmetic expressions and return values in parentheses.

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
- Minimize multiple `return` statements; keep them at the start or end of a function.
- Use `break` only inside `switch`/`case` blocks.
- Avoid `continue` unless it yields a clear benefit.
- Reserve `goto` for error‑handling cleanup paths.
- Replace magic numbers with `const`, `constexpr`, `enum`, or `#define`.
- Prefer `if (condition)` over `if (!condition)` when an `else` follows.
- Use compact `if` only for boolean variables, not pointers.
- Favor `while` loops unless the loop variable is fully expressed in a single `for` header.
- Every `switch` must include a `default` case.
- Prefer bit‑field structures over manual bitwise operations for protocol/driver data.

**Additional pointer/reference guidelines**

- Use a **pointer** when a function needs to return a value through an argument. The syntax `func(..., &out)` makes it immediately obvious at the call site that this parameter is meant to receive a result rather than provide input.
- Prefer passing arguments as a **`const` reference** whenever you need read‑only access to an object. A reference cannot be null, which eliminates the need for null checks, and `const` guarantees that the function will not modify the argument.

---

## 🧩 Functions & Methods
- **Class member**: `[verb]_[subject]_[attributes]`
  - Example: `SetAddress`, `ResetCounter`
- **Static local C functions**: `[verb]_[subject]_[attributes]
  - Example: `set_address`, `reset_counter`
- **Global C functions**: `[module]_[verb]_[subject]_[attributes]`
  - Example: `network_set_address`, `device_reset_counter`

---

## ⚠️ Exceptions & Assertions
- Use `try`/`catch` judiciously; for unrecoverable errors prefer `ASSERT_EXCEPTION()`.
- Validate all inputs; use `ASSERT()` when a violation cannot be recovered.

---

## 📑 Doxygen Comments  

Consistent documentation is essential for maintainability and automatic API generation. Follow these rules when writing Doxygen comments:

| Rule                             | Description                                                  |
| -------------------------------- | ------------------------------------------------------------ |
| **Use the `/// @` form**         | Prefer triple‑slash (`///`) with an `@` tag (e.g., `/// @brief`). This keeps comments close to the code and works well with most IDEs. |
| **Return values**                | Even if a function returns `void`, include an `@retval` (or `@return`) line describing the effect or side‑effects. This clarifies intent for callers. |
| **Parameter direction tags**     | `[in]`, `[out]`, and `[in,out]` are optional . |

> **Tip:** Keep comments up‑to‑date. Out‑of‑date documentation is more harmful than none.
