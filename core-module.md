# Core Module

Provides everything needed to create and evaluating properties programmatically.

The core module will be independent from any concrete testing framework or assertion framework.
Thus it can be used from anywhere, e.g. JUnit Jupiter, TestNG or Spock.

Ideally, the only dependencies are `org.opentest4j` and `org.apiguardian`.

## Required API Capabilities

- [Basic interfaces for arbitraries and generators](https://github.com/jqwik-team/jqwik2-api-discussion/issues/1),
  which allow to map, filter and transform them.

- Create _arbitraries_ of fundamental types.

- Compose several arbitraries into new ones.

- Generate values (samples) from arbitraries by providing a generation source.
  The generation source can be a pseudo-random one or represent the recording of a previously generated random source.

- Specifying _properties_ for certain pieces of code.

- Validate properties by executing them.

- Validating properties can be done in many different and configurable ways,
  e.g. by generating random sets of input data (samples) with a fixed number of tries - or trying all possible values unless a max duration is reached.
  Validation can be successful, failed or aborted.
  A failed validation will also report all or a subset of falsifying samples that have been identified.

- Statistical validation must be possible, e.g. "Succeed in 95% of all tries".

- Check the distribution of generated values as part of invariants.

- Change the default configuration for validating properties in a straightforward way.

- Change the validation configuration for a specific property concisely.
