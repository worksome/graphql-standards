# Non-nullable ids

## Summary

> One paragraph explanation of the change.

All fields named `ID` (or `id`) **MUST** be non-nullable.

## Motivation

> Why are we doing this? What use cases does it support? What is the expected
outcome?

An ID is the primary key of any type, and therefore should be non-nullable as it **MUST** always have a value.

## User impact

> Is the impact on users major? How will they benefit from this proposal?

None, unless the user is checking for nullable values. Users will benefit from this change as they will know that a value will always be returned for an ID field.

## Design Proposal

> The core of proposal. How does it work? What are the pros/cons? What alternatives
> where there and why this solution over them?

When declaring an ID field, this should always have a value as it is the primary key of the type. By always enforcing a value, we are letting end-users know that this will never be null.

> ❌ Invalid
```graphql
type User {
    id: ID
}
```

> ✅ Valid
```graphql
type User {
    id: ID!
}
```

## Implementation

> How should this be implemented in the automated tool for validating the rules?

It should visit all fields, check whether the name is ID (or id) and check that it is defined as non-nullable.
