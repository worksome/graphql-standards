# Rules
The GraphQL Standard defines a set of rules which **MUST** be followed.

Each rule has a badge explaining its status in the linting tool. The following badges are used:
- ![linting](https://img.shields.io/badge/linting-auto-blue) 
- ![linting](https://img.shields.io/badge/linting-checks-blue)
- ![linting](https://img.shields.io/badge/linting-missing-red)

The difference is if it is automatically fixed, only checked or completely missing. 


## CamelCase field name ![linting](https://img.shields.io/badge/linting-missing-red)
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