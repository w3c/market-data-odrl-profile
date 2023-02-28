## Purposes
Purposes are ofter used to constrain an action, e.g. for what purpose are you deriving the data?

We have plenty of values for this property [already](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile-draft.html#usage-0-9). But several more have been suggested: risk management , profit and loss calculations , valuation, reference pricing.

Are these all distinct? Do we have any duplications? And are there any others we should consider?

"Internal business purposes" appears quite frequently. Is it simply a shorthand for all the purposes - or does it have a specific meaning that we need to capture?

## Assignees Vs Users
The Assignee List property was supposed to identify the organisations in a rights assigment. But as we've modelled it [in the pattern book](https://w3c.github.io/market-data-odrl-profile/patterns_temp.html#assignment-patterns), we're applying geography and line-of-business constraints to the assignees. Are we confusing the assignees of a permission with its users?

The former is supposed to model the contractual rights assignment between organisations. The latter is supposed to model the individual users of the permission (be they people or machines), Perhaps constraints like geography and line-of-businees belong only on the user, not on the assignee.

## Counts across User Type
Sometimes the number of users is constrainted, e.g. no more than 100 users.

Until now, we've used a simple "less than" constraint with an integer value. But there are cases where the limit on numbers carries across user types, e.g. less that 100 users both internally and among your service providers.

To model this we can introduce the concept of a "count lock" that can be applied across user types (and permissions). We can also indicate "concurrent count locks" to capture some realtime use cases. But do we need to? Is this a significant use case?

## Geography Constraints
We can use the UN's [Standard Country or Area Codes](https://unstats.un.org/unsd/methodology/m49/) to identify geographic regions and countries.

Similarly, we can use the UN's [Code for Trade and Transport Locations](https://unece.org/trade/uncefact/unlocode) to identify localities like cities.

Should we recommend use of these standards? And are there any other geographic distinctions that we need to capture?

