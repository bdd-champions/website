---
sidebar_position: 4
---

# BDD Cycle

## Failing tests

:::caution

Run the tests if you haven't already.

:::

Can you work out how to run SpecFlow so that it executes the scenarios in the feature file? When you run your tests you should see a mixture of passing and failing scenarios and tests.

#### Questions

<details>
  <summary>What is the name of the passing scenario?</summary>

`InRangeShoutIsHeard`

</details>

<details>
  <summary>What is the name of the failing scenario?</summary>

`OutOfRangeShoutIsNotHeard`

</details>
<details>
  <summary>What is the name of the passing programmer test?</summary>

`ItCalculatesTheDistanceFromItself`

</details>
<details>
  <summary>What is the name of the failing programmer test?</summary>

`ItCalculatesTheDistanceFromAnotherCoordinateAlongXAxis`

</details>

:::tip DISCUSS

How would you explain to your product owner what is wrong with Shouty, from what you see in the test results?

:::

## Getting to green

It’s time to write the production code that will make the failing programmer test pass. You should not need to edit the feature file, the step definition file or the programmer test file.

:::info HINT
There’s a commented out line of code in the `Coordinate` file that will get the test passing.
:::

Run all the tests again. Both the programmer tests should be passing, but one of the scenarios
should still be failing.

:::tip DISCUSS
Does the code you have just uncommented look like a complete solution?
:::

Now, open the **programmer test** file and uncomment the programmer test that is commented out.

Run all the tests again.

:::tip DISCUSS

- Which programmer test(s) are failing?
- Which scenario(s) are failing?
- Can you see what changes you have to make to get the new programmer test to pass?

:::

:::info HINT
Use Pythagoras' theorem.
:::

Keep working and running all the tests until you see all the programmer tests, steps and scenarios pass.

## Where are we?

Now that we've got everything passing we've moved into new territory in the BDD Cycle.

![BDD Process](/img/shouty/bdd-process.png)

1. Decide the next user story to work on
2. Use concrete examples to explore and discover the acceptance criteria for the user story
3. Formulate a concrete example as a scenario
4. Automate a scenario and see it fail
5. Write a programmer test and see it fail
6. Write enough code to make the programmer test pass
7. Refactor to clean up the code
8. Manual exploratory testing
9. Release to production

:::tip DISCUSS

Where are we now? What do we need to do next?

:::
