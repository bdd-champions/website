---
sidebar_position: 1
---

import Tabs from "@theme/Tabs";
import TabItem from "@theme/TabItem";

# Getting Started

This is a hands-on tutorial for automating BDD scenarios using Cucumber and SpecFlow. By completing this tutorial you will have practice using all the meaningful features of these tools and confidence in your ability to apply them to real-world projects.

## Business Concept

You will be developing a new social media app - with some similarities to Twitter - called **Shouty**. Users of the app will be able to ’shout’ - and will be ’heard’ by other users who are within 1000 meters of the shouter.

Shouty will initially support the following use case:

- Local Business Promotions e.g. "Half price coffee at Barney’s Café until 12 today"

The target platform is GPS-enabled smartphones.

Functional Requirements:

- Shouts should be text only - limited to 2000 characters
- The range of shouts should be 1000m

User Story:

> As a business owner I want Shouty users within range to receive my promotional shouts So that I can generate more business

## Select your programming language

<Tabs groupId="lang">
<TabItem value="C#">

**What you'll need:**

- **Visual Studio 2022**, Visual Studio 2019, or Visual Studio 2017 (Community, Professional or Enterprise edition)
- **.NET Core v3.1** (alternatively `TargetFramework` in the `.csproj` files can be changed to `net6.0`)
- **SpecFlow extension for Visual Studio**

**We recommend:**

- Visual Studio 2022

</TabItem>
<TabItem value="Java">

**What you'll need:**

- TODO: JDK version

**We recommend:**

- IntelliJ

</TabItem>
<TabItem value="JavaScript">

**What you'll need:**

- [Node.js](https://nodejs.org/en/download/) version 16.14 or above:

**We recommend:**

- VS Code

</TabItem>
<TabItem value="TypeScript">

**What you'll need:**

- [Node.js](https://nodejs.org/en/download/) version 16.14 or above:

**We recommend:**

- VS Code

</TabItem>
</Tabs>

## Import the code into your IDE

<Tabs groupId="lang">
<TabItem value="C#">

Clone the Shouty project from [`https://github.com/cucumber-examples/shouty.net`](https://github.com/cucumber-examples/shouty.net) and open it in Visual Studio.

</TabItem>
<TabItem value="Java">

TODO

</TabItem>
<TabItem value="JavaScript">

TODO

</TabItem>
<TabItem value="TypeScript">

TODO

</TabItem>
</Tabs>

:::warning Proxy Issues

If dependency installation stalls or errors it may be blocked by your corporate proxy. Try disconnecting from your work VPN to install dependencies. You should only need to do this step once.

:::

:::caution Dependencies

There's no need to modify the project configuration or dependency versions to get the code to work. Many have come before you and done just fine. If you see a dependency that needs updating please let us know.

:::

## Run the Tests

<Tabs groupId="lang">
<TabItem value="C#">

- Open the `Shouty.NET.sln` file in Visual Studio
- Select `Test` > `Run` > `All Tests` from the menu, or press `CTRL-R, A`

</TabItem>
<TabItem value="Java">

</TabItem>
<TabItem value="JavaScript">

```shell title="Run the tests."
npm run test
```

</TabItem>
<TabItem value="TypeScript">

```shell title="Run the tests."
npm run test
```

</TabItem>
</Tabs>

:::info Check the output

If you see two tests passing and two tests failing, you're good to go.

:::
