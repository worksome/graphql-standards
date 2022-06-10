# Non-nullable lists

## Summary

> One paragraph explanation of the change.

All fields with a list value **MUST** be non-nullable.

## Motivation

> Why are we doing this? What use cases does it support? What is the expected
outcome?

A list **MUST** never be null as it allows for better handling of empty queries (the value SHALL either be an empty list, or a list populated with a specified type).

## User impact

> Is the impact on users major? How will they benefit from this proposal?

None, unless the user is checking for nullable list values. Users will benefit from this change as they will know that a list value will always be returned for a list field.

## Design Proposal

> The core of proposal. How does it work? What are the pros/cons? What alternatives
> where there and why this solution over them?

When declaring a list field, the value **MUST** always be a list (either empty, or populated). By always enforcing a value, we are letting end-users know that this will never be null.

> ❌ Invalid
```graphql
type Company {
    """
    The lack of non-nullable enforcement means that this can either be `[]`, `null`, or a populated list.
    This means that end-users would need to implement checks for both `null` and an empty list.
    """
    invoices: [Invoice!]
}
```

> ✅ Valid
```graphql
type Company {
    """
    The use of non-nullable enforcement means that the value will only ever be `[]` or a populated list.
    """
    invoices: [Invoice!]!
}
```

## Implementation

> How should this be implemented in the automated tool for validating the rules?

It **MUST** visit all fields with a value type of list, and check that it is defined as non-nullable.
