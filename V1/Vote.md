# To Vote On

## Actions for Duties
**md:Notify**

_Sub-class of odrl:Action_

The debtor makes the creditor aware of a relevant change in the state of the world (defined by the action scope).

Where the action scope is **md:Usage**, the debtor makes the creditor aware that they are using the asset.

<br>**md:Request**

_Sub-class of odrl:Action_

The debtor makes the creditor aware of a desired state of the world (defined by the action scope).

Where the action scope is **md:Audit**, the debtor requests the creditor to accede to an audit.

Where the action scope is **md:ServiceFacilitator**, the debtor requests the creditor allow a service facilitator to access the asset.

<br>**md:Report**

_Sub-class of odrl:Action_

The debtor provides a report to the creditor on a relevant state of the world (defined by the action scope).

Where the action scope is **md:ResonableSuspicion**, the debtor reports a reasonable suspicion that the asset is being misused.

Where the action scope is **md:Controls**, the debtor reports on their implementation of access controls.

Where the action scope is **md:Usage**, the debtor reports on their usage of the asset as specified in the duty.

<br>**md:Consent**

_Sub-class of odrl:Action_

The debtor accedes to a desired state of the world (defined by the action scope).

Where the action scope is **md:Audit**, the debtor consents to be audited by the creditor.

Where the action scope is **md:ServiceFacilitator**, the debtor consents to the creditor's use of a service facilitator.

<br>**md:Compensate**

_Sub-class of odrl:Action_

The debtor pays the creditor.

<br>**md:Invoice**

_Sub-class of odrl:Action_

The debtor bills the creditor.

<br>**md:Attribute**

_Sub-class of odrl:Action_

The debtor publishes a description of the creditor's relation to the asset.

Where the action scope is **md:Ownership**, the attribution describes the creditor's ownership of the asset identified by the odrl:target relation.

Where the action scope is **md:Disclaimer**, the attribution clarifies the creditor's relation to the asset identified by the odrl:target relation.

<br>

## Action Scope for Duty Actions
**md:Usage**

_Sub-class of md:ActionScope_

Qualifies actions taken in the context of the assignee's usage of the asset.

<br>**md:ServiceFacilitator**

_Sub-class of md:ActionScope_

Qualifies actions taken in the context of the assignee employing a service facilitator.

<br>**md:Ownership**

_Sub-class of md:ActionScope_

Qualifies actions taken in the context of the assigner's ownership of the asset.

<br>**md:Disclaimer**

_Sub-class of md:ActionScope_

Qualifies actions taken in the context of the assigner's clarification of their relation to the asset. 

<br>**md:Audit**

_Sub-class of md:ActionScope_

Qualifies actions taken in the context of a proposed audit of the assignee by the assigner.

<br>**md:ReasonableSuspicion**

_Sub-class of md:ActionScope_

Qualifies actions taken in the context of a reasonable suspicion that the assignee is misusing the asset.

<br>

## Constraints: predicates that test the state of the world
**md:recipient**

_Domain: odrl:Rule_  

_Range: odrl:Party_

A party with access to the asset

Frequently used to indicate whether the party is internal or external (i.e. a third party) to the assignee

Can be qualified by the role constraint.

<br>**md:role**

_Domain: odrl:Party_

_Range: md:Role_

The role a party plays in respect of the asset.

Parties can play multiple roles.

<br>

## Simple Properties that specify an entity

**md:unitOfCount**

_Domain: odrl:Action_

_Range: md:UnitOfCount_

The thing to be counted.

Often used to specify the things to be counted (e.g. devices or access IDs) in a usage report or in calculating a payment.

Examples of Unit of Count:
* User ID
* Device
* Person
* Location
* Site
* Client Organisation
