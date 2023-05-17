---
sidebar_position: 2
---

# Take a look around

Now that you've cloned the Shouty project let's have a look around. You’ll find a single feature file in the `Shouty.Specs` project and you’ll find programmer tests in one of the files in the `Shouty.Tests` project.

We’re going to take a look around and get to know what a typical C# SpecFlow test suite looks like.

There are only a few files here. Use the following diagram to help you decide what each file in the project is doing.

![Project anatomy](/img/shouty/cucumber-anatomy.png)

### 🤔 Questions 

<details>
  <summary>Which files correspond to the shapes on the diagram?</summary>


![Project anatomy](/img/shouty/cucumber-anatomy-csharp.png)

</details>


:::tip DISCUSS

Are there any files whose reason for existing is not clear? Which ones?

:::

<details>
  <summary>
  
  The feature file contains scenarios made up of steps. Each step causes SpecFlow to look for a C# step definition to run. How does SpecFlow decide which step definition to run for each step?
  
  </summary>

Step-definitions are denoted by C# attributes: 

```csharp
[Given(@"Lucy is at {int}, {int}")]
``` 

Which match steps in the Gherkin like:

```gherkin
Given Lucy is at 0, 0
```


</details>

