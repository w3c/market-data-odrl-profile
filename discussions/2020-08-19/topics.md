# August 19th, 2020: Topics for Discussion

Agenda: 

* Finalize definitions of Notify and Report
* New Terms for "Creditor" and "Debtor"
* Changes Over Time: Static or Dynamic Identifiers? 
* Properties of Resources

## Duties: Notify and Report

### Editor's Recomendation 

These definitions of Notify and Report draw their distinction between the notification of an *event* and the reporting of a *state of affairs*:

**Notify:** The debtor makes the creditor aware of a relevant event (defined by the action scope).

**Report:** The debtor provides a report to the creditor on a relevant and on-going state of affairs (defined by the action scope).

### Other attempts

*Previous suggestion*:

**Notify**: The debtor makes the creditor aware of a relevant change in the state of the world (defined by the action scope).

**Report**: The debtor provides a report to the creditor on a relevant state of the world (defined by the action scope).

*Frequency*:

**Notify**: The debtor makes the creditor aware of a relevant change in the state of the world, usually done once. (defined by the action scope).

**Report**: The debtor provides a report to the creditor on a relevant state of the world, often on a regularly defined schedule. (defined by the action scope).

*Structure*:

**Notify**: The debtor makes the creditor aware of a relevant change in the state of the world, usually in an unstructured manner. (defined by the action scope).

**Report**: The debtor provides a report to the creditor on a relevant state of the world, usually in a format defined by the creditor. (defined by the action scope).

*Unit of Count*:

**Notify**: The debtor makes the creditor aware of a relevant change in the state of the world, usually with no specified unit of count. (defined by the action scope).

**Report**: The debtor provides a report to the creditor on a relevant state of the world, usually by counting items of a partular unit. (defined by the action scope).

*Sender/Receiver*:

**Notify**: The debtor (most often the provider) makes the creditor aware of a relevant change in the state of the world. (defined by the action scope).

**Report**: The debtor (most often the consumer) provides a report to the creditor on a relevant state of the world. (defined by the action scope).

## New Terms for "Creditor and "Debtor"

A Duty has two related parties: The party requiring the Duty and the party responsible for permforming the Duty. We've been calling these parties the Creditor and the Debtor, but would like to find a clearer pair of terms. Some suggestions:

| Creditor | Debtor |
|---|---|
| Actor  | Target  |
| Giver  | Receiver |
| Subject  | Object  | 
| Obligatee | Obligator  |
| Licensor | Licensee  |
| Requiring Party  | Responsible Party  |

[Read more on the Issue thread.](https://github.com/w3c/market-data-odrl-profile/issues/17)

## Changes Over Time: Static or Dynamic Identifiers?  

Last session, we agreed that contracts and agreements for the data industry do need some form of temporal support. Polices and prices change, and one contract or document needs to be able to reference both the time before and the time after a change.

ODRL is largely a language of objects. So, should we support time-based changes by requiring a second object be defined with the properties of a new time period, or should we create a "wrapper" layer that will allow systems to refer to the same object and then "drill down" to find out what its properties were at a particular time?

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


### Wrapper approach:

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

    :Pt1    rdf:type                    md:TemporalPermission ;
            md:version                  :P1 , :P2 .

The "wrapper approach" simply adds a layer on top of the definitions whose sole purpose is to give systems a single, unchanging, identifier. 

Are there any arguments against using a wrapper layer?

1. It addes some complexity
2. It's not part of the original ODRL spec

It seems like a wrapper layer has value, are the above arguments enough to recommend against it?

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

Are there other terms useful in describing Resources in our industry?

See [the New Terms page](https://github.com/w3c/market-data-odrl-profile/blob/gh-pages/NewTerms.md) for more detail.

### Time to Vote

[New Terms to Vote On](https://github.com/w3c/market-data-odrl-profile/blob/gh-pages/NewTerms.md#to-vote)

* Definitions for Notify and Report
* Replacement terms for Creditor and Debtor
* Static or Dynamic References for Time-based Objects

