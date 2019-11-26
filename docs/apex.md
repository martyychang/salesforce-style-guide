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

## Service classes

A service class is intended to perform non-deterministic operations that
interact with the Salesforce database or with external APIs.

As a result, business logic within service classes should always
be implemented in instance methods. Furthermore, service instances
should be obtained through calls to a static `getInstance` method, which
may be overloaded.

Service classes should be named as a noun followed by the word `Service`.
Below is a sample service class that creates reminders.

```java
public with sharing class ReminderService {

    /**
     * The default number of days in the future at which to set
     * the due date for a reminder task.
     */
    @TestVisible
    private Integer defaultPeriod;

    @TestVisible
    private DatabaseJockey dj;

    @TestVisible
    private static ReminderService instance = new ReminderService(7);

    @TestVisible
    private Date referenceDate;

    private ReminderService(Integer defaultPeriod) {
        this(defaultPeriod, Date.today(), DatabaseJockey.getInstance());
    }

    private ReminderService(
        Integer defaultPeriod,
        Date referenceDate,
        DatabaseJockey dj
    ) {
        this.defaultPeriod = defaultPeriod;
        this.referenceDate = referenceDate;
        this.dj = dj;
    }

    @TestVisible
    private Date getDefaultActivityDate() {
        return this.referenceDate.addDays(this.defaultPeriod);
    }

    public static ReminderService getInstance() {
        return instance;
    }

    public Id createReminder(String subject, Id ownerId) {
        return this.dj.ins(
            new Task(
                ActivityDate = this.getDefaultActivityDate(),
                OwnerId = ownerId,
                Subject = subject
            )
        ).getId();
    }
}
```

Service classes should prefer `with sharing` as the default setting.

Instances of service classes should be named as the plural form of
the noun preceding `Service` in the class name.

```java
    /**
     * ReminderService instance to be used within another service.
     */
    private ReminderService reminders;
```
