# Vocabulary

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

## User Controls
I know we've been over this a few times - but just to confirm:

Seems we have three types of user controls:
1. Those which both authenticate and authorise users (we know who they are and what they are allowed to do)  - a closed user group
2. Those which just authenticate users (we know who they are) - an open user group
3. Those which neither authenticate nor authorise users but can count them (like the open web) - a public user group.

Does this cover the ground?

## Format Constraint
We introduced the Reproduce, Print, and Format actions as forms of distribution where the asset is transformed in its presentation. For example, the data might be presented in a charted form.

Sometimes, the form in which it is presented is controlled by the vendor. To cover this use case, we could introduce a format constraint on the action that specifies the type of presentation permitted. 

To avoid the intricacies of actually specifying this, we could instead introduce a duty to ensure that the format is vendor approved.

This use case is an interesting example of how the semantics of constraints and duties differ. To discus!

## Storage
We've identified Store as an action. But we've said nothing about what kind of storage is allowed. One pressing issue is whether cloud storage is permitted. So I suggest we support a storage constraint on the action which offers two values: on-prem storage and cloud storage. Are there any other values we should add?

## Duty Targets
The target of a duty identifies the entity over which the duty action is taken. Unlike permissions, this is not a dataset. We've never explicitly specified these. So, what exactly are these targets? It depends on the duty:

For [attachment duties], we have Attributions, Disclaimers, or Proscriptions.

For [agreement duties], we have Licenses and Proscriptions. We may have to add NDAs (for prospective customers).

For [notification duties], we have two types of Notification - notification of the start of use by a new internal user (i.e. a new location) and notification of the start of use by a new external organisation (i.e. a service facilitator).

For [reporting duties], we identify two types of Report: usage reports and honesty statements. Is there a difference? Is the first generated from an access control system like DACS and the second not?

Then we have the [Request and Consent] pattern, in which we make Appeals for an audit, a free trial, a service facilitatot, a new recipient, and, maybe, a format (see above). So four or five types of Appeal.

Finally, we [invoice and compensate] Payments.

## Tiered Payments
We presently can't support tiered payments - so one price for, say, for the firm and up to five affiliates, and a higher price for the firm and more than five affiliates.

To do so, we could provide a tier constraint which activates the applicable payment duty. So in the affiliates example, we'd provide two payment duties with two different tier constraints. Which ever duty matched the actual number of affiliates would activate. The other would remain dormant.


