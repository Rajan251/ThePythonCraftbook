# **Variables, Data Types & Operators (Simplest Explanation)**  

## **1. Variables**  
**Variables** are like containers that store data.  
- **Example:**  
  ```python
  name = "Alex"  # A variable storing a name
  age = 25       # A variable storing age
  ```
- **Rules:**  
  - Must start with a letter or `_` (e.g., `_name`, `age1`).  
  - Cannot start with a number (❌ `1age`).  
  - Case-sensitive (`Age` ≠ `age`).  

---

## **2. Data Types**  
Python has different **types of data**:  

| Data Type | Example | Description |
|-----------|---------|-------------|
| `int` (Integer) | `5`, `-3` | Whole numbers |
| `float` (Decimal) | `3.14`, `-0.5` | Numbers with decimals |
| `str` (String) | `"Hello"`, `'Python'` | Text (in quotes) |
| `bool` (Boolean) | `True`, `False` | Represents truth values |
| `list` | `[1, 2, 3]` | Ordered, changeable collection |
| `tuple` | `(1, 2, 3)` | Ordered, unchangeable collection |
| `dict` (Dictionary) | `{"name": "Alice", "age": 30}` | Key-value pairs |
| `set` | `{1, 2, 3}` | Unordered, unique elements |

**Checking Data Type:**  
```python
type(10)       # Output: <class 'int'>
type("Hello")  # Output: <class 'str'>
```

---

## **3. Operators**  
Operators perform operations on variables.  

### **1. Arithmetic Operators**  
| Operator | Example | Result |
|----------|---------|--------|
| `+` (Addition) | `5 + 3` | `8` |
| `-` (Subtraction) | `5 - 3` | `2` |
| `*` (Multiplication) | `5 * 3` | `15` |
| `/` (Division) | `6 / 3` | `2.0` (float) |
| `//` (Floor Division) | `7 // 3` | `2` (int) |
| `%` (Modulus) | `7 % 3` | `1` (remainder) |
| `**` (Exponent) | `2 ** 3` | `8` (2³) |

### **2. Comparison Operators** (Return `True`/`False`)  
| Operator | Example | Meaning |
|----------|---------|---------|
| `==` | `5 == 5` | Equal to |
| `!=` | `5 != 3` | Not equal |
| `>` | `5 > 3` | Greater than |
| `<` | `3 < 5` | Less than |
| `>=` | `5 >= 5` | Greater than or equal |
| `<=` | `3 <= 5` | Less than or equal |

### **3. Logical Operators** (Combine conditions)  
| Operator | Example | Meaning |
|----------|---------|---------|
| `and` | `(5 > 3) and (2 < 4)` → `True` | Both must be `True` |
| `or` | `(5 > 3) or (2 > 4)` → `True` | At least one `True` |
| `not` | `not (5 == 3)` → `True` | Reverses the result |

### **4. Assignment Operators** (Shortcuts)  
| Operator | Example | Equivalent to |
|----------|---------|---------------|
| `=` | `x = 5` | `x = 5` |
| `+=` | `x += 3` | `x = x + 3` |
| `-=` | `x -= 2` | `x = x - 2` |
| `*=` | `x *= 4` | `x = x * 4` |

---

## **Simple Example**  
```python
# Variables
name = "Alice"
age = 25
height = 5.6
is_student = True

# Operations
sum = 10 + 5          # 15
is_adult = age >= 18   # True
print(f"Hello {name}!")  # Hello Alice!
```

### **Key Takeaways**  
✔ **Variables** store data.  
✔ **Data Types** define what kind of data is stored.  
✔ **Operators** perform calculations & comparisons.  

