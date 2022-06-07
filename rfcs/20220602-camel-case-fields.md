# CamelCase fields

## Summary

> One paragraph explanation of the change.

All fields **MUST** be camelCase.

## Motivation

> Why are we doing this? What use cases does it support? What is the expected
outcome?

This is being done to have a consistency on field names. It does not allow for any extra use-cases, it just makes the
schema prettier.  
The expected outcome is a schema where the casing is unified and well defined.

## User impact

> Is the impact on users major? How will they benefit from this proposal?

The impact on users will be major as all their fields will now have to follow the new naming convention for fields.  
They will benefit by having a more streamlined schema and reduce confusion for developers on what casing to use.

## Design Proposal

> The core of proposal. How does it work? What are the pros/cons? What alternatives
> where there and why this solution over them?

When defining a field, the developer has to decide what casing to what the field in, by always enforcing a specific
case we are taking that decision away from the developer and streamlining all fields.  
This means when creating a query all the fields will always have the same casing also.

> :x: Invalid
```graphql
type user {
    email_address: String!
    FullName: String!
    DAY_OF_BIRTH: Date!
}
```

> :white_check_mark: Valid
```graphql
type user {
    emailAddress: String!
    fullName: String!
    dayOfBirth: Date!
}
```

> Why camelCase over snake_case or other casing?

Main reason is because this is what is used in examples on [graphql.org](https://graphql.org).


## Implementation

> How should this be implemented in the automated tool for validating the rules?

It should visit all field definitions and check that the name is camel case.