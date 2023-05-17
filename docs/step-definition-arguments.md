---
sidebar_position: 5
---

# Step definition arguments

The `Sean is at {int}, {int}` and `Lucy is at {int}, {int}` Cucumber Expression are almost identical except for the person’s name. We’re already using `{int}` output parameters to extract the coordinates and pass them to the step definition.

The [Cucumber Expression docs](https://github.com/cucumber/cucumber-expressions#readme) are quite helpful here. Take a moment to review them.

Let’s replace the person’s name in the Cucumber Expression with another output parameter so that the person’s name is also passed to the step definition as an argument.

In the first of the existing step definitions, replace `Lucy` with `{word}` to make it an output parameter that matches a word:

`{word} is at {int}, {int}`

Now that the cucumber expression has 3 output parameters, the step definition method is going to need an equal number parameters.

:::tip Discuss
What type should the new parameter be? What’s a good name for it?
:::

Replace the hard-coded `"Lucy"` in the body of the step definition method with your new parameter.

Run SpecFlow. You should get a `BindingException` because of an ambiguous step definition.

:::tip Discuss

- What do you think an ambiguous step definition is?
- What should you do to fix it?

:::

Run SpecFlow and check everything is still working as before.

:::info
Cucumber Expression are new to SpecFlow and to be able to use it an additional NuGet package, CucumberExpressions.SpecFlow.3-7 has to be added to the project. Even if you have enabled Cucumber Expressions, you can still use Regular Expressions as well. In the exercise above, using `(.*)` instead of `{int}` and `{word}` provides the same result.
:::
