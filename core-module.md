# Core Module

Provides everything needed to create and evaluating properties programmatically.

The core module will be independent from any concrete testing framework or assertion framework.
Thus it can be used from anywhere, e.g. JUnit Jupiter, TestNG or Spock.

Ideally, the only dependency is to `org.opentest4j`.

## API Needs

- Create _arbitraries_ of fundamental types and to map, filter and transform them.

- Composing several arbitraries into one

- Allows to generate values (samples) from arbitraries by providing a generation source.
  The generation source can be a pseudo-random one or represent the recording of a previously generated random source.

- Provides the capability of specifying _properties_ for certain pieces of code.

- Allows to validate properties by executing them.

- Validating properties can be done in many different and configurable ways,
  e.g. by generating random sets of input data (samples) with a fixed number of tries - or trying all possible values unless a max duration is reached.
  Validation can be successful, failed or aborted.
  A failed validation will also report all or a subset of falsifying samples that have been identified.

- Statistical validation must be possible, e.g. "Succeed in 95% of all tries".

- Checking the distribution of generated values as part of invariants.

- It must be possible to change the default configuration for validating properties in a straightforward way.

- It must be possible to change the validation configuration for a specific property concisely.
