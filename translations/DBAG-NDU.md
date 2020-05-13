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
* The Market Data Dissemination Agreement and its various annexes is available from here (as are the above two documents): <https://www.mds.deutsche-boerse.com/mds-en/data-services/real-time-market-data/agreements>

## Actions

The DBAG Non-dispay use license is wide-ranging. It covers automated trading; index calcualtions; and other non-display uses.

What is non-display use? Historically, it was introduced when data started being routed to machines to act on, rather than people. There's a limit to how much data a human can process. This is not so for a machine. So non-display use was split out and priced accordingly.

Now machine use has proliferated, with some uses being more high-value than others. Non-display use try to make sense of this.

So we have lots of different actions available at different prices.

The first one is automated trading. So, at it's simplest, we have a permission that offers automated trading:

>```
>:P1    rdf:type        odrl:Permission .
>:P1    odrl:action     md:AutomatedTrading .
>```

But this permission comes in several versions (and price points) depending on whether it is exercised by a trading platform, a principle (trading on their own account), a broker, or a principle using a managed environment. So we need to scope the action and generate several more permissions.

>```
>:P1    rdf:type        odrl:Permission .
>:P1    dc:desciption   "Platform trading"^^xsd:string ;
>:P1    odrl:action     [  rdf:type       md:TradeAutomatically ;
>                          md:actionScope	md:Platform 
>                       ]  .
>```
### Allowed Actions

### Disallowed Actions

## Assets

### Resources

### Timeliness of Delivery

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
