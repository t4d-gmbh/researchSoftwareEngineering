# DRY Principle

The **DRY (Don't Repeat Yourself)** principle is a cornerstone of efficient software engineering.
At its core, it asserts that **"Every piece of knowledge must have a single, unambiguous, authoritative representation within a system."**
Simply put: if you have to perform the same logical operation in multiple places, define it once in a function or class and reuse it, rather than copying and pasting the code.

## Benefits

Adherence to the DRY principle naturally guides developers toward modular design, separating reusable logic from specific scripting tasks.

By following this principle, developers can:

* **Minimize Errors:** Repetition breeds inconsistency. If logic is duplicated, a bug fix applied to one instance might be missed in another.
* **Simplify Maintenance:** When logic is centralized, updates need to be made in only one location, ensuring changes propagate instantly throughout the application.
* **Enhance Quality:** Reusable components are used more frequently, making them easier to stress-test and justify documenting rigorously.
* **Improve Architecture:** It fosters a modular structure, where components are decoupled and can be easily repurposed for other projects.

## Drawbacks and Challenges

While DRY generally leads to cleaner code, it is not a dogma to be followed blindly.
When pushed to the extreme, DRY can lead to the "Wrong Abstraction," introducing several risks:

* **Over-abstraction:** Code can become so generic that it loses clarity. Logic that handles every possible edge case often becomes convoluted and hard to read.
* **Coupling and Complexity:** Striving to make a single function serve two slightly different use cases often results in "parameter soup"—functions requiring complex configuration to work.
* **Fragility:** If two unrelated parts of an application rely on the same shared code (accidental duplication rather than logical duplication), changing the shared code for one part may inadvertently break the other.
* **Performance Overhead:** Highly generalized functions may introduce unnecessary processing steps compared to a simple, specific implementation.

The goal is to find the balance. As the saying goes: *"Duplication is far cheaper than the wrong abstraction."* Determining "how DRY" to be is often a matter of experience and domain context.

## Additional considerations

Closely related to DRY is the concept of **Single Source of Truth (SSOT)**.
While DRY usually refers to logic (code), SSOT refers to data. It states that data elements should be mastered in only one place to prevent synchronization issues.

In computational analysis, the line between data and code often blurs.
A prime example is **column names** in a DataFrame. Are they data (strings in a CSV)? Or are they code (identifiers used to access attributes)?
Regardless of the classification, having a single definition for these elements is always advantageous.

## Example

The following Python script illustrates how the line between code and data blurs, and how applying DRY can prevent "magic strings" from polluting your code.

**The "WET" (Write Everything Twice) approach:**

```python
import pandas as pd

# Create a sample fighter df
data = {
    'Name': ['Hans', 'Urs', 'Fritz', 'Luzia', 'Greta'],
    'Age': [28, 34, 30, 25, 29],
    'City': ['Zurich', 'Bern', 'Lucerne', 'Geneva', 'Lausanne']
}
fighter_df = pd.DataFrame(data)

# Accessing columns using string notation
# "Name" and "Age" are hardcoded strings repeated multiple times.
print(fighter_df['Name'])  # Output: Series with names
print(fighter_df['Age'])   # Output: Series with ages

# Accessing columns using attribute notation
print(fighter_df.Name)     # Output: Series with names
print(fighter_df.Age)      # Output: Series with ages

```

In the script above, the concepts *Name* and *Age* appear as string literals multiple times. If the data source changes (e.g., the column is renamed to `"Vorname"`), you must hunt down and replace every occurrence of the string `"Name"`.

**A DRY version of this script:**

```python
import pandas as pd
from types import SimpleNamespace

# Define the column names once and for all (Single Source of Truth)
fighter_cn = SimpleNamespace()  # Acts like a dictionary where keys are attributes
                                # (`cn` is an abbreviation for column name.)
fighter_cn.name = 'Name'
fighter_cn.age = 'Age'
fighter_cn.city = 'City'

# Create a sample fighter DataFrame using the variables
data = {
    fighter_cn.name: ['Hans', 'Urs', 'Fritz', 'Luzia', 'Greta'],
    fighter_cn.age: [28, 34, 30, 25, 29],
    fighter_cn.city: ['Zurich', 'Bern', 'Lucerne', 'Geneva', 'Lausanne']
}
fighter_df = pd.DataFrame(data)

# Accessing columns using the defined variables
print(fighter_df[fighter_cn.name])  # Output: Series with names
print(fighter_df[fighter_cn.age])   # Output: Series with ages

```

For a script this short, defining a namespace seems like overkill. However, in a real project, this approach is powerful:

1. **Refactoring is trivial:** If a column name changes, you update `fighter_cn` in one place, and the entire codebase adapts automatically.
2. **IDE Support:** Modern IDEs provide autocompletion for variables (`fighter_cn.name`), but not for string literals.
3. **Error Catching:** If you type `fighter_cn.naame`, the script crashes immediately (or the IDE flags it) because the attribute doesn't exist. If you type `fighter_df["Naame"]`, the script might run silently until it creates a new, empty column or crashes much later in the pipeline.

---

Source:\

* Hunt, A., & Thomas, D. (2019). The Pragmatic Programmer: Your journey to mastery. Addison-Wesley. ISBN 9780135957059. (Original publication)
