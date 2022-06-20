# Enforce NonNullable list requirement on output types only

## Summary

> One paragraph explanation of the change.

All output types **MUST** have non-nullable lists fields

## Motivation

> Why are we doing this? What use cases does it support? What is the expected
outcome?

Sometimes users would like to not supply a list when doing input objects.  
However as the rules enforces all list to be non-nullable, this is not possible

## User impact

> Is the impact on users major? How will they benefit from this proposal?

None. There are no breaking changes, it's only loosening the current rules

## Design Proposal

> The core of proposal. How does it work? What are the pros/cons? What alternatives
> where there and why this solution over them?

When creating a list, it can be nullable if it is not an output type.  
Output type is defined as per graphql spec http://spec.graphql.org/draft/#sec-Input-and-Output-Types.

Essentially this means that all lists which are on an `input` object are allowed to be null, however not
enforced to be null. The following is now valid.

> :white_check_mark: Valid
```graphql
input PersonInput {
    friends: [String!]
    parents: [String!]!
}
```

## Implementation

> How should this be implemented in the automated tool for validating the rules?

Check the type definition of the field and check if that is of type `input`.
If it is then skip it.
