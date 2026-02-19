# Coding strategies

## Rubber ducking

The "rubber ducking" technique is a debugging classic. Simply put, it involves explaining your code, line-by-line, to an inanimate object—traditionally a rubber duck sitting on your desk.

Verbalizing your logic forces you to slow down and articulate your thoughts. Even without feedback from the duck, this externalization often reveals logical inconsistencies or obvious errors that you missed while reading silently.

While associated with debugging, rubber ducking is equally powerful *before* code is written:

1. **Planning**: explain the problem and your intended solution to the duck. This clarifies requirements before you write a single line.
2. **Designing**: Narrate your architectural decisions. This helps spot structural flaws early.
3. **Pseudocode**: Verbalize your logic while drafting pseudocode to ensure the algorithm flows naturally.
4. **Testing**: Explain the "why" behind each test case to ensure you are covering edge cases effectively. (We will cover testing in detail in [0716UnitTesting.md](https://www.google.com/search?q=/jump_to_id/0716UnitTesting.md)).

Rubber ducking is also the secret to mastering **Large Language Models (LLMs)**.
Treat the LLM prompt as your rubber duck. By typing out a detailed, step-by-step explanation of your problem to the AI, you are effectively rubber ducking. This often leads to you solving the problem yourself, or at the very least, providing the LLM with the context it needs to give a high-quality answer.

---

## Practical approach to writing and developing a script with rubber ducking

Rubber ducking is not just a mental trick; it is a practical workflow for writing better scripts.

There is no "correct" way to do it, but the following step-by-step guide offers a structured way to integrate this strategy into your development process:

1. **Define the problem/task**:
* **Rubber ducking step**: Tell the duck exactly what problem you are solving, including context and constraints.
* **Outcome**: A clear, unambiguous goal.
* **In practice**: Write this definition into the `docstring` of your script.
*Recall: Docstrings are the triple-quoted strings (`"""..."""`) at the very top of a file.*
*Example (Task 05 from Section 04):*
```python
"""Exploratory script to get the first view of the fight data.

This script loads the fight data from a CSV file into a pandas DataFrame,
finds all the unique names, and compiles the set of characters used in the
fighter names.
"""
...

```




2. **Outline your approach**:
* **Rubber ducking step**: Talk through the steps required to reach the solution. Break the big problem into small, manageable chunks.
* **Outcome**: A structural roadmap of the script.
* **In practice**: Write these steps as comments in your file. This creates a "recipe" for your code.
*Example:*
```python
"""Exploratory script to get the first view of the fight data.
...
"""
# Import needed packages

# Set the path to the fight_data.csv

# Read the CSV with pandas

# Get the column names and print them

# Identify the column names with fighter names

# Get all unique fighter names and display the count

# Make a collection of all characters used in names

```




3. **Write pseudocode**:
* **Rubber ducking step**: For each step in your outline, explain the specific logic to the duck. How exactly will you achieve that step?
* **Outcome**: A refined algorithm. You will identify areas where you are unsure of the implementation details.
* **In practice**: Expand your outline comments into detailed pseudocode. ideally, every line of pseudocode corresponds to one future line of real code.
*Example:*
```python
...
# Get all unique fighter names and display the count
# - First, select the two columns
# - Get all of the values from the two columns
# - Flatten the array to 1D (combine the values of the two columns)
# - Get all unique values
# - Sort the unique names (for good measure)
# - Print output
...

```




4. **Implement the code**:
* **Rubber ducking step**: As you type, explain what each function or line is doing.
* **Outcome**: You catch syntax errors and logic bugs in real-time. You also verify if your planned approach actually works in practice.
* **In practice**: Translate your pseudocode into Python.
*Note: You will likely need to adjust your plan. The goal is to solve the problem, not to blindly follow your initial pseudocode. If the code requires a different approach, update your mental model (and your comments) and proceed.*
*Example:*
```python
...  # (assume fight_df and fighter_columns are defined)

# Get all unique fighter names and display the count
# - First, select the two columns
_fighters_df = fight_df[fighter_columns]
# - Get all unique values
fighters = pd.unique(fight_df[fighter_columns].values.ravel())
# - Sort the unique names (for good measure)
fighters.sort()
# - Print output
print(f"Unique names in the fight dataset: {fighters.shape[0]}")
# >>> Unique names in the fight dataset: 3371
...

```




5. **Review and finalize**:
* **Rubber ducking step**: Do a final walkthrough. Explain the finished script to the duck, focusing on *how* it solves the initial problem defined in Step 1.
* **Outcome**: High-quality, readable code that is ready for others to use.
* **In practice**: Run the script to verify the output. Then, clean up your comments. The "recipe" comments (pseudocode) should either be removed (if the code is self-explanatory) or updated to explain *why* complex lines exist.
*Example:*
```python
...  # (assume fight_df and fighter_columns are defined)

# Get all unique fighter names and display the count
_fighters_df = fight_df[fighter_columns]
# Create a collection of unique elements from both fighter columns
fighters = pd.unique(fight_df[fighter_columns].values.ravel())
fighters.sort()
print(f"Unique names in the fight dataset: {fighters.shape[0]}")
# >>> Unique names in the fight dataset: 3371
...

```





---

Source:\

* Hunt, A., & Thomas, D. (2019). The Pragmatic Programmer: Your journey to mastery. Addison-Wesley. ISBN 9780135957059. (Original publication)\
* [https://realpython.com/documenting-python-code/](https://realpython.com/documenting-python-code/)\
* [https://peps.python.org/](https://peps.python.org/)\
