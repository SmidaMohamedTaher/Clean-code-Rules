# Clean code rules

In this documentation, we will discuss the rules of writing clean and readable code.

## 1- Main Naming Rules for Variables

In Clean Code, variable names should be **meaningful, descriptive, readable, and easy to understand**. A good name explains what the variable represents without requiring extra comments.

### Rule 1: Use meaningful names

Choose names that explain the purpose of the variable.

**Bad**
```python
x = 21
d = 10
```

**Good**
```python
student_age = 21
max_attempts = 10
```

### Rule 2: Use pronounceable names

Names should be easy to read and say aloud.

**Bad**
```python
genymdhms = 20261024
```

**Good**
```python
generation_timestamp = 20261024
```

### Rule 3: Use searchable names

Avoid single letters or short abbreviations when they make the code difficult to understand.

**Bad**
```python
n = 100
s = 0
```

**Good**
```python
number_of_students = 100
total_score = 0
```

Single-letter names can be acceptable for short, conventional contexts, such as `i` in a simple loop.

### Rule 4: Use `snake_case` in Python

Separate words with underscores.

**Bad**
```python
studentName = "Ahmed"
StudentAge = 22
```

**Good**
```python
student_name = "Ahmed"
student_age = 22
```

In Python, `snake_case` is the standard convention for variables and functions.

### Rule 5: Avoid unnecessary words

Keep names concise without losing meaning.

**Bad**
```python
the_number_of_students_in_the_university = 500
```

**Good**
```python
student_count = 500
```

### Rule 6: Use names that reveal intent

The name should explain what the variable is used for.

**Bad**
```python
temp = 36
```

**Good**
```python
temperature_celsius = 36
```

### Rule 7: Use consistent terminology

Use the same word for the same concept throughout your project.

**Inconsistent**
```python
student_list = []
pupil_count = 0
learner_names = []
```

**Consistent**
```python
students = []
student_count = 0
student_names = []
```

### Rule 8: Avoid misleading names

A variable's name must match its actual content.

**Bad**
```python
student_names = 25
```

**Good**
```python
student_count = 25
```

### Rule 9: Use names appropriate to the data type

The name should make the variable's role clear.

```python
# Integer or count
student_count = 30

# List
student_names = ["Ali", "Sara"]

# Boolean
is_student_registered = True

# Dictionary
student_grades = {"Ali": 15, "Sara": 18}
```

For Boolean variables, prefixes such as `is_`, `has_`, and `can_` often make conditions easier to read.

### Rule 10: Avoid magic numbers in names and code

When a number has a specific meaning, give it a descriptive constant name.

**Bad**
```python
if age >= 18:
    allow_registration()
```

**Good**
```python
MINIMUM_REGISTRATION_AGE = 18

if age >= MINIMUM_REGISTRATION_AGE:
    allow_registration()
```

In Python, constants are conventionally written in `UPPER_SNAKE_CASE`.

### Rule 11: Use the popular abbreviations

If the variable can be abbreviated with a popular abbreviation, it's best to use it.

**Good**
```python
Value = 10
message = "Hello world"
Accuracy = 90
Learning_rate = 0.02
```

**Better**
```python
val = 10 
msg = "Hello world"
acc = 90
LR = 0.02
```


## 2- Rules for Writing Functions

In Clean Code, functions should be **small, focused, readable, and responsible for one clear task**. A well-written function should be easy to understand, test, reuse, and maintain.

### Rule 1: Keep functions small

A function should contain only the code needed to perform its task. Avoid long functions with many different operations.

**Bad**
```python
def process_student(student):
    # Validate student
    # Calculate average
    # Determine result
    # Save to database
    # Print report
    pass
```

**Good**
```python
def calculate_average(grades):
    return sum(grades) / len(grades)

def is_passing(average):
    return average >= 10
```

### Rule 2: A function should do one thing

Each function should have one clear responsibility. If you need to describe a function using several unrelated actions, consider splitting it.

**Bad**
```python
def process_data(data):
    cleaned_data = clean_data(data)
    model = train_model(cleaned_data)
    save_results(model)
```

**Good**
```python
def prepare_data(data):
    return clean_data(data)

def train_classifier(data):
    return train_model(data)

def save_model_results(model):
    save_results(model)
```

A Boolean parameter that changes the function's behavior can indicate that the function has more than one responsibility.

**Bad**
```python
def get_price(price, apply_discount):
    if apply_discount:
        return price * 0.9
    return price
```

**Good**
```python
def get_regular_price(price):
    return price

def get_discounted_price(price):
    return price * 0.9
```

### Rule 3: Use descriptive function names

The name should explain exactly what the function does.

**Bad**
```python
def calc(x):
    return x * 0.19
```

**Good**
```python
def calculate_tax(price):
    return price * 0.19
```

Use a **verb or verb phrase** because a function performs an action.

Examples:
- `calculate_average()`
- `validate_email()`
- `load_dataset()`
- `train_model()`
- `send_notification()`

### Rule 4: Keep the number of parameters small

Functions with many parameters are harder to understand and call. Prefer a small number of meaningful parameters.

**Bad**
```python
def create_student(name, age, email, city, grade, group):
    pass
```

**Good**
```python
def create_student(student_info):
    pass
```

Here, `student_info` could be a suitable object or dictionary containing the student's details. Do not combine parameters artificially if that makes the function harder to understand.

### Rule 5: Avoid side effects

A function should not unexpectedly modify data, change global variables, or perform unrelated operations.

**Bad**
```python
total = 0

def calculate_total(price):
    global total
    total += price
    return total
```

**Good**
```python
def calculate_total(prices):
    return sum(prices)
```

The second function calculates and returns a result without modifying external state.

### Rule 6: A function should return a clear result

Make the return value predictable and consistent with the function's purpose.

**Bad**
```python
def calculate_average(grades):
    print(sum(grades) / len(grades))
```

**Good**
```python
def calculate_average(grades):
    return sum(grades) / len(grades)
```

Printing displays information; returning a value allows other functions to reuse it.

### Rule 7: Avoid deeply nested conditions

Deeply nested `if` statements make functions difficult to read. Use early returns or guard clauses where appropriate.

**Bad**
```python
def process_user(user):
    if user is not None:
        if user.is_active:
            if user.has_permission:
                return perform_action(user)
    return None
```

**Good**
```python
def process_user(user):
    if user is None:
        return None

    if not user.is_active:
        return None

    if not user.has_permission:
        return None

    return perform_action(user)
```

### Rule 8: Keep function arguments and return values meaningful

Choose parameter names that describe the expected input, and make the returned value match the function's name.

**Bad**
```python
def f(x):
    return x * 2
```

**Good**
```python
def double_value(number):
    return number * 2
```

### Rule 9: Avoid unnecessary comments

Readable code should explain itself through good names and simple structure. Comments are useful for explaining *why* a non-obvious decision was made, rather than repeating what the code already says.

**Bad**
```python
# Increment counter by one
counter += 1
```

**Good**
```python
# Retry count is incremented after each failed request.
retry_count += 1
```

### Rule 10: Handle errors clearly

A function should handle invalid inputs and expected errors appropriately. Avoid silently hiding failures.

**Bad**
```python
def divide(a, b):
    return a / b
```

**Good**
```python
def divide(numerator, denominator):
    if denominator == 0:
        raise ValueError("Denominator cannot be zero")

    return numerator / denominator
```

The second example provides a clear error message when the operation is invalid.
