---
sidebar_position: 1
---

# Getting Started

```gherkin 
Scenario: Multiple shouters
  Given Lucy is at 0, 0
  And Sean is at 0, 500
  And Oscar is at 1100, 0
  When Sean shouts
  And Oscar shouts
  Then Lucy should not hear Oscar
  But Lucy should hear Sean
```