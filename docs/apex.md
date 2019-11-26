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

## `DatabaseJockey` class

Every Salesforce org should have a `DatabaseJockey` class which serves
the singular purpose of wrapping DML operations, so that Apex tests
can be true unit tests without the friction of hitting the Salesforce database.

Below is the unsurprising interface for a `DatabaseJockey`.

```java
public interface DatabaseJockey {

    /**
     * Delete a single record.
     */
    Database.DeleteResult del(SObject record);

    /**
     * Delete multiple records.
     */
    List<Database.DeleteResult> del(List<SObject> record);

    /**
     * Insert a single record.
     */
    Database.SaveResult ins(SObject record);

    /**
     * Insert multiple records.
     */
    List<Database.SaveResult> ins(List<SObject> record);

    /**
     * Update a single record.
     */
    Database.SaveResult upd(SObject record);

    /**
     * Update multiple records.
     */
    List<Database.SaveResult> upd(List<SObject> record);
}
```
