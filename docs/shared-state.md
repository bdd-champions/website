---
sidebar_position: 11
---

# Shared State

## Add another scenario

Now we’re going to add a new scenario:

```gherkin title="HearShout.feature"
#...

Scenario: Multiple shouts from one person
  Given Lucy is at 0, 0
  And Sean is at 0, 500
  When Sean shouts
  And Sean shouts
  Then Lucy should hear 2 shouts from Sean

```

:::info note

You will not need to change any production code to get this scenario to pass.

:::

## Isolation

Tests should not depend on each other - they should run in **_isolation_**. You should be able to run tests in any order and get the same result.

We have been running several scenarios and Sean has been shouting in most of them.

:::tip discuss

How is it that in the scenario that you have just implemented Lucy has only heard 2 shouts from Sean?

:::

**SpecFlow helps maintain isolation by instantiating all step definition classes before every scenario.**

### Growing your specification

Right now we have a single feature file and a single step definition file. You’ve already learnt that a feature file acts as the specification of one capability of your application. Your application will have many capabilities and there will be many feature files. It is tempting to create a single step definition for each feature file, but this is not a good idea. Remember that SpecFlow loads all step definitions when it starts - and they all exist in a single, global scope.

Instead create step definition files aligned to your domain entities (such as customer, account, fund). If you organise your step definitions like this, then it will be easier to find the step definition that you need, no matter which feature file you are working with.

### Separating the step definitions

Even though we have only just started with this application, we already have step definitions for 2 domains in a single step definition file:

- Location domain: the step(s) that say where a person is located
- Shout domain: the step(s) that control the shouting and hearing of messages

Create a new step definition class, `LocationStepDefinitions`, and move the steps that deal with location into it. In order to make it compile, copy the `shouty` field declaration and initialization as well.

You will need to annotate the `class` with `[Binding]` attribute. **SpecFlow uses this attribute to find classes which contain step definitions.**

:::tip discuss

What problem is this going to cause? What happens if you run SpecFlow now?

:::

## Sharing state

We need some way to share state between our step definition classes, while at the same time maintaining isolation between our scenarios. SpecFlow encourages you to do this by using a feature called context injection. Context injection is a simplified implementation of Dependency Injection (DI), using a built-in DI container of SpecFlow. (You can also configure SpecFlow to use an external DI container as well, but the built-in one is just enough for the majority of projects.)

The problem you encountered when splitting the existing step definitions between 2 classes was sharing the `ShoutyNetwork` instance. As the `Shouty` class is a simple class with a default constructor, we can use context injection to let SpecFlow create the `ShoutyNetwork` instance.

To be able to use this, the following changes have to be made in in **both** step definition classes:

1. Remove the field initializer of the `shouty` field, so that the declaration should be `private readonly ShoutyNetwork shouty;`.
2. Create a constructor for the step definition class with a parameter of `ShoutyNetwork` and
   initialize the `shouty` field from the parameter in the constructor body.

The constructor parameter of the step definition class instructs SpecFlow to manage the
`ShoutyNetwork` instance and inject it to all step definition class instances that need it.

Run SpecFlow.

:::tip discuss

What happens? How many instances of the ShoutyNetwork are created?

:::

### `ShoutyNetwork` is production code

You may have noticed that we are now leaving SpecFlow to initialize our `ShoutyNetwork`, which is in our production code. Production code often has complex initialization code, and various dependencies that change based on different configurations. So sometimes we need another solution.

There’s a famous computer science quote by David Wheeler, which says:

> All problems in computer science can be solved by another level of indirection

And that’s just what we’re going to do here.

1. Create a `ShoutyContext` class in the `Shouty.Specs` project
2. In `ShoutyContext`, create a property called `Shouty` of type `ShoutyNetwork` and initialize it using `new`
3. Replace direct references to `ShoutyNetwork` in the step definition classes with references to `ShoutyContext` and use its `Shouty` property to access the shouty network.

Run SpecFlow again. All scenarios should still be passing.

Context injection got its name from the "context" classes we use to wrap the data we would like to share across multiple step definition classes.

The [SpecFlow docs on Context-Injection](https://docs.specflow.org/projects/specflow/en/latest/Bindings/Context-Injection.html#examples) provide a nice example for reference.
