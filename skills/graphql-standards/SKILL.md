---
name: graphql-standards
description: Worksome's GraphQL schema standards — naming conventions, nullability, mutation input shape, and description requirements. Use ONLY when authoring, modifying, or reviewing GraphQL schema files (`.graphql`, `.graphqls`, SDL in code) or when the user mentions GraphQL types, queries, mutations, inputs, or enums. Do NOT apply these rules to non-GraphQL code.
metadata:
  source: https://github.com/worksome/graphql-standards
  conformance: RFC 2119
---

# GraphQL Standards

These rules apply **only** when working with GraphQL files (schema definitions in `.graphql` / `.graphqls`, or GraphQL SDL embedded in code). Do not apply them to other languages or formats.

The keywords **MUST**, **MUST NOT**, **SHOULD**, **MAY**, etc. follow [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

When in doubt about the motivation behind a rule, consult the corresponding RFC in [`rfcs/`](https://github.com/worksome/graphql-standards/tree/main/rfcs).

---

## 1. Field names MUST be camelCase

All field names on any node type MUST be camelCase.

- ❌ `email_address`, `FullName`, `DAY_OF_BIRTH`
- ✅ `emailAddress`, `fullName`, `dayOfBirth`

RFC: [`rfcs/20220602-camel-case-fields.md`](https://github.com/worksome/graphql-standards/blob/main/rfcs/20220602-camel-case-fields.md)

---

## 2. Input types MUST be suffixed with `Input`

Every `input` type's name MUST end in `Input`.

```graphql
# ❌ Invalid
input Review { stars: Int!, commentary: String }

# ✅ Valid
input ReviewInput { stars: Int!, commentary: String }
```

RFC: [`rfcs/20220602-input-suffix-input-type.md`](https://github.com/worksome/graphql-standards/blob/main/rfcs/20220602-input-suffix-input-type.md)

---

## 3. All nodes MUST have a description

Every node — types, fields, arguments, queries, mutations, enums, enum values — MUST have a description (`"""..."""`).

```graphql
"""An invoice that is stored."""
type Invoice {
    """The global identifier for the invoice."""
    id: ID! @globalId
    """A number referencing the invoice. Used by booking and finance systems."""
    number: String!
}
```

RFC: [`rfcs/20220609-descriptions-required-for-all-nodes.md`](https://github.com/worksome/graphql-standards/blob/main/rfcs/20220609-descriptions-required-for-all-nodes.md)

---

## 4. `id` fields MUST be non-nullable

Any field named `id` (or `ID`) MUST be non-nullable — it is the primary key of its type.

```graphql
# ❌ Invalid
type User { id: ID }

# ✅ Valid
type User { id: ID! }
```

RFC: [`rfcs/20220609-non-nullable-ids.md`](https://github.com/worksome/graphql-standards/blob/main/rfcs/20220609-non-nullable-ids.md)

---

## 5. List fields MUST be non-nullable on output types

List-valued fields on **output types** MUST be non-nullable (so the value is always `[]` or a populated list, never `null`). List fields on **input types** MAY be nullable.

```graphql
# ❌ Invalid (output type)
type Company { invoices: [Invoice!] }

# ✅ Valid
type Company { invoices: [Invoice!]! }

# ✅ Valid (nullable list permitted on input)
input CompanyInput { owners: [String!] }
```

RFCs:
- [`rfcs/20220609-non-nullable-lists.md`](https://github.com/worksome/graphql-standards/blob/main/rfcs/20220609-non-nullable-lists.md)
- [`rfcs/20220620-non_nullable_lists_input_types-fields.md`](https://github.com/worksome/graphql-standards/blob/main/rfcs/20220620-non_nullable_lists_input_types-fields.md)

---

## 6. Items inside lists MUST be non-nullable

The element type inside any list MUST be non-nullable, so consumers never have to check for `null` entries.

```graphql
# ❌ Invalid
type Company { invoices: [Invoice]! }

# ✅ Valid
type Company { invoices: [Invoice!]! }
```

RFC: [`rfcs/20220610-non-nullable-types-in-lists.md`](https://github.com/worksome/graphql-standards/blob/main/rfcs/20220610-non-nullable-types-in-lists.md)

---

## 7. Mutations MUST take a single `input` argument

Every mutation MUST accept exactly one argument, named `input`, whose type is a dedicated `Input` object.

```graphql
# ❌ Invalid
mutation ($currency: CurrencyType!, $company: Company!) {
    updateInvoiceCurrency(company: $company, currency: $currency) { ... }
}

# ✅ Valid
input UpdateInvoiceCurrencyInput {
    currency: CurrencyType!
    company: Company!
}

mutation ($input: UpdateInvoiceCurrencyInput!) {
    updateInvoiceCurrency(input: $input) { currency, value }
}
```

RFC: [`rfcs/20220610-mutation-argument-field-requires-single-input.md`](https://github.com/worksome/graphql-standards/blob/main/rfcs/20220610-mutation-argument-field-requires-single-input.md)

---

## 8. Object types MUST be PascalCase

All object type names MUST use PascalCase.

```graphql
# ❌ Invalid
type userInvoice { }

# ✅ Valid
type UserInvoice { }
```

RFC: [`rfcs/20220610-pascal-case-object-types.md`](https://github.com/worksome/graphql-standards/blob/main/rfcs/20220610-pascal-case-object-types.md)

---

## 9. Enum values MUST be `UPPER_SNAKE_CASE`

All enum cases MUST use upper snake case.

```graphql
# ❌ Invalid
enum Status { Active, fulfilled, in_progress }

# ✅ Valid
enum Status { ACTIVE, FULFILLED, IN_PROGRESS }
```

RFC: [`rfcs/20230210-upper-snake-case-enum-cases.md`](https://github.com/worksome/graphql-standards/blob/main/rfcs/20230210-upper-snake-case-enum-cases.md)

---

## How to apply

When reviewing or editing GraphQL schema content:

1. Confirm the file is GraphQL (SDL) — if it isn't, this skill does not apply.
2. Walk each rule above against the change. Each rule's status in the linting tooling is in [`rules.md`](https://github.com/worksome/graphql-standards/blob/main/rules.md) (auto-fixed, checked-only, or missing).
3. If a rule needs nuance beyond the summary here, open the linked RFC for the original reasoning.
4. New rules cannot be invented on the fly — they go through the [RFC process](https://github.com/worksome/graphql-standards/blob/main/rfcs/README.md) first.
