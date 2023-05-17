---
sidebar_position: 14
---

# Hooks & Tags

## Hooks

Earlier we saw how `Backgrounds` could be used remove duplication between scenarios. This is similar to a `setup` method, but only for concepts that make sense to the business. There may be technical tasks that need to be performed, which have no place in the feature file, such as:

- starting a web server
- clearing up temporary files
- truncating a database table

SpecFlow provides hooks for this purpose. Peruse the [hooks documentation](https://docs.specflow.org/projects/specflow/en/latest/Bindings/Hooks.html) at your leisure.

A hook is simply a public method annotated with one of the following:

- `[BeforeScenario]`: runs before each scenario
- `[AfterScenario]`: runs after each scenario

You can have as many hooks as you need.

Create a `ShoutyHooks` class next to your step definition classes and create a `BeforeScenario` hook
and an `AfterScenario` hook in it.

Remember the `[Binding]` attribute we added to our new step definition class earlier? SpecFlow
also needs this attribute to find hooks.

Make each hook print a different string to the console using `Console.WriteLine`.

Run SpecFlow. Is the output on the console as you expected?

:::info NOTE
Due to the way output to the screen is buffered, your print statements may not interleave as expected with SpecFlow’s output. Check that they’re in the right order
:::

## Ordered Hooks

Now add another set of `BeforeScenario` and `AfterScenario` hooks. What order are the two `BeforeScenario` and `AfterScenario` hooks firing in?

There are situations when the order that hooks run in is critical, and SpecFlow gives you some control over this.
This is done by supplying an integer with the annotation: `[BeforeScenario(Order = 4)]`

`BeforeScenario` hooks execute in ascending order, `AfterScenario` hooks also execute in ascending order.

If you don’t specify an order in the annotation, SpecFlow defaults it to `10000`. Remove the order attribute from one of your annotations to confirm this.

We recommend that you define related `BeforeScenario` and `AfterScenario` hooks next to each other.

# Tags

SpecFlow allows you to add free-text tags to your features, scenarios, scenario outlines and example tables (see Scenario Outline sections):

- tags are an `@` character followed by some text (without any white space)
- tags applied to a feature apply to every scenario in that feature
- tags are case sensitive
- you can apply as many tags to a feature/scenario as you wish

SpecFlow converts the tags into **_"Traits"_** or **_"Categories"_** which you can use to selectively run scenarios in your test-runner.

Lets use the VisualStudio Test Explorer window to just run a single **_"Work in Progress"_** scenario.

- Add a `@wip` tag to one of the scenarios
- Run SpecFlow to confirm all scenarios are still green
- Open the Test Explorer window
- Type `Trait:wip` in to the Search text box, and press enter
- `Run all` will now only execute the scenario you tagged as `@wip`

## Tagged Hooks

Some hooks are only relevant for certain scenarios. To enable you to control the execution of a hook you can supply a tag value:

```csharp
[BeforeScenario("@SpecialTest")]
```

Hooks tagged in this way will only run if the current scenario also has this tag on it. Try it out.

:::tip DISCUSS

Can you work out how to create a tagged hook that runs for multiple tags?

:::
