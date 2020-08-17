# To Discuss

## Properties of Resources
The list of properties below leans heavily on the work done by Phil Rimell on the Revelation Business Information Model. 

**md:provider** | -    
----------------|------------
Definition | Points to the Party playing the role of Provider in relation to the Resource.  
Label | is provided by  
Domain | Resource  
Range | Party  

***Example:** The Resource :R1 is provided by the CME*
```turtle
:R1    a              md:Resource .
:R1    md:provider    <https://permid.org/1-4295899615> . # CME
```

<br><br>

**md:resource** | -    
----------------|------------  
Definition | Points to the original Resource(s) that the subject Resource or Asset qualifies.  
Editorial Note | New resources can be created by constraining and/or aggregating other resources.  
Label | has resource  
Domain | Resource  
Range | Resource  

***Example:** The Resource :R2 is Delayed version of the Resource :R1*
```turtle
:R2    a                        md:Resource .
:R2    md:resource              :R1 .
:R2    md:timelinessOfDelivery  md:Delayed .
```

<br><br>

**md:assetClass** | -    
----------------|------------
Definition | Categorises resources by the financial asset class they describe  
Label | describes the asset class  
Domain | Resource  
Range | Asset Class  

But what should we use as our controlled list of asset classes? ISO 10962 (aka CFI codes): https://en.wikipedia.org/wiki/ISO_10962?

***Example:** The Resource :R1 describes Commodity Futures*
```turtle
:R1    md:assetClass    <https://sec.report/CFI/FCEPSX> . # Commodity Futures for Extraction Resources with Physical Delivery
```
<br><br>

**md:contentType** | -    
----------------|------------  
Definition | Given the asset class, further specifies the type of content provided by the resource  
Example | Data describing indices can be segmented by index value, constituent data, weightings data, and divisors.  
Label | has content type  
Domain | Asset Class  
Range | Content Type  

Again, what should we use as our controlled list of content types?

***Example:** The Resource :R3 descibes the Values and Constituents of an Index of Equities*
```turtle
:R3    a                md:Resource .
:R3    md:assetClass    [   a                <https://sec.report/CFI/TIEXX> . # Index of equities
                            md:contentType   (md:Value md:Constituents)
                        ] .
```

<br><br>

**md:intraday** | -    
----------------|------------  
Definition | Indicates whether the resource changes intraday or not.  
Label | is intraday  
Domain | Resource  
Range | Boolean  

***Example:** The Resource :R3 does not change intraday*
```turtle
:R3    md:intraday    false .
```

<br><br>

**md:timelinessOfDelivery** | -    
----------------|------------  
Definition | Specifies the timing of the permitted receipt, use, or onwards delivery of a resource.  
Editorial Note | Usually specified as an interval (or intervals) relative to the data's origination, publication, issue, or release (or some other specified event).  
Editorial Note | Unless explicitly prohibited, permissions over shorter intervals carry across to longer intervals (e.g. real-time data also covers delayed, embargoed, and historic data)  
Label | is delivered as  
Domain | Resource  
Range | Proper Interval  

***Example:** The Resource :R1 is realtime*
```turtle
:R1    md:timelinessOfDelivery    md:Realtime .
```

We can also specify the precise meaning of realtime defined in a license.

***Example:** Realtime is data delivered within 10 minutes of Time-of-Issue*
```turtle
:R1    md:timelinessOfDelivery [    a                   time:ProperInterval , md:Realtime ;
                                    time:intervalBefore [   a                    time:ProperInterval ;
                                                            md:timeReference     [   a   time:Instant , md:TimeOfIssue ] ;
                                                            time:hasXSDDuration  "PT10M"^^xsd:duration
                                                        ]
                                ] .
```

We can do the same for delayed:

***Example:** Delayed data is defined as being between ten minutes and eight hours of Time-of-Issue*
```turtle
:R2    md:timelinessOfDelivery [    a                   time:ProperInterval , md:Delayed ;
                                    time:intervalAfter  [    a                   time:ProperInterval ;
                                                             md:timeReference    [   a   time:Instant , md:TimeOfIssue ] ;
                                                             time:hasXSDDuration "PT10M"^^xsd:duration
                                                             
                                                        ] ;
                                    time:intervalBefore [     a                  time:ProperInterval ;
                                                            md:timeReference     [   a   time:Instant , md:TimeOfIssue ] ;
                                                            time:hasXSDDuration  "PT8H"^^xsd:duration
                                                        ]
                                ] .
```                                

And for historic:

***Example:** Historic data is defined as being after eight hours of Time-of-Issue*
```turtle
:R4    md:timelinessOfDelivery [   a                   time:ProperInterval , md:Historical ;
                                    time:intervalAfter  [     a                  time:ProperInterval ;
                                                            md:timeReference     [   a   time:Instant , md:TimeOfIssue ] ;
                                                            time:hasXSDDuration  "PT8H"^^xsd:duration
                                                        ]
                                ] .
```   

End-of-day data can be specified in a similar manner:

***Example:** End-of-Day data is defined as data embargoed until market close at 4pm CST*
```turtle
:R3    md:timelinessOfDelivery [   a                   time:ProperInterval , md:Embargo ;
                                   time:after          [   a                   time:Instant, md:MarketClose ;
                                                            time:inDateTime     [   a               time::DateTimeDescription ; # Monday to Friday?
                                                                                    time:hour       "16"^^xsd:int ;
                                                                                    time:timeZone   <https://www.wikidata.org/wiki/Q2086913>
                                                                                ]
                                                        ]
                                ] .
```
 
Time of Origination, Publication, Issue, and Release can be defined as time instants  

<br><br>

**md:methodOfUpdate** | -    
----------------|------------  
Definition | Specifies the method by which updates to the Resource are delivered  
Label | is updated by  
Domain | Resource  
Range | Update Method  

The possible values are:
* Snapshot: A single response to a request. An update is provided only in response to a request (like an API call) and not further updated. Also known as “one-shot”.
* Streaming: All changes are captured and continuously transmitted either individually or in batches.
* Time Series: Multiple updates are delivered together in bulk 

<br><br>

**md:updatePeriod** | -    
----------------|------------  
Definition | The period during which the Resource continues to be updated  
Label | is updated during  
Domain | Resource  
Range | Interval  

Service Period can be defined as a time interval  

<br><br>

**md:frequencyOfUpdate** | -    
----------------|------------  
Definition | Specifies how frequently updates to the Resource are delivered  
Label | has frequency of update  
Domain | Resource  
Range | Update Frequency  

The possible values are:
* Tick-by-tick
* Sampled

<br><br>

**md:complexID** | -    
----------------|------------  
Definition | Provides a universal identifier by specifying a local identifier and it's context.  
Editorial Note | For identifying market data Sources, the context is usually provided by the venue  
Label | has complex ID  
Domain | Resource  
Range | Complex ID  

<br><br>

**md:depthOfMarket** | -    
----------------|------------  
Definition |    
Label | provided by  
Domain | Resource  
Range | Party  

The possible values are:
* Level 1
* Level 2
* Level 3

Each of which can be qualified by md:positionFrom and md:positionTo

<br><br>

**md:geography** | -    
----------------|------------   
Definition | The geographic subject matter and focus of the content.  
Scope Note | A characteristic of the content rather than its source/origin or any limitations on its distribution.  
Label | has geographic coverage  
Domain | Resource  
Range | ISO 3166 country codes and UN Regions and Sub-Regions? Do we need geopolitical entities like the EU, MERCOSUR, or APEC?

(inc. exclusions)

<br><br>

**md:amount** | -    
----------------|------------     
Definition | The amount, or fraction, of a Resource.  
Label | has amount  
Domain | Resource  
Range | Amount  

Possible value:
* Insubstantial

<br><br>

## Policy Status: policy lifecycle descriptors
To manage policies through their life-cycle, we need to track their status:

<br>**md:Draft**

Work in progress or for review or approval.

<br>**md:Cancelled**

Abandoned, never published.

<br>**md:Published**

Live, operative (subject to effective dates), available for new users.

<br>**md:Obsolete**

Operative (subject to effective dates) for existing use/users, not available for new use/users.

<br>**md:EOL**

End Of Life, removed, no longer valid, unusable.

<br>

# To Vote
## Actions for Duties
**md:Notify**

_Sub-class of odrl:Action_

The debtor makes the creditor aware of a relevant change in the state of the world (defined by the action scope) usually on a one-off basis.

Where the action scope is **md:Usage**, the debtor makes the creditor aware that they are using the asset.

<br>**md:Report**

_Sub-class of odrl:Action_

The debtor provides a report to the creditor on a relevant state of the world (defined by the action scope) usually on a regular basis.

The periodicity of reporting is defined by the `time interval` property.

Where the action scope is **md:ResonableSuspicion**, the debtor reports a reasonable suspicion that the asset is being misused.

Where the action scope is **md:Controls**, the debtor reports on their implementation of access controls.

Where the action scope is **md:Usage**, the debtor reports on their usage of the asset as specified in the duty.

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
<br>

# Agreed

## Actions for Duties

<br>**md:Request**

_Sub-class of odrl:Action_

The debtor makes the creditor aware of a desired state of the world (defined by the action scope).

Where the action scope is **md:Audit**, the debtor requests the creditor to accede to an audit.

Where the action scope is **md:ServiceFacilitator**, the debtor requests the creditor allow a service facilitator to access the asset.

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

## Roles in the Data Supply Chain
**md:Originator**

_Sub-class of md:Role_

A party that generates/owns a resource and acts as an assigner of the rights and obligations controlling the use of that resource by third-parties. 

<br>**md:Provider**

_Sub-class of md:Role_

A party that distributes a resource to a consumer and acts as an assigner of the rights and obligations controlling the use of that resource by third-parties

<br>**md:Consumer** 

_Sub-class of md:Role_

A party that receives a resource and acts as an assignee of the rights and obligations controlling the use of that resource.

<br>**md:Service Facilitator** 

_Sub-class of md:Role_

An external organisation contracted by a Party (or its affiliated companies) to assist in the delivery of data services.

<br>**md:Administrator**

_Sub-class of md:Role_

An external organisation contracted by a Party (or its affiliated companies) to assist in the assignment of rights.

<br>

## Sources, Resources, & Assets
**md:Resource**

A Resource is some commodity (e.g. API calls, bandwidth, data) access to which (or to some part of which) may be controlled by a Rule.

Example: In the context of market data, a Resource could be the all the pricing and trading data generated by the trade in one or more financial instruments on an exchange, or indices derived from that data.

Editorial Note: Resources are sensitive to their means of delivery and informational completeness. A real-time version of that data may be a different Resource than the delayed. Book depth too can distinguish between Resources.

Editorial Note: A Resource can be transformed through some calculation but still remain the same Resource. It only becomes a new Resource if the transformation is irreversible (i.e. the original data cannot be recovered) and non-substitutive (i.e. the altered data cannot be used in place of the original).

Example: The operation of currency conversion does not change the identity of a Resource

Example: Augmenting a Resource with additional symbology does not change the identity of that Resource

Example: Co-mingling Resources does not change the identities of the combined Resources

Example: Normalising a Resource does not change the identity of that Resource

<br>**md:Asset**

_Sub-class of md:Resource_

An Asset is a Resource, a collection of Resources, or the part of a Resource controlled by a Rule. (A Rule being a Permission, a Prohibition, or a Duty).

<br>**md:Source**

A Source is a root Resource: unconstrained and informationally complete, independent of the aspects of commercialisation and/or delivery including timeliness, method of delivery, or book depth.

<br>
<br>

# To Do
"*What do we all* [the exchanges] *really care about? It's simple: distribution, non-display uses such as automated trading, and the creation of new financial products*"

## AGENTS



### Broker
**Description:** Acting on behalf of another person’s name and for another person’s account or acting in one’s own name and for another person’s account i.e. trading to execute orders on behalf of clients.

**Scope Note:** DBAG - Smart order routing is considered to facilitate customer business

### Principle
**Description:** Undertakes activities for their own purposes i.e. acting in one’s own name or for one’s own account - not on someone else's account (like that of a client)

**Example:** Proprietary trading, Trading firms

**Scope Note:** DBAG - Market making is considered to be trading as principal

### Trading Platform
**Description:** A venue on which buy and sell orders from multiple parties are matched

**Scope Note:** Broker crossing networks and dark pools are examples of alternative trading systems (ATS), and are thus trading platforms.

**Scope Note:** Includes alternative trading systems (ATS) as defined by *300a of the SEC regulation on ATS*: any organization, association, person, group of persons, or system that constitutes, maintains, or provides a market place or facilities for bringing together purchasers and sellers of securities or for otherwise performing with respect to securities the functions commonly performed by a stock exchange.

**Scope Note:** Includes multilateral trading facilities (MTF) as defined in *MIFD II*: multilateral systems, operated by an investment firm or a market operator, which bring together multiple third-party buying and selling interests in financial instruments (in the system and in accordance with non- discretionary rules) in a way that results in a contract.

**Scope Note:** Includes organised trading facilities (OTF) as defined in *MIFD II*: multilateral systems which are not a regulated market or an MTF and in which multiple third-party buying and selling interests in bonds, structured finance products, emission allowances, or derivatives are able to interact in the system in a way that results in a contract.

**Scope Note:** Includes systematic internalization as defined in *MIFD II*: dealing on an organised, frequent, systematic, and substantial basis on one's own account when executing client orders outside a regulated market, an MTF, or an OTF, without operating a multilateral system.



## Actions

### Distribute
**Description:** The onward dissemination of a Resource or any of its parts to a third-party.

### Display
**Description:** The display of data to a person or persons

###  Non-Display Use
**Description:** Usage when the scope and scale of usage is beyond that which could be reasonably expected of a person

**Editorial Note:** CME - Non-viewable use of Information in any system, process, program, machine or calculation other than in order to display or distribute Information for display. Such use may include, but is not limited to, calculation of P&L, portfolio valuation, order processing, use within Automated Trading Systems and automated order routing.

**Editorial Note:** DBAG - Non-Display Information Usage is accessing, processing or consumption of Real-Time Information for purposes other than the support of its display, onward dissemination to third parties or CFD Information-Usage.

**Example:** Automated valuations

**Example:** Calculating risk figures

**Example:** Portfolio valuation

**Example:** Profit and loss calculations

###  Benchmark
**Editorial Note:** The act of benchmarking as defined by the *EU Benchmark Regulation* is where an Index is used to determine the amount payable under a financial instrument or financial contract, or the value of a financial instrument, or is used to measure the performance of an investment fund for the purpose of tracking the return, defining the asset allocation or a portfolio, or computing the performance fees.

###  TradeAutomatically
**Editorial Note:** CME - Non-Display Use of Information by a Licensee Group entity in Automated Trading Systems."@en ,

**Editorial Note:** DBAG - Trading based activities’ include, but are not limited to, semi-automated or automated order/quote generation, order pegging, price referencing for trading purposes, smart order routing to facilitate trading, order management, execution management, market making, ‘black box’ trading, algorithmic trading, program trading and operation of multilateral trading facilities as well as quoting and trading of financial derivatives (including but not limited to futures, options, warrants and certificates linked to the respective underlying market data).

**Example:** Semi-automated or automated order/quote generation

**Example:** Algorithmic or program trading 

**Example:** Black-box trading

**Example:** Order Pegging

**Example:** Price referencing for trading purposes

**Example:** Systematic internalization *[Article 4(1)(20) of MiFID II]*

**Example:** Mid-point trading

**Example:** Smart order routing to facilitate trading

**Example:** Market making

**Example:** Execution Management

**Example:** Quoting and trading of financial derivatives

###  Derive
**Description:** To create a new derivative Resource from an Asset

**Editorial Note:** Derivations are frequently generated for the purposes of risk management, profit and loss calculation, portfolio valuation, quantitative analysis, fund administration, fund accounting, portfolio management or instrument pricing.

**Note:** The output of the derivation can be controlled by using a duty to impose a "next policy" action that points to a new policy that controls the use of the derived resource .


###  CalculateIndex
**Editorial Note:** An index as defined by the *EU Benchmark Regulation* means any figure that is regularly determined either by applying a formula or other calculation or making an assessment on the basis of the value of one or more underlying assets/prices (including estimated prices, actual or estimated interest rates, quotes and committed quotes, or other values or surveys).

###  Price
                                                 
# Hierarchy

    Distribute

    Use

      Display

      Non-Display Use

        Trade Automatically

        Benchmark

        Derive

          Calculate Index

          Price
