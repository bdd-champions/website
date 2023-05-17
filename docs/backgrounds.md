---
sidebar_position: 13
---

# Backgrounds

Sometimes each scenario in a feature file repeats exactly the same `Given` step(s). It can be useful to remove this duplication by placing them in a `Background` which gets run before **_each_** scenario. In our example Lucy is always at `0, 0` so we could move this step into a background.

```gherkin
Background:
  Given Lucy is at 0, 0
```

Create this background in your feature file and remove the references to `Lucy is at 0, 0` from all the scenarios. Run SpecFlow again to make sure it’s all still working.

Remember, though, that the purpose of the feature file is to make the specification of the system easy to read. Moving steps out of a scenario and into a background can make it harder to read the feature file, because now each scenario now needs to be read in conjunction with the background.

```

```
