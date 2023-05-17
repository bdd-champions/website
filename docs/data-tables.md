---
sidebar_position: 10
---

# Data tables

If you look at the **_Multiple shouters_** scenario that includes Sean, Lucy, and Oscar you can see that it’s a bit hard to read. SpecFlow and Gherkin let you use **_data tables_** in a step, which can help you remove clutter and improve the readability of the specification. The scenario could be simplified by using a data table, like this:

```gherkin
 Given people are located at
    | name  | x    | y   |
    | Lucy  | 0    | 0   |
    | Sean  | 0    | 500 |
    | Oscar | 1100 | 0   |
```

Modify the scenario and run SpecFlow. You should get an undefined step error, because this is a new step. Look at the **_snippet_** that has been emitted, which defines a step definition that takes a `TechTalk.SpecFlow.Table` parameter .

There are a number of ways that you can use this parameter (see the following page), but to start with let’s keep it simple and use the `Table.Rows` property, which returns a collection of objects that implement the `IDictionary<string, string>` interface. There’s an entry in the collection for each row (except the heading).

You can use this in your step definition to see an example.

```csharp
foreach (var row in table.Rows)
  {
      // access cells by e.g. row["name"]
  }
```

:::tip discuss

How much do you like the look of the code?

:::

Next, create a new class `PersonLocation` (in the `Shouty.Specs` project) with public properties called
`Name`, `X`, and `Y`.

Then, change the step definition parameter from `Table` to `PersonLocation[]`.

When you run SpecFlow you should get an `InvalidCastException` exception because SpecFlow doesn’t know how to convert the data table to a `PersonLocation` array. Add the following to the `ShoutStepDefinitions` class:

```csharp title="ShoutStepDefinitions.cs"
// ...

[StepArgumentTransformation]
public PersonLocation[] ConvertPersonLocations(Table personLocationsTable)
{
    return personLocationsTable.Rows
        .Select(row => new PersonLocation
        {
          Name = row["name"],
          X = int.Parse(row["x"]),
          Y = int.Parse(row["y"])
        }).ToArray();
}
```

Now you can change the implementation of your stepdef to iterate over the list.

:::tip discuss

Is the code more readable?

:::

Now get the scenario passing again.

## The "Assist" table helper functions

The `Rows` property is very useful, but included in the `TechTalk.SpecFlow.Assist` namespace are some extension methods of `Table` that provide some further functionality. The [SpecFlow.Assist helpers docs](https://docs.specflow.org/projects/specflow/en/latest/Bindings/SpecFlow-Assist-Helpers.html) are helpful here.

- `CreateSet<T>()` — This method will create an instance of `T` for each non-header row of the table. It will try to match the row headers with the names of public properties of `T` and set them using the values found in each row.
- `CreateInstance<T>()` — Works similarly to `CreateSet`, but creates a single instance from data tables that have either a single data row or _field_ and _value_ columns and a row for each field setting.
- `CompareToSet<T>(IEnumerable<T>, bool)` and `CompareToInstance<T>(T)` — These helper methods can be used in `Then` steps to assert that a list of `T` objects contain the property values that were specified in the data table.

Change your implementation of the `ConvertPersonLocations` method to use the `CreateSet` method. Don’t forget to add a namespace using to the `TechTalk.SpecFlow.Assist` namespace.
