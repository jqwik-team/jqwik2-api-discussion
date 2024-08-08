# Jqwik 2 API Discussion

Let's discuss and figure out some aspects of the new Jqwik 2 API

Jqwik 2 will - in some areas - have a different or re-worked API from jqwik 1.
It's not going to be backwards-compatible. 
Nevertheless, it shouldn't be different just for the sake of being different.

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
- Test Data Builder module: Use arbitraries for generating example data for example-based tests


### Core

- Allows to create _arbitraries_ of fundamental types and to map, filter and compose them.

- Allows to generate values from arbitraries by providing a generation source.
  The generation source can be a pseudo-random one or represent the recording of a previously generated random source.

- Provides the capability of specifying _properties_ for certain pieces of code.

- Allows to validate properties by executing them.

- Validating properties can be done in many different and configurable ways,
  e.g. by generating random sets of input data with a fixed number of tries - or trying all possible values unless a max duration is reached.
  Validation can be successful, failed or aborted.
  A failed validation will also report all or a subset of falsifying examples that have been identified.

- Validating a property can be a statistical process, e.g. "validation must succeed in 95% of all tries".

- It must be possible to change the default configuration for validating properties in a straightforward way.

- It must be possible to change the validation configuration for a specific property concisely.


### JUnit Platform Engine

- Provide all necessary annotations to use Jqwik 2 just like Jqwik 1.

- Stick to Jqwik 1 names where reasonable, and deviate where necessary.
 

## Glossary

- **Arbitrary**: A composable abstraction of arbitrary values of a given type.
  An arbitrary includes all constraints that reduce the set of all possible values.

- **Property**: The four main aspects of a property are...

  1. The arbitraries describing the input data
  2. An optional set of additional preconditions to make the property meaningful
  3. The code under test
  4. The invariants and postconditions that must hold.
     Invariants and postconditions are often expressed by _assertions_ within the code under test.
 
  If one or more invariants fail in a _try_ (or a statistically relevant number of tries), the property is considered to be falsified.

- **Try**: A single execution of a property with a specific set of test data.
