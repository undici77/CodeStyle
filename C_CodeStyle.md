# 📄 C Code Style Guide (v2.0)

## 📚 Quick Reference
| Category | Convention | Example |
|---|---|---|
| **Local variables** | `lower_case_with_underscores` | `rx_buffer` |
| **Struct fields / Functions** | `lower_case_with_underscores` | `process_data()` |
| **Global variables** | `Upper_Camel_Case_With_Underscores` | `Global_Variable` |
| **Constants, enums, macros, typedefs** | `UPPER_CASE_WITH_UNDERSCORES` | `MAX_BUFFER_SIZE` |
| **Structures / typedefs** | `UPPER_CASE_WITH_UNDERSCORES` | `STRUCT_NAME` |

---

## 🎯 Purpose
This document defines a concise, consistent set of rules for writing **readable**, **maintainable**, and **portable** C code that can be easily shared with C++ projects.

---

## 🏷️ Identifiers
- Use **English** names only.  
- Choose descriptive identifiers; avoid ambiguous abbreviations.  
- Follow the naming tables above to infer scope and purpose at a glance.

### 📌 Examples
```c
int rx_buffer;                     // local variable
struct device_config 
{
	int baud_rate;
};                                 // struct field (lower case)
void process_data(void);           // function name
int Global_Variable = 0;           // global variable
#define MAX_BUFFER_SIZE 1024       // constant macro
typedef struct 
{
	int id; 
} STRUCT_NAME;                     // typedef
```
> **Note:** Opening `{` and closing `}` braces must always appear on their own line.

---

## 🛠️ Code Formatting
- **Braces**: placed alone on a new line.
- **Indentation**: use **tabs** for block indentation; use spaces only to align columns within a line.
- Declare **one variable per line**.
- Prefer separate declaration and initialization.
- One statement per line – no mixed assignments/comparisons.
- Enclose all arithmetic expressions and return values in parentheses.

### 📌 Example
```c
int main(void)
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
- Minimize multiple `return` statements; keep them at the start or end of a function.
- Use **break** only inside `switch`/`case` blocks.
- Avoid `continue` unless it provides a clear performance benefit.
- Use `goto` solely for error‑handling cleanup.
- Replace magic numbers with `const`, `enum`, or `#define`.
- Prefer `if (condition)` over `if (!condition)` when an `else` follows.
- Use compact `if` only for boolean variables, not pointers.
- Favor `while` loops unless the loop variable is initialized, tested, and incremented in a single `for` statement.
- Every `switch` must include a `default` case.
- Prefer bit‑field structures over manual bitwise operations for protocol/driver data.

---

## 🧩 Functions & Methods
- **Static local functions**: `[verb]_[subject]_[attributes]`
  - Example: `set_address`, `reset_counter`
- **Global functions**: `[module]_[verb]_[subject]_[attributes]`
  - Example: `network_set_address`, `device_reset_counter`

---

## ⚠️ Exceptions & Assertions
- Validate all input parameters.
- Use `ASSERT()` for unrecoverable errors; if handling is possible, return an error code instead of aborting.

---

## 📑 Doxygen Comments  

Consistent documentation is essential for maintainability and automatic API generation. Follow these rules when writing Doxygen comments:

| Rule                             | Description                                                  |
| -------------------------------- | ------------------------------------------------------------ |
| **Use the `/// @` form**         | Prefer triple‑slash (`///`) with an `@` tag (e.g., `/// @brief`). This keeps comments close to the code and works well with most IDEs. |
| **Return values**                | Even if a function returns `void`, include an `@retval` (or `@return`) line describing the effect or side‑effects. This clarifies intent for callers. |
| **Parameter direction tags**     | `[in]`, `[out]`, and `[in,out]` are optional . |

> **Tip:** Keep comments up‑to‑date. Out‑of‑date documentation is more harmful than none.
