# Rules
The GraphQL Standard defines a set of rules which **MUST** be followed.

Each rule has a badge explaining its status in the linting tool. The following badges are used:
- ![linting](https://img.shields.io/badge/linting-auto-blue) 
- ![linting](https://img.shields.io/badge/linting-checks-blue)
- ![linting](https://img.shields.io/badge/linting-missing-red)

The difference is if it is automatically fixed, only checked or completely missing. 


## CamelCase field name ![linting](https://img.shields.io/badge/linting-auto-blue)
All field names **MUST** be camelCase.  

When creating a field under any node type, the field names should always be written in camelCase.

> ❌ Invalid
```graphql
type user {
    email_address: String!
    FullName: String!
    DAY_OF_BIRTH: Date!
}
```

> ✅ Valid
```graphql
type user {
    emailAddress: String!
    fullName: String!
    dayOfBirth: Date!
}
```

## Suffix input type with `Input` ![linting](https://img.shields.io/badge/linting-auto-blue)
All input types **MUST** be suffixed with `Input`

When creating an input type node, the name should always be suffixed with `Input`.

> ❌ Invalid
```graphql
input Review {
  stars: Int!
  commentary: String
}
```
> ✅ Valid
```graphql
input ReviewInput {
  stars: Int!
  commentary: String
}
```

## Description required for all nodes ![linting](https://img.shields.io/badge/linting-auto-blue)
All nodes (arguments, fields, queries, types, etc.) **MUST** have a description.

When a new node of any type is created a description shall be available for it.

> ❌ Invalid

```graphql
type Invoice {
    id: ID! @globalId
    number: String!
}
```

> ✅ Valid

```graphql
"""
An Invoice that is stored.
"""
type Invoice {
    """
    The global identifier for the invoice.
    """
    id: ID! @globalId
    """
    A number referencing the invoice.

    This is usually printed on the invoice itself and should be used by booking system and finance departments.
    The format is a human readable format.
    """
    number: String!
}
```

## ID fields are non-nullable ![linting](https://img.shields.io/badge/linting-auto-blue)
All fields named `ID` (or `id`) **MUST** be non-nullable.

When declaring an ID field, this should always have a value as it is the primary key of the type.

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

## Lists are non-nullable ![linting](https://img.shields.io/badge/linting-auto-blue)
All fields with a list value **MUST** be non-nullable.

When declaring a list field, the value **MUST** always be a list (either empty, or populated).

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

## Mutation have one `input` argument field ![linting](https://img.shields.io/badge/linting-auto-blue)
All mutations **MUST** have a single input object named `input`.

> ❌ Invalid

```graphql
# Mutation with multiple input variables
mutation ($currency: CurrencyType!, $company: Company!) {
    updateInvoiceCurrency(company: $company, currency: $currency) {
        title
        company {
            name
        }
    }
}
```

> ✅ Valid

```graphql
# Input Type
input UpdateInvoiceCurrencyInput {
    currency: CurrencyType!
    company: Company!
}

# Request mutation with single input variable named "input"
mutation ($input: UpdateInvoiceCurrencyInput!) {
    updateInvoiceCurrency($input: UpdateInvoiceCurrencyInput!) {
        currency
        value
    }
}
```

## Types in list are non-nullable ![linting](https://img.shields.io/badge/linting-auto-blue)
All types inside fields with a list value **MUST** be non-nullable.

> ❌ Invalid
```graphql
type Company {
    """
    The lack of non-nullable enforcement means that this can either be `[]`, `[null]`, or a populated list of 'Invoice' types.
    This means that end-users would need to implement checks for both a list containing `null` and an empty list.
    """
    invoices: [Invoice]!
}
```

> ✅ Valid
```graphql
type Company {
    """
    The use of non-nullable enforcement means that the value will only ever be `[]` or a populated list of type 'Invoice'.
    """
    invoices: [Invoice!]!
}
```

## Pascal case object types ![linting](https://img.shields.io/badge/linting-auto-blue)

All object types **MUST** use pascal case.

> ❌ Invalid

```graphql
type userInvoice {
}
```

> ✅ Valid

```graphql
type UserInvoice {
}
```
