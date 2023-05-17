---
sidebar_position: 12
---

# Test Strategy

## Testing pyramid

The testing pyramid tells us that we’re better off with fewer end-to-end tests and more unit tests. This is because end-to-end tests are typically:

- slow
- brittle
- difficult to diagnose when they fail

The pyramid also emphasises that there will always be a certain amount of manual and exploratory testing needed.

![Testing pyramid](/img/shouty/pyramid.png)

## Testing iceberg

The testing pyramid doesn’t help us answer the question:

**_When should I write my test using SpecFlow and when using MsTest?_**

We learnt earlier that SpecFlow is primarily a collaboration tool, not a test automation tool. So, the answer to the question is:

**_When writing the test in business language will help communication._**

The overriding question when choosing SpecFlow or your unit testing framework is:

**_Will the business be interested enough in this scenario to give meaningful feedback?_**

![Testing iceberg](/img/shouty/iceberg.png)

## SpecFlow and non .NET interfaces

Some of the scenarios that the business are interested in will be written as end-to-end tests. This means that SpecFlow may need to interact with web applications or REST services. SpecFlow doesn’t know anything about HTML or web browsers, so what should we do?

All that SpecFlow can do is run .NET step definitions and, luckily, we can use any of the .NET libraries that specialise in interacting with diverse interfaces, such as web browsers or REST services. Some of the more popular libraries are:

- [Playwright](https://playwright.dev/dotnet/): to interact with web browsers
- [RestSharp](https://restsharp.dev/): to interact with HTTP/REST APIs

We can interact directly with C# production code from our SpecFlow step definitions. For direct interaction with other languages there are implementations of Cucumber in several other languages.
