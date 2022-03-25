The guiding principle is "no underscores", which is a reminder to pay attention
to details. Salesforce out-of-the-box will auto-generate API names for many
common components such as objects and fields, but sadly those API names use
underscores as filler to replace special characters and spaces. The result is
that uncoordinated implementations will result in the creation of _things_
in the org like the following.

* **# of Users** number field (`Account.of_Users__c`)
* **Platforms** number field (`Account.Platforms__c`) on one object and 
  **Platforms** _checkbox_ field on a different object
* Child relationships that have cryptic API names like `Contact.Accounts1__r`,
  `Lead.Accounts2__r` or `Opportunity.Accounts3__r`

If you care to avoid such tragedies, talk to your team about adopting
a few simple habits.

1. Agree to use a shared style guide. Feel free to fork this one to start!
2. Update the guide as you go. Create new styles where none exist
   for the feature you're implementing, and update existing styles when
   the team agrees to change things up for new development.
3. Use pull requests as a means for discussing, enforcing and converging
   style across all developers. This will take some time in the beginning
   but with repetition will soon become second nature.
4. Sync up regularly to not only talk about cool new features but also about
   updates to the team's style guide.

# Say no to underscores

Below are step-by-step instructions for getting rid of underscores and making
your components look as if they came natively out of the box.

1. Write the label in plain English
2. Expand common abbreviations
3. Drop to lowercase
4. Strip or delete special characters (e.g., hyphens)
5. Replace spaces with underscores to create a `snake_case` name
6. Convert `snake_case` to `CamelCase`
7. Apply well known conventions (e.g., `Is` prefix for checkbox fields)

## Example: Auto-POST Job Status

Step | Result
---- | ------
Write the label in plain English | Auto-POST Job Status
Expand common abbreviations | Auto-POST Job Status
Drop to lowercase | auto-post job status
Strip special characters | autopost job status
Replace spaces with underscores | autopost_job_status
Convert to `CamelCase` | AutopostJobStatus
Apply well known conventions | AutopostJobStatus

## Example: PayPal Transaction No.

Step | Result
---- | ------
Write the label in plain English | PayPal Transaction No.
Expand common abbreviations | PayPal Transaction Number
Drop to lowercase | paypal transaction number
Strip special characters | paypal transaction number
Replace spaces with underscores | paypal_transaction_number
Convert to `CamelCase` | PaypalTransactionNumber
Apply well known conventions | PaypalTransactionNumber

# Contents

Below are conventions for different component types, ordered by
the current label (e.g., Aura Component vs. Lightning Component)
seen in the latest Salesforce release notes and other documentation.

## Custom fields

Custom fields should be named following the conventions below.

### URL fields

URL fields should be named with the word "URL" in the label,
unless the name is well known (e.g., website) to imply a URL.

Object Label  | Field Label   | Field API Name
------------- | ------------- | --------------
Account       | Website       | `Website`
Auth Provider | Authorize URL | `AuthorizeUrl`
Auth Provider | Error URL     | `ErrorUrl`

## Custom settings

Custom settings come in two types: hierarchy and list.

### Hierarchy settings

Hierarchy settings should be named with a descriptor
and end with the word "Setting".

Custom Setting Label | API Name
-------------------- | -----------------------
Feature Setting      | `FeatureSetting__c`
Integration Setting  | `IntegrationSetting__c`

Conceptually this is similar to the "settings" field
in [scratch org definition files][3].

## Email templates

Email templates should be named to match the subject.
This will make it easier to locate specific email templates
when troubleshooting.

See examples below.

Subject | Email Template Name | Template Unique Name
------- | ------------------- | --------------------
CTA: Rock the Vote! | CTA: Rock the Vote! | `CtaRockTheVote`
Big Deal Alert | Big Deal Alert | `BigDealAlert`
What's on your mind? | What's on your mind? | `WhatsOnYourMind`
Account Name Changed to {!Account.Name} | Account Name Changed | `AccountNameChanged`

## Flows

Object-specific flows should be prefixed with the object's API name.
Omit the namespace for objects from a managed package if possible.

Object API Name | Flow Label | Flow API Name
--------------- | ---------- | -------------
`outfunds__Disbursement__c` | Disbursement: Submit for Full Approval | DisbursementSubmitForFullApproval
`Opportunity` | Opportunity: Submit for Finance Review | OpportunitySubmitForFinanceReview

Record-triggered flows should be limited to a maximum of five per object, one in each context.

Flow Label | Flow API Name
---------- | -------------
Account: Before Create | AccountBeforeCreate
Account: After Create | AccountAfterCreate
Account: Before Update | AccountBeforeUpdate
Account: After Update | AccountAfterUpdate
Account: Before Delete | AccountBeforeDelete

If you must split record-triggered flows for ease of maintenance,
keep the object label and context as a prefix.

Flow Label | Flow API Name
---------- | -------------
Account: After Update Create Follow-up Task | AccountAfterUpdateCreateFollowupTask
Account: After Update Alert on Finance Hold | AccountAfterUpdateAlertOnFinanceHold
Account: After Update Alert on Poor Health | AccountAfterUpdateAlertOnPoorHealth

## Permission sets

Keep the scope of each permission set meaningful, and choose one of these
two naming conventions.

### Action-oriented permission set

This permission set grants a user access to perform a specific action
or well known set of actions. Simple examples below.

Label | API Name
----- | --------
Convert Leads | `ConvertLeads`
Hide Salesforce Classic | `HideSalesforceClassic`
Manage Closed Opportunities | `ManageClosedOpportunities`

### Feature-oriented permission set

This permission set grants a user access to a robust feature for which
fine-grained control of specific cations is either unnecessary or infeasible.
Simple examples below.

Label | API Name
----- | --------
DML History App | `DmlHistoryApp`
Lightning Dialer | `LightningDialer`
Lightning Experience | `LightningExperience`

## Workflow rules

Workflow rules should be named as imperative statements.

Rule Name | Description
--------- | -----------
Alert Operator on Account Name Change | Send an email to operators when Account Name changes.

Prefer evaluating the rule when a record is "created, and every time it's edited".

### Email alerts

Email alerts should be named to match the associated email template.

Email Alert Field | Email Template Field
----------------- | --------------------
Description | Subject
Unique Name | Template Unique Name	

### Field updates

Field updates are named like assignment statements in Apex,
using the field label in the **Name** and the field name
in the **Unique Name**. The new value should also be included.

Name | Unique Name
---- | -----------
Old Account Name = PRIORVALUE | OldNamePriorvalue
Success Plan = NULL | SuccessPlanNull
Success Plan = Premier | SuccessPlanPremier

# How to contribute

This repo is configured to [publish a GitHub Pages site from the `/docs` folder 
on the `master` branch][1], using the [Leap Day theme][2].
Feel free to create issues or pull requests into `master` update the guide!

[1]: https://help.github.com/en/articles/configuring-a-publishing-source-for-github-pages#publishing-your-github-pages-site-from-a-docs-folder-on-your-master-branch
[2]: https://github.com/pages-themes/leap-day
[3]: https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_scratch_orgs_def_file_config_values.htm
