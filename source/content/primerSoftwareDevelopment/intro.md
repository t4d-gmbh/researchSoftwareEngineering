{% if slide %}
## Why Software Development Principles?

::::{grid} 2
:::{grid-item-card} The Problem
- Research code often starts as a quick script
- "Just get it working" turns into 5000 lines nobody understands
- Including your future self, six months later
:::
:::{grid-item-card} The Fix
- A handful of principles go a long way
- They reduce bugs, ease collaboration, and save time
- Not rules to memorize, rather habits to develop
:::
::::

{% else %}

## Why Software Development Principles?

Most research code starts as a quick script: load data, run analysis, plot results.
That script grows. Parameters get hardcoded, functions get copy-pasted, and before long you have a tangled mess that only works on your machine, with your data, on a good day.

The principles in this section are not abstract theory. They are practical guidelines that help you write code you can actually maintain, share, and trust.
We focus on three ideas:

1. **Good coding practices**: making code readable and consistent.
2. **Orthogonality**: keeping unrelated parts of your code independent.
3. **DRY**: avoiding unnecessary repetition.

None of these require advanced programming skills. They are about discipline and awareness, and they pay off immediately.

{% endif %}
