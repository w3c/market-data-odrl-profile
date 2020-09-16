# September 2nd, 2020: Topics for Discussion

Agenda: 

* VOTE on replacement terms for Creditor and Debtor
* VOTE on Temporal Aspects: do we need temporal objects?
* VOTE - Properties of Resources
* To Discus - Policy Lifecycle Descriptors

## Replacement Terms for Creditor and Debtor

A Duty has two related parties: The party requiring the Duty and the party responsible for permforming the Duty. We've been calling these parties the Creditor and the Debtor, but would like to find a clearer pair of terms. 

Two terms emerged as the favorites last session:

| Debtor | Creditor |
|---|---|
| Subject  | Object  | 
| Obligatee | Obligator  |

Here's how they'd be used in some example phrases:

### Subject/Object

*Invoice:* The Subject bills the Object.

*Request:* The Subject makes the Object aware of a desired state of the world (defined by the action scope).

*Compensate:* The Subject pays the Object.

### Obligatee/Obligator

*Request:* The Obligatee makes the Obligator aware of a desired state of the world (defined by the action scope).

*Invoice:* The Obligatee bills the Obligator.

*Compensate:* The Obligatee pays the Obligator.

[Read more on the Issue thread.](https://github.com/w3c/market-data-odrl-profile/issues/17)

## Temporal Aspects: do we need temporal objects?

Examples of the non-temporal approach and temporal approach to objects below. Should we support temporal objects in our language implementation?

### New object approach:

    :A1     rdf:type                    odrl:Asset ;
            md:effectiveDate            [   a             time:ProperInterval ;
                                            time:after    "2019-01-01T00:00:00Z"^^xsd:dateTime
                                            time:before   "2021-01-01T00:00:00Z"^^xsd:dateTime
                                        ] ;
            md:resource                 :S1 ;
            md:timelinessOfDelivery     ...
            md:depthOfMarket            [  a                    md:Level2 ;
                                        md:positionFrom      1 ;
                                        md:positionTo        10 ;
                                        ] ;
            md:contentNature            ...


    :A2     rdf:type                    odrl:Asset ;
            md:effectiveDate            [   a             time:ProperInterval ;
                                            time:after    "2021-01-01T00:00:00Z"^^xsd:dateTime 
                                        ] ;
            md:resource                 :S1 ;
            md:timelinessOfDelivery     ...
            md:depthOfMarket            [  a                    md:Level2 ;
                                        md:positionFrom      1 ;
                                        md:positionTo        12 ;
                                        ] ;
            md:contentNature            ...


### Temporal Object approach:

    :A1     rdf:type                    odrl:Asset ;
            md:effectiveDate            [   a             time:ProperInterval ;
                                            time:after    "2019-01-01T00:00:00Z"^^xsd:dateTime
                                            time:before   "2021-01-01T00:00:00Z"^^xsd:dateTime
                                        ] ;
            md:resource                 :S1 ;
            md:timelinessOfDelivery     ...
            md:depthOfMarket            [  a                    md:Level2 ;
                                        md:positionFrom      1 ;
                                        md:positionTo        10 ;
                                        ] ;
            md:contentNature            ...


    :A2     rdf:type                    odrl:Asset ;
            md:effectiveDate            [   a             time:ProperInterval ;
                                            time:after    "2021-01-01T00:00:00Z"^^xsd:dateTime
                                        ] ;
            md:resource                 :S1 ;
            md:timelinessOfDelivery     ...
            md:depthOfMarket            [  a                    md:Level2 ;
                                        md:positionFrom      1 ;
                                        md:positionTo        12 ;
                                        ] ;
            md:contentNature            ...

    :At1    rdf:type                    md:TemporalAsset ;
            md:version                  :A1 , :A2 .

[Read more on the Issue thread.](https://github.com/w3c/market-data-odrl-profile/issues/14)

## Properties of Resources

An Asset is a Resource, a collection of Resources, or the part of a Resource controlled by a Rule. "Resource" is, intentionally, a very generic term. Assets are further defined by assigning them attributes and defining values for the assigned attributes.

What attributes are needed to fully describe Assets produced and licensed in our industry?

| Property | Definition | Possible Values |
|---|---|---|
| Provider  | Points to the Party playing the role of Provider in relation to the Resource. |  |
| Resource  | Points to the original Resource(s) that the subject Resource or Asset qualifies. |  |
| Asset Class  | Categorises resources by the financial asset class they describe |  |
| Content Type  | Given the asset class, further specifies the type of content provided by the resource |  |
| Intraday  | Indicates whether the resource changes intraday or not. |  |
| Timeliness of Delivery | Specifies the timing of the permitted receipt, use, or onwards delivery of a resource. | Real-Time, Delayed, etd. |
| Method of Update | Specifies the method by which updates to the Resource are delivered | Snapshot, Streaming, Time Series |
| Update Period | The period during which the Resource has been, or continues to be, updated |
| Frequency of Update | Specifies how frequently updates to the Resource are delivered |  |
| Complex ID | Provides a universal identifier by specifying a local identifier and it's context. |  |
| Depth of Market | Indicates the amount of book information in a market data product | Level 1, Level 2, etc. |
| Geography | The geographic subject matter and focus of the content. |  |
| Amount | The amount of a resource. |  | 

See [the New Terms page](https://github.com/w3c/market-data-odrl-profile/blob/gh-pages/NewTerms.md) for more detail.

## Policy Lifecycle Descriptors

When managing policies through their life-cycle, we might also want to give them a status. 

* *Draft:* Work in progress or for review or approval.
* *Cancelled:* Abandoned, never published.
* *Published:* Live, operative (subject to effective dates), available for new users.
* *Obsolete:* Operative (subject to effective dates) for existing use/users, not available for new use/users.
* *EOL:* End Of Life, removed, no longer valid, unusable.

[Read more on the Issue thread.](https://github.com/w3c/market-data-odrl-profile/issues/13)