---
sidebar_position: 7
---

# Snippets

## Multiple shouters

Let’s make sure that our system can handle more than one person shouting.

Add this scenario to the feature file:

```gherkin title="HearShout.feature"
# ...

Scenario: Multiple shouters
  Given Lucy is at 0, 0
  And Sean is at 0, 500
  And Oscar is at 1100, 0
  When Sean shouts
  And Oscar shouts
  Then Lucy should not hear Oscar
  But Lucy should hear Sean
```

When you run SpecFlow you’ll see some errors. Look in the console output and you’ll see that SpecFlow has generated some template code for you - look for the text:

```
No matching step definition found for one or more steps.
```

:::tip discuss

- What is SpecFlow telling us?
- Should you always copy the generated snippet into your step definition file?
- Can you think of any reasons why you might have to edit the generated snippet?

:::

## Snippets

When SpecFlow comes across a step that doesn’t match any existing step definitions it signals that there is an **_undefined_** step and the scenario containing that step is also marked as **_skipped_** or **_inconclusive_** . For each **_undefined_** step SpecFlow prints out some skeleton code (called a **_snippet_**) that you can use in your step definition class.

SpecFlow also allows you to generate step definitions for undefined steps from the feature file. Use the `Define steps...` (or `Generate Step Definitions`) command from the context menu. You can either generate a new step definitions class, or you can copy the snippets to your clipboard, to paste into an existing class.
The snippet is only a suggestion and you should edit the and the regular expression method’s parameters so that they make sense in the context of your scenario.
Copy the snippets and paste them into your step definition file and run SpecFlow again. Edit the method name as well.

### PendingStepException

The default implementation of a snippet is to throw a `PendingStepException`. What do you think will happen when you run SpecFlow now?
You’ll see that the error has changed from `undefined` to `pending` (shown as **skipped** or inconclusive). The `PendingStepException` is treated as a special case by SpecFlow. It shows that the development team is still working on the step definition.

### Signalling an error

Comment out the line that is throwing the `PendingStepException` and run SpecFlow again.

:::tip discuss

What happened this time and why?

:::

SpecFlow considers that any step definition that doesn’t throw an exception has passed. By commenting out the "pending" statement we’ve changed this step from `pending` to `passed`.

If you now replace the commented out line with:

```csharp
throw new System.InvalidOperationException("bad step")
```

Run SpecFlow, you’ll see the step has gone from `passed` to `failed`.

## SpecFlow Lifecycle

When SpecFlow runs the first thing it does is load all the step definitions. Then, each time it tries to run a step it searches through these step definitions looking for matches:

- 0 matches => Undefined step, fail scenario & emit snippet
- 1 match => Run the step definition
- more than 1 match => Ambiguous step definition & fail scenario

### Get to green

Now implement the new step definitions so that all the scenarios pass. You didn’t have to write any production code to make this scenario pass.

:::tip discuss

Is this healthy? What problems might this show?

:::

### Refactor your step definitions

Take a look at your Step definitions. Do you notice anything you don’t like? If you do, refactor them and run SpecFlow between each change so you know you haven’t broken anything.
