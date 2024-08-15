# Core Module

Provides everything needed to create and evaluating properties programmatically.

The core module will be independent from any concrete testing framework or assertion framework.
Thus it can be used from anywhere, e.g. JUnit Jupiter, TestNG or Spock.

Ideally, the only dependencies are `org.opentest4j` and `org.apiguardian`.

## Required API Capabilities

- [Basic interfaces for arbitraries and generators](https://github.com/jqwik-team/jqwik2-api-discussion/issues/1),
  which allow to map, filter and transform them.

- [Create _arbitraries_ of fundamental types](https://github.com/jqwik-team/jqwik2-api-discussion/issues/2).

- [Compose several arbitraries](https://github.com/jqwik-team/jqwik2-api-discussion/issues/3) into new ones.

- [Specifying _properties_ and validating](https://github.com/jqwik-team/jqwik2-api-discussion/issues/4) them by running code.

- Since property validation is highly configurable, the validation result must contain and report a lot of details
  to allow proper interpretation. 
  Also, a failed validation must report all or a subset of falsifying samples that have been identified.

- Generate values (samples) from arbitraries directly by providing a generation source.
  The generation source can be a pseudo-random one or represent the recording of a previously generated random source.

- Check the distribution of generated values as part of invariants.

- Change the default configuration for validating properties in a straightforward way.

