---
sidebar_position: 15
---

# Custom Parameters

We saw how SpecFlow captures certain parts of our steps and passes them as arguments to our step definitions. Output parameters declared as `{int}` will be passed as integers. Output parameters declared as `{word}` and `{string}` will be passed as strings.

Sometimes it’s useful to be able to pass more meaningful arguments to our step definitions. This is easy with custom parameter types. Let’s try this out with our `Coordinate` class.

Create a new class in the `Shouty.Specs` project called `Conversions` and add the following code:

```csharp title="Conversions.cs"
[Binding]
public class Conversions
{
    [StepArgumentTransformation(@"(\d+), (\d+)")]
    public Coordinate ConvertCoordinate(int xCoord, int yCoord)
    {
        return new Coordinate(xCoord, yCoord);
    }
}
```

The `[StepArgumentTransformation]` attribute defines a regular expression to capture our location notation, passes the matching values to the method, which then returns a new `Coordinate` object.

Change your step definition from:

```csharp
[Given(@"{word} is at {int}, {int}")]
public void GivenPersonIsAt(string name, int xCoord, int yCoord)
{
    shoutyContext.Shouty.SetLocation(name, new Coordinate(xCoord, yCoord));
}
```

to

```csharp
[Given("{word} is at {Coordinate}")]
public void GivenPersonIsAt(string name, Coordinate coordinate)
{
    shoutyContext.Shouty.SetLocation(name, coordinate);
}
```

Run SpecFlow and all scenarios should still be green.

Move the other `StepArgumentTransformation` method you created earlier to convert the data table
also to the newly created `Conversions` class.

You can now add different `StepArgumentTransformation`s which will deal with place names rather than coordinates, e.g. North Pole is at `0, 0`. See if you can add the transformation and change Lucy’s location to the North Pole.
