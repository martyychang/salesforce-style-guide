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

* [Permission sets](./permissionsets.html)

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

# How to contribute

This repo is configured to [publish a GitHub Pages site from the `/docs` folder 
on the `master` branch][1], using the [Leap Day theme][2].
Feel free to create issues or pull requests into `master` update the guide!

[1]: https://help.github.com/en/articles/configuring-a-publishing-source-for-github-pages#publishing-your-github-pages-site-from-a-docs-folder-on-your-master-branch
[2]: https://github.com/pages-themes/leap-day
