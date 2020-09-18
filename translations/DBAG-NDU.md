# Translation Two: DBAG Non-Display Agreement

```diff
- The interpretation presented below is a work in progress. 
- It is presented solely as an exploration of automated rights management and is intended to provoke debate.
```

`Code` uses the turtle syntax defined here: <https://www.w3.org/TR/turtle/>. Hopefully though you can usefully read the document without reading the code.

The semantics of the ODRL terms are defined here: <https://www.w3.org/TR/odrl-model/> and here: <https://www.w3.org/TR/odrl-vocab/>

## Contents
1. [License](#license)
   * [License Documentation](#license-documentation)
2. [Actions](#actions)
   * [Allowed Actions](#allowed-actions)
   * [Disallowed Actions](#disallowed-actions)
3. [Assets](#assets)
   * [Resources](#resources)
   * [Timeliness of Delivery](#timeliness-of-delivery)
4. [Policies and Permissions I](#policies-and-permissions-i)
5. [General Obligations](#general-obligations)
   * [Audits](#audits)
   * [Controls](#controls)
   * [Notification](#notification)
   * [Service Facilitators](#service-facilitators)
6. [Policy Update I](#policy-update-i)
7. [Specific Duties](#specific-duties)
   * [Attribute](#attribute)
   * [Report](#report)
   * [Pay](#pay)
8. [Policy Update II](#policy-update-ii)
9. [Permissions Update](#permissions-update)

## License
The DBAG Non-Display Agreement.

### License Documentation
We need several documents from DBAG to understand this license:
* Probably the best place to start is the guidance note to clients on non-display usage: <https://www.mds.deutsche-boerse.com/resource/blob/1334848/d0f90031dcf62a50d8d31812304c9392/data/Guidance-Note-for-customers.pdf>
* The general terms for non-display usage: <https://www.mds.deutsche-boerse.com/resource/blob/1637380/d77459a7f1492c6f06808a8949b19a3f/data/NonDisplay_GTC_3_5.pdf>
* The fee schedule: <https://www.mds.deutsche-boerse.com/resource/blob/1334780/60ddf0a87283cdc57ec8ab9ae88ca4cc/data/NonDisplay_Price_List_5_11.pdf>
* The Market Data Dissemination Agreement and its various annexes (including the Audit guidelines) are available from here (as are the two documents above): <https://www.mds.deutsche-boerse.com/mds-en/data-services/real-time-market-data/agreements>

## Actions

### Allowed Actions

The DBAG Non-dispay use license is wide-ranging. It covers **automated trading**; **index calcualtions**; and other **non-display** uses.

What is non-display use? Historically, it was introduced when data started being routed to machines to act on, rather than people. There's a limit to how much data a human can process. This is not so for a machine. So non-display use was split out and priced accordingly.

Now machine use has proliferated, with some uses being more high-value than others. Non-display use tries to make sense of this.

So we have lots of different actions available at different prices. We best read the [guidance note](https://www.mds.deutsche-boerse.com/resource/blob/1334848/d0f90031dcf62a50d8d31812304c9392/data/Guidance-Note-for-customers.pdf), so:

The first one is automated trading. So, at it's simplest, we have a permission that offers automated trading:

>```
>:P1    rdf:type        odrl:Permission .
>:P1    odrl:action     md:TradeAutomatically .
>```

But this permission comes in several versions (and price points) depending on whether it is exercised by a trading **platform**, a **principle** (trading on their own account), a **broker**, or a principle using a **managed environment**. So we need to scope the action and generate several more permissions.

> For trading platforms:
>```
>:P1    rdf:type        odrl:Permission .
>:P1    dc:desciption   "Platform trading"^^xsd:string ;
>:P1    odrl:action     [  rdf:type       md:TradeAutomatically ;
>                           md:actionScope md:Platform 
>                        ]  .
>```
> For trading as both a principal and a broker:
>```
>:P2    rdf:type        odrl:Permission .
>:P2    dc:desciption   "Automated trading as both a principle and a broker"^^xsd:string ;
>:P2    odrl:action     [  rdf:type       md:TradeAutomatically ;
>                           md:actionScope ( md:Principle , md:Brokerage )
>                        ]  .
>```
> For trading as only a principle:
>```
>:P3    rdf:type        odrl:Permission .
>:P3    dc:desciption   "Automated trading as a principle"^^xsd:string ;
>:P3    odrl:action     [  rdf:type       md:TradeAutomatically ;
>                           md:actionScope md:Principle 
>                        ]  .
>```
> For trading as only a broker:
>```
>:P4    rdf:type        odrl:Permission .
>:P4    dc:desciption   "Automated trading as a broker"^^xsd:string ;
>:P4    odrl:action     [  rdf:type       md:TradeAutomatically ;
>                           md:actionScope md:Brokerage 
>                        ]  .
>```
> For trading as a principle in a managed environment:
>```
>:P5    rdf:type        odrl:Permission .
>:P5    dc:desciption   "Automated trading as a principle in a managed environment"^^xsd:string ;
>:P5    odrl:action     [  rdf:type       md:TradeAutomatically ;
>                           md:actionScope md:Principle 
>                        ]  .
>:P5    md:controls     md:Closed , md:Deployed .
>```
> Note that this final permission has an additional constraint because it only covers automated trading in managed evironments: the **controls** over data access must be **closed** (allowing acess to only named users) and **deployed** by the vendor of the data.

Now the automated trading permissions also come bundled with a permission to calculate indices, so long as these index calculations are used only to support the automated trading and are not distributed externally. We'll deal with these restrictions on the use of the index calculation later (using a **duty**), but the permission to do the calculations is so:
>```
>:P6    a               odrl:Permission .
>:P6    dc:desciption   "Index calculations for automated trading"^^xsd:string .
>:P6    odrl:action     md:CalculateIndex .
>```

There is a separate permission to calcluate indices that comes without the restictions above. Again, we'll deal with what can be done with the output of these calculations later, but as it includes external distribution, there is a constraint on the calculation itself: it's results must be **irreversable** and **non-substitutive** - i.e. there's no way back to the original data.
>```
>:P7    a               odrl:Permission .
>:P7    dc:desciption   "Index calculations for benchmarking and distribution"^^xsd:string .
>:P7    odrl:action     [  rdf:type       md:CalculateIndex ;
>                           md:derivation  md:Irreversable , md:Non-Substitutive
>                        ] .
>```

There is one more permission that allows index calculations. Its output is resticted to internal use excluding automated trading. Again, we'll deal with the output restrictions later, so, for now, this permission looks like :P6 above.
>```
>:P8    a               odrl:Permission .
>:P8    dc:desciption   "Index calculations for internal use excluding automated trading"^^xsd:string .
>:P8    odrl:action     md:CalculateIndex .
>```

Finally, there is a permission that covers many of the traditional aspects of non-display use "including, but not limited to, risk management, profit and loss calculation, portfolio valuation, quantitative analysis, fund administration, fund accounting, portfolio management or instrument pricing." As the output can be distributed, any derivation must again be irreversable and non-substitutive:
>```
>:P9    a               odrl:Permission .
>:P9    dc:desciption   "Non-display use excluding automated trading and index calculations"^^xsd:string .
>:P9    odrl:action     [  rdf:type       md:NonDisplayUse ;
>                           md:derivation  md:Irreversable , md:Non-Substitutive 
>                        ] .
>```

### Disallowed Actions
Much of the power of this license is in what you *can't do*. Here we'll just specify what you can't do with the data received from DBAG. We'll cover what can, and can't, be done with the *output* of any derivation (or index calculation) later.

You can't display the data, distribute it externally, or use it to price **contracts-for-difference**.
> So we have three prohibitions
>```
>:Pr1   a               odrl:Prohibition .
>:Pr1   dc:desciption   "No dispay allowed"^^xsd:string .
>:Pr1   odrl:action     odrl:Display .
>
>:Pr2   a               odrl:Prohibition .
>:Pr2   dc:desciption   "No distribution allowed"^^xsd:string .
>:Pr2   odrl:action     odrl:Distribute .
>
>:Pr3   a               odrl:Prohibition .
>:Pr3   dc:desciption   "No pricing of contracts-for-difference allowed"^^xsd:string .
>:Pr3   odrl:action     [  rdf:type       md:Price ;
>                           md:assetClass  md:ContractForDifference
>                        ] .
>```
But there are more: prohibitions that are specific to individual permissions. :P9 offers non-display use but excludes automated trading and index calculations. As these exclusions are not implicit in the meaning of non-display use, we must make the prohibitions explicit:
>```
>:P9    odrl:prohibition  ( [  rdf:type      odrl:Prohibition ;
>                               odrl:action   md:CalculateIndex        
>                            ] , 
>                            [  rdf:type      odrl:Prohibition ;
>                               odrl:action   md:TradeAutomatically        
>                            ] ) .
>```

So, for the permission :P9, and only :P9, there are prohibitions on index calculations and trading automatically.

Now :P8 also excludes automated trading. But as the action it allows (index calculations) does explicitly exclude automated trading, our expression of this prohibition is, in some senses, a judgement call: does it perhaps aid expressivity (for humans) and/or does it allow us to test that the target rights management system can distinguish between calculating an index and trading automatically? Either way, we don't lose any information by not expressing it explicitly.

For brevity's sake, I'm going to leave it out.


## Assets
We need the [fee schedule](https://www.mds.deutsche-boerse.com/resource/blob/1334780/60ddf0a87283cdc57ec8ab9ae88ca4cc/data/NonDisplay_Price_List_5_11.pdf) to see what assets this non-display license can control.

I'm going to select one: Xetra Ultra - market data for German and international instruments traded on the Xetra and Frankfurt Stock Exchange.

From the fee schedule, we can see that Xetra Ultra is just one of three views on the underlying resource: pricing and trading data from the Xetra exchange. Xetra Order by Order is lower latency and offers the full book, while Xetra Core is slower and offers less depth. These "views" are key to defining which assets the permissions control. 

But first, when we describe the resource, we want to ignore these distinctions to point to the underlying, unfiltered, data.

### Resources
We know a few things about this resource from the [product description](https://www.mds.deutsche-boerse.com/mds-en/data-services/real-time-market-data/spot-markets/Xetra-Ultra-1341016). It's provider is the Deutsche Boerse. It covers the following asset classes:
* Stocks
* Funds
* Certificates and warrants
* Bonds
* Exchange traded funds, notes, and commodities (ETFs, ETNs, and ETCs) 

We know that the data is dynamic and endlessly changing. It's not an end-of-day summary or an historical snap shot.

We have an operating MIC for the Xetra exchange: "XETR". The market MIC is the same (and there are several other market MICs that might be applicable).

But we don't seem to have an identifier provided by the exchange itself.

> We can pull this together so, calling the resource :R1:
>```
>:R1    rdf:type        md:Resource .
>:R1    rdfs:label      "Xetra" .
>:R1    dc:description  "Market data for German and international instruments traded on the Xetra and Frankfurt Stock Exchange" .
>:R1    md:provider     <https://permid.org/1-4298007872> . # Identifier for DBAG
>:R1    md:service      [  rdf:type     md:Service ;
>                           md:venue     [   rdf:type        md:Venue ;
>                                            rdfs:label      "Xetra" ;
>                                            md:operatingMic "XETR" ;
>                                            md:mic          "XETR"
>                                        ] ;
>                        ] .
>:R1    md:contentNature  md:Dynamic .
>```

I've left out any description of the asset classes covered until we have a standard way of describing them.

### Timeliness of Delivery
At a product level, the Deutsche Borse distinguishes between the latency at which Xetra Order by Order, Xetra Ultra, and Xetra Core are delivered. But this is not explicitly defined. Perhaps it's captured in an SLA. The license only cares that the data is real-time, and that real-time data is delivered within 15 minutes from time of issue. So we'll just capture that in our definition of the Asset, which we'll call :A1:

>```
>:A1     rdf:type                   odrl:Asset .
>:A1     rdf:label                  "Xetra Ultra" .
>:A1     md:resource                :R1 .
>:AI     md:timelinessOfDelivery    [  rdf:type             time:ProperInterval , md:Realtime ;
>                                       time:intervalEquals [  rdf:type    time:ProperInterval ;
>                                                              md:timeReference  time:Instant , md:TimeOfIssue ;
>                                                              time:hasXSDDuration "PT15M"^^xsd:duration
>                                                           ]
>                                    ] .
>```

### Order Book Depth
The differences in book depth between the three products are explicity defined. For Xetra Ultra, it's up to ten. Let's use some common language to descibe the asset as Level 2, with a book depth that runs from 1 to ten.

>```
>:A1      md:depthOfMarket            [  rdf:type             md:Level2 ;
>                                         md:positionFrom      1 ;
>                                         md:positionTo        10 ;
>                                      ] .
>```

## Policies and Permissions I
All the permissions and prohibitions described above target the asset Xetra Ultra. We can update them so:
>```
>:P1    odrl:target                   :A1 .
>:P2    odrl:target                   :A1 .
>:P3    odrl:target                   :A1 .
>:P4    odrl:target                   :A1 .
>:P5    odrl:target                   :A1 .
>:P6    odrl:target                   :A1 .
>:P7    odrl:target                   :A1 .
>:P8    odrl:target                   :A1 .
>:P9    odrl:target                   :A1 .
>:Pr1   odrl:target                   :A1 .
>:Pr2   odrl:target                   :A1 .
>:Pr3   odrl:target                   :A1 .
>```

By triangulating between the [guidance note](https://www.mds.deutsche-boerse.com/resource/blob/1334848/d0f90031dcf62a50d8d31812304c9392/data/Guidance-Note-for-customers.pdf) and the [fee schedule](https://www.mds.deutsche-boerse.com/resource/blob/1334780/60ddf0a87283cdc57ec8ab9ae88ca4cc/data/NonDisplay_Price_List_5_11.pdf), we can see how the permissions are packaged up into policies.

Those offering automated trading are as follows.

>The first of these allows trading at any scale, and index calculations to support it. Let's call it :T1
>```
>:T1    rdf:type                      odrl:Offer
>:T1    dc:desciption                 "Automated trading for platforms"^^xsd:string ;
>:T1    odrl:permission               :P1 , :P2 , :P3 , :P4 , :P5 , :P6 ;
>:T1    odrl:prohibition              :Pr1 , :Pr2 , :Pr3 .
>```
>The second is the same as the first, except that it does not offer platform trading:
>```
>:T2    rdf:type                      odrl:Offer
>:T2    dc:desciption                 "Automated trading as both a principle and a broker"^^xsd:string ;
>:T2    odrl:permission               :P2 , :P3 , :P4 , :P5 , :P6 ;
>:T2    odrl:prohibition              :Pr1 , :Pr2 , :Pr3 .
>```
>The third offers only trading as a principle:
>```
>:T3    rdf:type                      odrl:Offer
>:T3    dc:desciption                 "Automated trading as a principle"^^xsd:string ;
>:T3    odrl:permission               :P3 , :P5 , :P6 ;
>:T3    odrl:prohibition              :Pr1 , :Pr2 , :Pr3 .
>```
>The fourth offers trading as a broker (and as a principle if it occurs in a vendor-managed environment):
>```
>:T4    rdf:type                      odrl:Offer
>:T4    dc:desciption                 "Automated trading as a broker"^^xsd:string ;
>:T4    odrl:permission               :P4 , :P5 , :P6 ;
>:T4    odrl:prohibition              :Pr1 , :Pr2 , :Pr3 .
>```
>The fifth offers trading as principle in a vendor-managed environment:
>```
>:T5    rdf:type                      odrl:Offer
>:T5    dc:desciption                 "Automated trading as principle in a managed environment"^^xsd:string ;
>:T5    odrl:permission               :P5 , :P6 ;
>:T5    odrl:prohibition              :Pr1 , :Pr2 , :Pr3 .
>```

Then there is a policy that allows index calculation for benchmarking and distribution:
>```
>:T6    rdf:type                      odrl:Offer
>:T6    dc:desciption                 "Index calculations for benchmarking and distribution"^^xsd:string ;
>:T6    odrl:permission               :P7 ;
>:T6    odrl:prohibition              :Pr1 , :Pr2 , :Pr3 .
>```

Finally, a policy that covers the other non-display uses:
>```
>:T7    rdf:type                      odrl:Offer
>:T7    dc:desciption                 "Other application usage"^^xsd:string ;
>:T7    odrl:permission               :P8 , :P9 ;
>:T7    odrl:prohibition              :Pr1 , :Pr2 , :Pr3 .
>```

We're not finished yet. The non-display license also controls the use of outputs of any derivations allowed under these policies. 

First, let's create a policy :U1 that controls the indices generated under the automated trading policies (:O1 to :O5). This offers a permission (say :P10) to trade automatically using these indices, and a prohibition (:Pr4) from distributing them. So:
>```
>:U1    rdf:type                      odrl:Set
>:U1    dc:desciption                 "Indices for internal use in automated trading"^^xsd:string ;
>:U1    odrl:permission               :P10 ;
>:U1    odrl:prohibition              :Pr4 .
>```
> Where :P10 allows automated trading (so long as the recipients are internal):
>```
>:P10    rdf:type                     odrl:Permission .
>:P10    dc:desciption                "Automated trading for internal recipients" ;
>:P10    odrl:action                  [  rdf:type       md:TradeAutomatically ;
>                                         odrl:recipient md:Internal 
>                                      ]  .
>```
>And :Pr4 prohibits distribution of the indices:
>```
>:Pr4    a                            odrl:Prohibition .
>:Pr4    dc:desciption                "No distribution allowed"^^xsd:string .
>:Pr4    odrl:action                  odrl:Distribute .
>```

The indices generated under policy :O6 (index calculations for benchmarking and distribution) can be distributed. So let's create a new policy for these, :O9. We can drop the prohibtion, and create a new permission that allows benchmarking and distribution.
>```
>:V1    rdf:type                      odrl:Set
>:V1    dc:desciption                 "Indices for benchmarking and distribution" ;
>:V1    odrl:permission               :P11 .
>```
> Where :P11 allows benchmarking and distribution:
>```
>:P11    rdf:type                     odrl:Permission .
>:P11    dc:desciption                "Indices for benchmarking and distribution" ;
>:P11    odrl:action                  ( md:Benchmark , ordrl:Distribute )  .
>```

Finally policy :T7 (other application usage) offers two permissions that involve derivations. Their outputs needs to be handled separately, so we need to create two new policies: :O10 and :O11.

The first covers indices for internal use but not automated trading. 
>```
>:W1     a                   odrl:Set ;
>:W1     dc:desciption       "Index calculations for internal use excluding automated trading"^^xsd:string ;
>:W1     odrl:permission     :P12 . 
>```
> The permission :P12 does the work:
>```
>:P12    a                   odrl:Permission ;
>:P12    dc:desciption       "Indices for internal use not including automated trading"^^xsd:string ;
>:P12    odrl:action         [    a                 md:Use ;
>                                  odrl:recipient    md:Internal
>                             ] ;
>:P12    odrl:prohibition    [    a                 odrl:Prohibition ;
>                                  odrl:action       ( md:TradeAutomatically , md:Distribute )
>                             ] .
>```

The second covers outputs from other non-display activities excluding index creation. These can be both distributed and used internally - though not for automated trading.
>```
>:X1     a                   odrl:Set ;
>:X1     dc:desciption       "Derivations other than indices for use and distribution not including automated trading" ;
>:X1     odrl:permission     :P13 . 
>```
> Again, the permission does the work:
>```
>:P13    a                   odrl:Permission ;
>:P13    dc:desciption       "Derivations for use and distribution not including automated trading" ;
>:P13    odrl:action         md:Use , odrl:Distribute ;
>:P13    odrl:prohibition    [    a                 odrl:Prohibition ;
>                                  odrl:action       md:TradeAutomatically
>                             ] .
>```

## General Obligations
So that's what we can do. What do we have to do in return?

### Audits
Structurally, DBAG's audit requirements differ in only one respect from those of the [CME](https://w3c.github.io/market-data-odrl-profile//translations/CME-CatA.html#audits): CME limits itself to at most one ordinary audit in a year; DBAG does not. This means we can remove the time interval constraint that the CME offers. Then DBAG's obligation looks so:

>```
>:O1    rdf:type            odrl:Duty .
>:O1    nl:creditor         <https://permid.org/1-4298007872> . # DBAG
>:O1    nl:hasDeadlineDelta [  rdf:type            time:ProperInterval ;
>                               md:timeReference    time:Instant , md:TimeOfNotification ;
>                               time:hasXSDDuration "P30D"^^xsd:duration
>                            ] .
>:O1    odrl:action         [  rdf:type            md:Accept ;
>                               md:scope            md:Audit ;
>                               odrl:count          "1"^^xsd:int
>                            ] .
>:O1    odrl:duty           :D1 .
>```
> Then specifying the duty on the DBAG to provide notice:
>```
>:D1  rdf:type    odrl:Duty .
>:D1  nl:debtor   <https://permid.org/1-4298007872> . # DBAG
>:D1  odrl:action [  rdf:type     md:Notify ;
>                      md:scope    md:Audit ;
>                      odrl:count  "1"^^xsd:int
>                  ] .
>```
> DBAG's "Extraordinary Audits" are exactly the same of those of the CME: there is no notice period, and DBAG has a duty to **report** reasonable suspicion. Actually the wording is slightly politer ("reasonable discretion"), but the meaning seems to be the same: "inaccurate information on the Information Usage, discrepancies in Reporting, delayed or incomplete reports, or the material deterioration of the Contracting Party’s asset situation". So we'll keep the original term.

Let's call the duties :O2 and :D2 respectively.
>```
>:O2    rdf:type            odrl:Duty .
>:O2    nl:creditor         <https://permid.org/1-4298007872> . # DBAG
>:O2    odrl:action         [  rdf:type             md:Accept ;
>                               md:scope             md:Audit ;
>                               odrl:count           "1"^^xsd:int
>                            ] .
>:O2    odrl:duty           :D2 .
>```
> Then specifying the duty on DBAG to report reasonable suspicion:
>```
>:D2  rdf:type      odrl:Duty .
>:D2  nl:debtor     <https://permid.org/1-4298007872> . # DBAG
>:D2  odrl:action   [  rdf:type     md:Report ; 
>                       md:scope     md:ReasonableSuspicion ;
>                       odrl:count   "1"^^xsd:int
>                    ] .
>```

### Controls
DBAG's take on controls is buried deep in its Market Data Dissemination Agreement. I'll unpick them at a later date.

### Service Facilitators
DBAG must be notified, and then consent to, any use of service facilitators by the licensee. The Notification duty will be similar to the one above, expect the action's scope is a **Service Facilitator**:
>```
>:D3  a                   odrl:Duty .
>:D3  nl:creditor         <https://permid.org/1-4298007872> . # DBAG
>:D3  odrl:action         [  rdf:type        md:Notify ;
>                             md:actionScope  md:ServiceFacilitator ;
>                             odrl:count      "1"^^xsd:int
>                          ] ;
>:D3  md:otherParties     md:ServiceFacilitator .
>```

Fulfilling this duty then activates the obligation on DBAG to give consent: 
>```
>:O3  a             odrl:Duty .
>:O3  nl:debtor     <https://permid.org/1-4298007872> . # DBAG
>:O3  odrl:action   [  rdf:type        md:Consent ;
>                       md:actionScope  md:ServiceFacilitator ;
>                       odrl:count      "1"^^xsd:int
>                    ] .
>:O3  odrl:duty     :D3 . 
>```

## Policy Update
We have seven **Offer** policies described above that allow non-display use of DBAG's data. We can add the four obligations to them so:
>```
>:T1  odrl:obligation  :O1 , :O2 , :O3 .
>:T2  odrl:obligation  :O1 , :O2 , :O3 .
>:T3  odrl:obligation  :O1 , :O2 , :O3 .
>:T4  odrl:obligation  :O1 , :O2 , :O3 .
>:T5  odrl:obligation  :O1 , :O2 , :O3 .
>:T6  odrl:obligation  :O1 , :O2 , :O3 .
>:T7  odrl:obligation  :O1 , :O2 , :O3 .
>```

## Specific Duties

### Attribute
When signing the non-display license, a licensee must acknowledge the Deutsche Boerse's ownership of its data. But there does not appear to be an ongoing duty to attribute ownership during data operations. So it's probably out of scope for this policy.

### Notification
DBAG is explicit in its insistence on once-off notification before any non-display activities are initiated. This is easily modelled:
>```
>:D4  a             odrl:Duty .
>:D4  nl:creditor   <https://permid.org/1-4298007872> . # DBAG
>:D4  odrl:action   [  rdf:type        md:Notify ;
>                       md:actionScope  md:Usage ;
>                       odrl:count      "1"^^xsd:int
>                    ] .
>```

Each time we use a new policy, we probably need to provide a new notification. So let's create seven of these duties, one each for the seven policies on offer: :D4-1, :D4-2, :D4-3, :D4-4, :D4-5, :D4-6, :D4-7. 

### Report
There doesn't appear to be an explicit reporting duty for non-display use. I wonder if it's covered by the notification duties described above?

### Pay
The payment duties follow exactly the same pattern as those described in the [CME Category A license](https://github.com/w3c/market-data-odrl-profile/blob/gh-pages/translations/CME-CatA.md#pay): pay monthly, on reciept of invoice, on 30 days notice. Just the creditor and the amounts are different.

>Let's specify the duty on DBAG to invoice first:
>```
>:D5-1  rdf:type        odrl:Duty ;
>:D5-1  nl:debtor       <https://permid.org/1-4298007872> . # DBAG
>:D5-1  odrl:action     [  rdf:type     md:Invoice ; 
>                           odrl:count   "1"^^xsd:int
>                        ] .
>```
>Now we can write the full payment duty. The monthly price for platform trading is €5350.00:
>```
>:D6-1  rdf:type            odrl:Duty ;
>:D6-1  nl:creditor         <https://permid.org/1-4298007872> . # DBAG
>:D6-1  nl:hasDeadlineDelta [  rdf:type             time:ProperInterval ;
>                               md:timeReference     time:Instant , md:TimeOfInvoicing  ;
>                               time:hasXSDDuration  "P1M"^^xsd:duration
>                            ] ;
>:D6-1  odrl:timeInterval   [  rdf:type              time:ProperInterval ;
>                               time:hasXSDDuration   "P1M"^^xsd:duration 
>                            ] ;
>:D6-1  odrl:action         [  rdf:type              odrl:Compensate ;
>                               odrl:unitOfCount      md:Application ;
>                               odrl:payAmount        "5350.00"^^xsd:float ;
>                               odrl:unit             <https://www.wikidata.org/wiki/Q4916> ; # Euro
>                               odrl:count            "1"^^xsd:int
>                            ] ;
>:D6-1  odrl:duty           :D5-1 .
>```

Simply by generating new identifiers for the duties, and amending the amount, we can generate the payment duties for all the other policies here. :D5-2 (invoice) and :D6-2 (pay, €2,942.50) for trading as both principle and broker; :D5-3 and :D6-3 (€2,140.00) for trading as a principle; :D5-4 and :D6-4 (€2,140.00) for broker trading; :D5-5 and :D6-5 for index calculations (€5,350.00); and :D5-6 and :D6-6 for other application usage (€1,284.00). The pricing of automated trading in a managed environment is, I imagine, set by the **vendor**.

## Policies Update II
We can now update the policies with the notification and payment duties:
>```
>:T1  odrl:obligation  :O1 , :O2 , :O3 , :D4-1 , :D6-1 .
>:T2  odrl:obligation  :O1 , :O2 , :O3 , :D4-2 , :D6-2 .
>:T3  odrl:obligation  :O1 , :O2 , :O3 , :D4-3 , :D6-3 .
>:T4  odrl:obligation  :O1 , :O2 , :O3 , :D4-4 , :D6-4 .
>:T5  odrl:obligation  :O1 , :O2 , :O3 , :D4-5 , :D6-5 .
>:T6  odrl:obligation  :O1 , :O2 , :O3 , :D4-6 , :D6-6 .
>:T7  odrl:obligation  :O1 , :O2 , :O3 , :D4-7 , :D6-7 .
>```


## Permissions Update
Finally, we can tie the outputs of any derivations allowed under the permissions offered by DGAG, with the policies controlling thier use.

The policy :U1 controls the indices generated under the permission :P6 - index calculations for automated trading. We can link them so:
>```
>:P6    odrl:duty           :D7 .
>```
> With the duty being:
>```
>:D7     a                   odrl:Duty .
>:D7     odrl:action         odrl:nextPolicy .
>:D7     odrl:target         :U1 .
>```

The policy :V1 controls the indices generated under :P7 - index calculations for benchmarking and distribution. So:
>```
>:P7    odrl:duty           :D8 .
>```
> With the duty being:
>```
>:D8     a                   odrl:Duty .
>:D8     odrl:action         odrl:nextPolicy .
>:D8     odrl:target         :V1 .
>```

The policy :W1 controls the indices generated under :P8 - index calculations for internal use excluding automated trading. So:
>```
>:P8    odrl:duty           :D9 .
>```
> With the duty being:
>```
>:D9     a                   odrl:Duty .
>:D9     odrl:action         odrl:nextPolicy .
>:D9     odrl:target         :W1 .
>```

The policy :X1 controls the indices generated under :P9 - non-display use excluding automated trading and index calculations. So:
>```
>:P9    odrl:duty           :D10 .
>```
> With the duty being:
>```
>:D9     a                   odrl:Duty .
>:D9     odrl:action         odrl:nextPolicy .
>:D9     odrl:target         :X1 .
>```

You can access the full translation [here](https://github.com/w3c/market-data-odrl-profile/blob/gh-pages/translations/DBAGNon-Display.ttl)
