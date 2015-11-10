# Core design principles for software developers

@venkat_s
venkats@agiledeveloper.com
http://www.agiledeveloper.com

## Keep it simple

KISS.

- simple keeps you focused
- simple solves only real problem we know about
- simple solutions fail less
- simple is easier to understand

## Complexity

- inherent vs accidental
  + for example: concurrency
- simple vs familiar
  + for example: a for loop is NOT simple. it's familiar

## Postpone

Delay decisions as much as possible.
Tomorrow we are smarter than today,
so we can probably implement it better.

manual testing -> change something -> are you crazy?

automated testing -> change something -> give it a try

## Cohesion

Cohesion = doing one thing and do it well.

## Coupling

Worst form of coupling - inheritance.

When tests are so tightly coupled to code that it's hard to change the code -> your design sucks

"knock out before you mock out"

Good design has high cohesion and low coupling.

Reduce coupling by depending on interfaces instead of implementations.
