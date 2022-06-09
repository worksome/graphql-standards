# Descriptions required for all nodes

## Summary

> One paragraph explanation of the change.

All nodes (arguments, fields, queries, types, etc.) **MUST** have a description.

## Motivation

> Why are we doing this? What use cases does it support? What is the expected
outcome?

As this is a public API, having descriptions for everything in the API will make it much easier for third-parties (as well as our internal teams) to develop using the API.

## User impact

> Is the impact on users major? How will they benefit from this proposal?

No impact to users, however enforcing this has many benefits for users of the API.

## Design Proposal

> The core of proposal. How does it work? What are the pros/cons? What alternatives
> where there and why this solution over them?

When adding a new node, a description should be added at all times.

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

## Implementation

> How should this be implemented in the automated tool for validating the rules?

Check that all nodes have a description.
