# Jqwik 2 API Discussion

Let's discuss and figure out some aspects of the new Jqwik 2 API.

Jqwik 2 will - in some areas - have a different or re-worked API from jqwik 1.
It's not going to be backwards-compatible. 
Nevertheless, it shouldn't be different just for the sake of being different.

Many of the implementation challenges for Jqwik 2 have already been successfully tackled in a [proof of concept](https://github.com/jqwik-team/jqwik2-poc),
but the API is open for discussion.

## API principles

- Make simple things obvious, make complicated things possible.
- Have one standard way of doing things; provide alternative(s) for convenience if and only if it reduces the mental load significantly.
- Prefer existing terms and words over new ones, unless the existing terms suggest the wrong thing.
- Divide the API into different modules if the modules have significant values on their own.
- Use a new package namespace, e.g. `net.jqwik2` to allow Jqwik 1 and 2 side-by-side for easier migration.

## API modules

Unlike Jqwik 1 version 2's **core** will be independent from any concrete testing framework.
Thus it can be used from anywhere, e.g. JUnit Jupiter, TestNG or Spock.

In addition, there will be a **JUnit Platform engine**, which provides the same lifecycle support and tight IDE integration as Jqwik 1.

Other considered modules:
- JUnit Jupiter module with convenience extensions for easier usage with JUnit Jupiter.
- Kotlin module to offer an idiomatic Kotlin API.
- Model-based testing module with support for linear temporal logic and parallel execution.
- Time module
- Web module
- Test Data Builder module: Use arbitraries for generating sample data for example-based tests


### Core

See [core module](./core-module.md).

### JUnit Platform Engine

- Provide all necessary annotations to use Jqwik 2 just like Jqwik 1.

- Stick to Jqwik 1 names where reasonable, and deviate where necessary.

### JUnit Jupiter Extension

- Provide extension with lifecycle hooks for property validation and replay of failed samples

- Hook into Jupiter logging and reporting

- Use JUnit Platform configuration
 
## API Discussion

Discussion about specific API questions is happen through [issues](https://github.com/jqwik-team/jqwik2-api-discussion/issues) 

Open discussions are:

- [Arbitraries, Generators and Transformations](https://github.com/jqwik-team/jqwik2-api-discussion/issues/1)
- [Creating Arbitraries of Fundamental Types](https://github.com/jqwik-team/jqwik2-api-discussion/issues/2)
- [Combining Arbitraries](https://github.com/jqwik-team/jqwik2-api-discussion/issues/3)
- [Specifying and Validating Properties](https://github.com/jqwik-team/jqwik2-api-discussion/issues/4)
- [Package naming scheme](https://github.com/jqwik-team/jqwik2-api-discussion/issues/5)

## Glossary

- **Arbitrary**: A composable abstraction of arbitrary values of a given type.
  An arbitrary includes all constraints that reduce the set of all possible values.

- **Property**: The four main aspects of a property are...

  1. The arbitraries describing the input data, including boundaries and other constraints from the domain.
  2. An optional set of additional preconditions - called **assumptions** - that make the property meaningful.
  4. The code under test
  5. The invariants and postconditions that must hold.
     Invariants and postconditions are often expressed by _assertions_ within the code under test.

- **Property Validation**: Running a property's _code under test_ with _samples_ that comply with the _preconditions_.
  Validation is successful if invariants and postconditions hold in all runs.
  **Statistical Validation** can weaken the "all runs" rule by requiring only a certain percentage of runs to comply with invariants.

- **Sample**: The concrete set of values used in one _try_. The sample must follow all preconditions.

- **Try**: A single execution of a property with a specific set of test data.
