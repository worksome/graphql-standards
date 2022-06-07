# Input types suffixed with `input`

## Summary

> One paragraph explanation of the change.

All input types **MUST** be suffixed with `input`. 


## Motivation

> Why are we doing this? What use cases does it support? What is the expected
outcome?

When suffixing all input types with `input` it will make it clearer that the node is of input type.  
This also helps on a common case where an object and input type is named the same, as the name will not collide.

## User impact

> Is the impact on users major? How will they benefit from this proposal?

The impact is rather big as all users would have to change the naming of their input object to follow this new
convention.

## Design Proposal

> The core of proposal. How does it work? What are the pros/cons? What alternatives
> where are there and why this solution over them?

When defining an input object the name should end with `Input`. It removes name collisions with objects as often an
input object is created for an object.  
It will also help people realize that it is a node of input type, as the name clearly states it.

> :x: Invalid
```graphql
input Review {
  stars: Int!
  commentary: String
}
```
> :white_check_mark: Valid
```graphql
input ReviewInput {
  stars: Int!
  commentary: String
}
```

> Why suffix instead of prefix?

This proposal was made because that is how it is done on [graphql.org](https://graphql.org/learn/schema/#input-types)


## Implementation

> How should this be implemented in the automated tool for validating the rules?

Check if node is of input object type and check that the name ends with `Input`.
