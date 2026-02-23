## Rubber Ducking <i class="fa-solid fa-crow"></i>

{% if slide %}

Explain your code to an inanimate object out loud and line by line.

Verbalizing logic forces you to **slow down** and often reveals bugs you missed while reading silently.

{% else %}

The "rubber ducking" technique comes from a simple idea: explain your code, line by line, to an inanimate object, traditionally a rubber duck on your desk.
Verbalizing your logic forces you to slow down and articulate your reasoning. Without any feedback from the duck, this process alone often reveals logical inconsistencies or obvious errors you missed while reading silently.

{% endif %}

{% if slide %}

:::{admonition} Not just for debugging
:class: tip

Works *before* code exists too:

1. **Planning**: explain the problem and your intended solution
2. **Designing**: narrate architectural decisions
3. **Pseudocode**: verbalize logic while drafting algorithms
4. **Testing**: explain the "why" behind each test case
:::

Variation: Write down with pen on paper the pseudo code and logic.

{% else %}

While commonly associated with debugging, rubber ducking is equally useful *before* any code is written:

1. **Planning**: explain the problem and your intended solution to clarify requirements.
2. **Designing**: narrate your architectural decisions to spot structural flaws early.
3. **Pseudocode**: verbalize your algorithm while drafting it to ensure it flows naturally.
4. **Testing**: explain the reasoning behind each test case to ensure edge cases are covered.


Variation: Write down with pen on paper the pseudo code and logic.

{% endif %}

{% if page %}

### Rubber ducking and LLMs

Rubber ducking is also the secret to using Large Language Models effectively.
Treat the prompt as your duck: by typing out a detailed, step-by-step explanation of your problem, you often solve it yourself.
At the very least, you give the LLM exactly the context it needs for a useful answer.

### A practical workflow

There is no single correct way to rubber duck, but the following steps offer a structured approach:

1. **Define the problem**: Tell the duck what you are solving, including context and constraints. Write this definition into the docstring of your script.

   ```python
   """Exploratory script to get the first view of the fight data.

   This script loads the fight data from a CSV file into a pandas DataFrame,
   finds all the unique names, and compiles the set of characters used in
   the fighter names.
   """
   ```

2. **Outline your approach**: Talk through the steps. Write them as comments like a "recipe" for your code.

   ```python
   # Import needed packages
   # Set the path to the fight_data.csv
   # Read the CSV with pandas
   # Get the column names and print them
   # Get all unique fighter names and display the count
   ```

3. **Write pseudocode**: For each step, explain the specific logic. Expand your comments into detailed pseudocode.

4. **Implement**: Translate pseudocode into real code. Adjust the plan as needed. The goal is solving the problem, not following your initial sketch blindly.

5. **Review**: Walk through the finished script with the duck. Clean up comments: remove what the code already makes obvious, keep what explains *why*.

{% endif %}
