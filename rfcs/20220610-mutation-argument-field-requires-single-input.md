# Mutations argument field requires single input

## Summary

> One paragraph explanation of the change.

All mutations **MUST** have a single input object named `input`.

## Motivation

> Why are we doing this? What use cases does it support? What is the expected
> outcome?

This is being done to have consistency with the usage of mutations. It does not allow for any extra use-cases, it
just makes the schema prettier and easier to work with.

## User impact

> Is the impact on users major? How will they benefit from this proposal?

The impact on users will be major as all their mutation requests will now have to use a single input object.
They will benefit by having a more streamlined schema and reduce confusion for developers on what casing to use.

## Design Proposal

> The core of proposal. How does it work? What are the pros/cons? What alternatives
> where there and why this solution over them?

When defining a mutation, this makes it much easier for developers to work with as they know there is only a single
input object with the argument name "input". It also allows for re-usable input types, and for a single point (the input
object) to update the required input fields.

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

## Implementation

> How should this be implemented in the automated tool for validating the rules?

It **MUST** visit all mutation definitions and check that there is a single input with a name of "input".
