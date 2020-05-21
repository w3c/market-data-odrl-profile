# Translation Two: DBAG Non-Display Agreement

The interpretation presented below is a work in progess. It's presented solely as an exploration of automated rights management, and intended to provoke debate.

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
6. [Policy Update](#policy-update)
7. [Specific Duties](#specific-duties)
   * [Attribute](#attribute)
   * [Report](#report)
   * [Pay](#pay)
8. [Permissions Update](#permissions-update)

## License
The DBAG Non-Display Agreement.

### License Documentation
We need several documents from DBAG to understand this license:
* Probably the best place to start is the guidance note to clients: <https://www.mds.deutsche-boerse.com/resource/blob/1334848/d0f90031dcf62a50d8d31812304c9392/data/Guidance-Note-for-customers.pdf>
* The general terms for non-display usage: <https://www.mds.deutsche-boerse.com/resource/blob/1637380/d77459a7f1492c6f06808a8949b19a3f/data/NonDisplay_GTC_3_5.pdf>
* The fee schedule: <https://www.mds.deutsche-boerse.com/resource/blob/1334780/60ddf0a87283cdc57ec8ab9ae88ca4cc/data/NonDisplay_Price_List_5_11.pdf>
* The Market Data Dissemination Agreement and its various annexes is available from here (as are the two documents above): <https://www.mds.deutsche-boerse.com/mds-en/data-services/real-time-market-data/agreements>

## Actions

### Allowed Actions

The DBAG Non-dispay use license is wide-ranging. It covers **automated trading**; **index calcualtions**; and other **non-display** uses.

What is non-display use? Historically, it was introduced when data started being routed to machines to act on, rather than people. There's a limit to how much data a human can process. This is not so for a machine. So non-display use was split out and priced accordingly.

Now machine use has proliferated, with some uses being more high-value than others. Non-display use try to make sense of this.

So we have lots of different actions available at different prices. We best read the [guidance note](https://www.mds.deutsche-boerse.com/resource/blob/1334848/d0f90031dcf62a50d8d31812304c9392/data/Guidance-Note-for-customers.pdf), so:

The first one is automated trading. So, at it's simplest, we have a permission that offers automated trading:

>```
>:P1    rdf:type        odrl:Permission .
>:P1    odrl:action     md:AutomatedTrading .
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
>:P8    odrl:action     [  rdf:type       md:CalculateIndex ] .
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
But there are more: prohibitions that are specific to individual permissions. :P9 offers non-display use but excludes automated trading and index calculations. As this exclusion is not implicit in the meaning of non-display use, we must make the prohibitions explicit:
>```
>:P9    odrl:prohibition  ( [  rdf:type      odrl:Prohibition ;
>                               odrl:action   md:CalculateIndex        
>                            ] , 
>                           [  rdf:type      odrl:Prohibition ;
>                               odrl:action   md:TradeAutomatically        
>                            ] ) .
>```

Now :P8 also excludes automated trading, but as the action it allows (index calculations) does explicitly exclude automated trading, our expression of this prohibition is, in some senses, a judgement call: does it perhaps aid expressivity (for humans) and/or does it allow us to test that the target rights management system can distinguish between calculating an index and trading automatically.

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




### Book Depth

## Policies and Permissions I

## General Obligations

### Audits

### Controls

## Policy Update

## Specific Duties

### Attribute

### Report

### Pay

## Permissions Update
