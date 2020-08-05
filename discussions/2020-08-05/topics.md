# August 5th, 2020: Topics for Discussion

Agenda: 

* Finalize definitions of Notify and Report
* Begin discussion of Temporal Aspects of Policy Lifecycle

## Duties: Notify and Report

**Notify:** The debtor makes the creditor aware of a relevant change in the state of the world (defined by the action scope) usually on a one-off basis.

**Report:** The debtor provides a report to the creditor on a relevant state of the world (defined by the action scope) usually on a regular basis.

*"Usually on a one-off basis:" Is frequency the right differentiator between these Notify and Report?*

Possibilitites:

* Scheduled (Report) vs. Unscheduled (Notify)
* Structured (Report) vs. Unstructured (Notify)
* Has Unit of Count (Report) vs. No Unit of Count (Notify)
* "Multi-line" (Report) vs. "Single-Line" (Notify)
* Others?

## Time to Vote?

Did we agree on how to define Notify and Report? If so, let's make it official.

[Vote](https://w3c.github.io/market-data-odrl-profile/Vote)


## Temporal Aspects of Policy Lifecycle

In the real world, the terms that govern a particular asset may change over time, sometimes as specified by a new contract, other times as specified in policy documents *referred* to by a contract.

Read more: [Temporal aspects issue thread](https://github.com/w3c/market-data-odrl-profile/issues/14)

### Is it important to support temporal aspects in our standard? If so, why?

* **Support audits:** The model must support an account of history that both the data Provider and the data Consumer can agree upon through the audit process.

* **Ensure compliance as policies update:** The model must continue to support provably-correct compliance decisions in the present as policies change and update over time.

* **Enable forecasting:** The model must support an account of the future so actors in the supply chain can predict their capabilities and costs as and when updates are published.

Questions for discussion:

1. Any other reasons to support time-based changes?
1. Can we imagine a digital rights specification that *doesn't* support time-based changes? Would it still be at all useful?

### What kinds of things can change over time? Some examples:

1. A change in a pricing Duty - price goes up
1. A change in a reporting Duty - from User ID to Device ID
1. A change in the composition of an Asset - greater book depth
1. A change in the definition of an Action - broadening the action scope to allow derivations for pricing options as well as warrants
1. A change in the definition of a Permission - removing the condition that the consumer's access control system be deployed by a vendor
1. A change in the definition of a Permission - adding a new asset
