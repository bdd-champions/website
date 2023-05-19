---
sidebar_position: 9
---

# Scenario outlines

The first 2 scenarios in our feature file look almost identical. The only difference is that Sean is in a slightly different location, which affects whether Lucy can hear his shout or not.

We can combine these 2 scenarios using a single scenario **_outline_**.

```gherkin title="HearShout.feature"
# ...

Scenario Outline: only hear in-range shouts
  Given Lucy is at 0, 0
  And Sean is at <Seans-location>
  When Sean shouts
  Then Lucy should hear <what-Lucy-hears>

  Examples: some simple examples
    | Seans-location | what-Lucy-hears |
    | 0, 900         | Sean            |
    | 800, 800       | nothing         |
```

The lines that follow the `Examples` keyword are a Gherkin **_table_**. Each column is separated by a **_pipe_** character `|` and each new line is a separate row. The first row of the table contains column headings, which match text in the scenario outline.

Now replace the first 2 scenarios in `HearShout.feature` with the single scenario outline above and run SpecFlow again. You may find that you only need to edit the feature file - your existing step definitions probably won’t need changes.

:::tip discuss

- How many scenarios does Cucumber now report as passing?
- A scenario outline can be followed by multiple `Examples` tables each with their own name. Why might you want to do this?

:::
