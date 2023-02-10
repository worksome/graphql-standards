# `UPPER_SNAKE` case enum cases

## Summary

> One paragraph explanation of the change.

All enum cases **MUST** use `UPPER_SNAKE` case.

## Motivation

> Why are we doing this? What use cases does it support? What is the expected
outcome?

This is being done to have consistency with the naming of enum cases. It does not allow for any extra use-cases, it
just makes the schema prettier. The expected outcome is a schema where the casing is unified and well-defined.

## User impact

> Is the impact on users major? How will they benefit from this proposal?

The impact on users will be major as all their enum cases will now have to follow the new naming convention for enum
cases.
They will benefit by having a more streamlined schema and reduce confusion for developers on what casing to use.

## Design Proposal

> The core of proposal. How does it work? What are the pros/cons? What alternatives
> where there and why this solution over them?

When defining an object type, the developer has to decide what casing to use for the object name, by always enforcing a
specific case we are taking that decision away from the developer and streamlining all object names.  
This means when creating a query all the object types will always have the same casing.

> ❌ Invalid

```graphql
enum Status {
    case InProgress
    case approved
    case investigationUnderway
}
```

> ✅ Valid

```graphql
enum Status {
    case IN_PROGRESS
    case APPROVED
    case INVESTIGATION_UNDERWAY
}
```

> Why `UPPER_SNAKE` case over pascal case or other casing?

The main reason is that this is what is used in examples on [graphql.org](https://graphql.org/learn/schema#enumeration-types).

## Implementation

> How should this be implemented in the automated tool for validating the rules?

It **MUST** visit all enum case definitions and check that the name is `UPPER_SNAKE` case.
