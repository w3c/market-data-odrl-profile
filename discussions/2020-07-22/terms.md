# July 22, 2020: Terms for Discussion

Agenda: Review and agree on the universe and definitions of **actions for duties** required to describe obligations in market data contracts. A duty is "the obligation to perform an Action." The goal of this session is to agree on all the kinds of duties that are used in market data contracts.

At the same time, we'll review some of the **action scopes** that modify duties for specific use cases.

## Duty: Request

**Definition: The Debtor makes the Creditor aware of a desired state of the world (defined by the action scope).**

The Debtor is the party that wants something from the Creditor. They are the Debtor in this instance because the obligation is on them to make the request.

### Action Scopes

**Service Facilitator:** The debtor requests the creditor allow a service facilitator to access the asset.

**Audit:** The debtor requests the creditor to accede to an audit

Service Facilitator Example: A user of Exchange X data would like a Service Facilitator to assist them in processing the data internally. Before they are allowed to do so, they must *request* permission. In some cases, simply making the request is enough to satisfy the terms of the agreement. But, as we'll see in the next duty, sometimes it's only the beginning of the process.

Audit Example: Exchange X would like to perform an audit of an investement bank's internal data use and distribution. They are contractually entitled to so periodically, but they must first inform that bank of the impending audit by making a *request*.

Read more: [Notification, Request, and Consent Duties](https://github.com/w3c/market-data-odrl-profile/issues/6)

## Duty: Consent

**Definition: The debtor accedes to a desired state of the world (defined by the action scope).**

Now, the Debtor is the party responding to the request made previously. They are the Debtor because the action is on them to accede to the request. They may or may not be contractually obligated to fulfil the request, but they are the Debtor in the sense that they have the next action.

### Action Scopes

**Service Facilitator:** The debtor consents to the creditor's use of a service facilitator.

**Audit:** The debtor consents to be audited by the creditor.

Service Facilitator Example: A user of Exchange X data has previously requested that they be allowed to use a Service Facilitator in a certain scenario. Before they can do so, Exchange X must give their *consent*  that the request has been granted.

Audit Example: The investment bank contacted by Exchange X accedes to be audited.

Read more: [Notification, Request, and Consent Duties](https://github.com/w3c/market-data-odrl-profile/issues/6)

## Duty: Notify

**Definition: The Debtor makes the Creditor aware of a relevant change in the state of the world (defined by the action scope).**

Often, the Debtor is a Redistributor or Consumer of data, *notifying* the Originator that they've begun using a particular data product or that they've begun distributing data to a new third party.

### Action Scopes

**Usage:** The debtor makes the creditor aware that they are using the asset.

Example: Vendor Y is required to tell Exchange X before distributing uncontrolled data to a new end user. There are no additional obligations (e.g. no need to wait or approval) but they must inform the exchange before entitling their new client.

Read more: [Notification, Request, and Consent Duties](https://github.com/w3c/market-data-odrl-profile/issues/6)

## Duty: Report

**Definition: The Debtor provides a report to the Creditor on a relevant state of the world (defined by the action scope).**

In most, if not all, cases, the Debtor is a Redistributor or Consumer of data, peridically updating the Originator on something happening in their jurisdiction with regards to a data set. The big difference between the notification duty modeled above and standard reporting duties is their periodicity: while notification only need happen once, reporting must be repeated.

### Action Scopes

**Controls:** The debtor reports on their implementation of access controls.

**Usage:** The debtor reports on their usage of the asset as specified in the duty.

Usage Example: Vendor Y must send Exchange X a *report* each month listing products delivered to devices under Vendor Y's entitlement control, used by professional subscribers, summarized at the location level. The action for this example has an action scope of Usage, with a unitOfCount of Device. Since the report is required monthly, the duty has a timeInterval of monthly, and the action specifies that it must be done once per month.

Read more: [Reporting Duties](https://github.com/w3c/market-data-odrl-profile/issues/7)

## Duty: Invoice

**Definition: The Debtor bills the Creditor.**

Counterintuitively, the Debtor in this case is the party required to create an invoice (Of course, they are only *required* to make an invoice if they want to get paid.)

Example: Exchange X has processed Vendor Y's monthly report and uses the information therein to generate an *invoice* for Vendor Y. In the case of a direct bill exchange, the duty to create an invoice would be de-coupled from the duty to report, with the invoice generated by the exchange sent directly to the data consumer.

Read more: [Payment Duties](https://github.com/w3c/market-data-odrl-profile/issues/8)

## Duty: Compensate

**Definition: The Debtor pays the Creditor.**

The Debtor is the party required to compensate the Creditor. Most often, this would be a Redistributor or Consumer of data paying the Originator. This duty may or may not have been triggered by the issuing of an invoice.

Example: Exchange X has an online webstore where data consumers can browse and purchase historical data. If the data is less than a certain amount, the purchaser is required to enter their credit card at the point of sale to make a payment to *compensate* Exchange X for access to the data.

Read more: [Payment Duties](https://github.com/w3c/market-data-odrl-profile/issues/8)

## Duty: Attribute

**Definition: The Debtor publishes a description of the Creditor's relation to the asset.**

Attributions usually attribute ownership, but we'll use the duty to also cover the disclaimers required on derived data. The action scope makes the distinction between Ownership and Disclaimer.

Example: An online news site has a widget on their website that displays a selection of ticker prices after a certain delay period. Exchange X requires that the website *attribute* ownership of the information to them.

Read more: [Attribution Duties](https://github.com/w3c/market-data-odrl-profile/issues/9)

## Time to Vote!

Are the definitions for these terms correct?

Are there other terms needed to fully define duties related to market data contracts?

[Vote](https://w3c.github.io/market-data-odrl-profile/Vote)

## New Topics

[Temporal Aspects of Policy Management](https://github.com/w3c/market-data-odrl-profile/issues/12)
[Policy Types & Lifecycle](https://github.com/w3c/market-data-odrl-profile/issues/13)