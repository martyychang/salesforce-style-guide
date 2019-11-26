# Apex Style Guide

This guide prescribes styles where conventions may be established
and maintained without exception.

## Collections

The three main collection types in Apex are `Set`, `List` and `Map`.
For all three types, name the variable as a singular noun or an adjective
followed by the explicit collection type.

Collection Variable Name | Type                   | Description
------------------------ | ----                   | -----------
`accountList`            | `List<Account>`        | A list of **Account** records.
`contactIdSet`           | `Set<Id>`              | A set of Contact ID values.
`accountMapByName`       | `Map<String, Account>` | A map of accounts with Account Name as the key.
`expectedMap`            | `Map<String, String>`  | A map of expected output values with input values as keys.
