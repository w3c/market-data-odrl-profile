# July 22, 2020: Terms for Discussion

## Duty: Request

**Definition: The Debtor makes the Creditor aware of a desired state of the world (defined by the action scope).**

In this case, the Debtor is a Consumer of data; the Creditor is the Originator.

Example: A user of DBAG data would like a Service Facilitator to assist them in processing the data internally. Before they are allowed to do so, they must *request* permission. In some cases, simply making the request is enough to satisfy the terms of the agreement. But, as we'll see in the next duty, sometimes it's only the beginning of the process.

Read more: [Notification, Request, and Consent Duties](/w3c/market-data-odrl-profile/issues/6)

## Duty: Consent

**Definition: The debtor accedes to a desired state of the world (defined by the action scope).**

Often, the Debtor is the Originator who is informing the Consumer (the Creditor) of something, often that a request has been granted.

Example: A user of DBAG data has previously requested that they be allowed to use a Service Facilitator in a certain scenario. Before they can do so, DBAG must give their *consent*  that the request has been granted.

Read more: [Notification, Request, and Consent Duties](/w3c/market-data-odrl-profile/issues/6)

## Duty: Notify

**Definition: The Debtor makes the Creditor aware of a relevant change in the state of the world (defined by the action scope).**

Often, the Debtor is a Redistributor or Consumer of data, *notifying* the Originator that they've begun using a particular data product or that they've begun distributing data to a new third party.

Example: Refinitiv is required to tell DBAG before distributing uncontrolled data to a new end user. There are no additional obligations (e.g. no need to wait or approval) but they must inform the exchange before entitling their new client.

Read more: [Notification, Request, and Consent Duties](/w3c/market-data-odrl-profile/issues/6)

## Duty: Report

**Definition: The Debtor provides a report to the Creditor on a relevant state of the world (defined by the action scope).**

In most, if not all, cases, the Debtor is a Redistributor or Consumer of data, peridically updating the Originator on something happening in their jurisdiction with regards to a data set. The big difference between the notification duty modeled above and standard reporting duties is their periodicity: while notification only need happen once, reporting must be repeated.

Example: Bloomberg must send DBAG a *report* each month listing products delivered to devices under Bloomberg's entitlement control, used by professional subscribers, summarized at the location level. The action for this example has an action scope of Usage, with a unitOfCount of Device. Since the report is required monthly, the duty has a timeInterval of monthly, and the action specifies that it must be done once per month.


Read more: [Reporting Duties](/w3c/market-data-odrl-profile/issues/7)