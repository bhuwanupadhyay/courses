# Modularity

This concept is universal in software development. 
It is the ability to break a system into smaller, more manageable pieces.

For example, in java we have the concept of packages.

> A package is a namespace that organizes a set of related classes and interfaces.

Modularity can be measured using metrics: cohesion, coupling, and connascence. 

## Cohesion

Cohesion refers to what extent the parts of a module should be contained within the same module.

> Attempting to divide a cohesive module would only result in increased coupling and decreased readability. - Larry Constantine

Ranges of cohesion measures (best to worst):
- Functional cohesion
- Sequential cohesion
- Communication cohesion
- Procedural cohesion  
- Temporal cohesion
- Logical cohesion
- Coincidental cohesion

## Coupling

Coupling refers to the extent to which the parts of a module depend on each other.

## Connascence

Connascence refers to the extent to which the parts of a module are aware of each other.