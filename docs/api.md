---
sidebar_position: 16
---

# Gherkin API

Gherkin has 5 keywords that we use to introduce steps: `Given`, `When`, `Then`, `And`, `But`.

If you look in our feature file you’ll see that we use 4 of them already. Now look in the step definition file - how many different attributes can you find? Why is that?

Change `And Sean is at 0, 900` in the feature file to `When Sean is at 0, 900` and run SpecFlow.

What happens now?

How does SpecFlow decide which step definition to run for And steps?

Try changing an `And` in your Gherkin to `*`.

What happens when you run SpecFlow?

Now undo those edits so that the scenarios make sense to us again.
