Distribute

Display

Non-Display Use

    Trade Automatically

    Derive
    
    
    
## Automated Trading
```
odrl:action       [ a md:AutomatedTrading ] 

-

odrl:action       [ a md:AutomatedTrading 
                      md:purpose      [ a md:PlatformTrading ] // also [ a md:TradingAsPrincipal ] [ a  md:Brokerage ]
                  ] 
```
## Derive
```

odrl:action       [ a odrl:Derive ] 

-

odrl:action       [ a odrl:Derive 
                      md:derivation	[ a md:Irreversable ] , [ a md:Non-Substitutive ] 
                  ] 

-

odrl:action       [ a odrl:Derive 
                      md:derivation    [ a md:Irreversable ] , [ a md:Non-Substitutive ] 
                      md:purpose       [ a md:CalculateIndex ]
                  ] 
```
## Non-Display
```
odrl:action       [ a md:NonDisplayUse 
                      md:derivation    [ a md:Irreversable ] , [ a md:Non-Substitutive ] 
                  ] 
odrl:prohibition  [ a                  odrl:Prohibition 
                    odrl:action        [ a            md:Derive 
                                         md:purpose   [ a md:CalculateIndex ]
                                       ] 
                  ]
		  [ a                  odrl:Prohibition ;
                    odrl:action       [ a md:TradeAutomatically ]     
                  ] 
```
## Display
```
md:users          [ a md:InternalParty ] 
odrl:action       [ a odrl:Display  
                      md:purpose    ( [ a md:TechnicalSupport ] [ a md:QualityAssurance ] [ a md:ProductDevelopment ] )
                  ] 
```
## Use
```
odrl:action       [ a md:Use ]

-

odrl:users        [ a md:InternalParty ]
odrl:action       [ a md:Use ; 
                    md:purpose      [ a md:Trading ]
                  ]

-

odrl:action       [ a odrl:Use 
	            md:purpose    ( [ a md:Trading] [ a md:Marketing ] )
	          ] 
```
## Distribute
```
odrl:action       [ a odrl:Distribute ] 

-

md:recipients     [ a md:ProfessionalParty ]
odrl:action       [ a odrl:Distribute ] 

-

md:service        [ a md:Service ;
                      md:provides   [ a              md:TradedProduct, md:Asset
                                      md:assetClass  [ a md:Warrants ] , [ a cfi:RWXXXX ]
                                    ] 
                  ] 
odrl:action       [ a odrl:Distribute ] 
```


## SIXX
Any software using Data for a purpose other than in support of its display or distribution is considered a fee-liable Application (aka non-display).

Real-time data only.

Non-display Information Usage means all accessing, processing or consumption of Real-time Data, whether or not connected with any other use of Data, for a purpose other than in support of its display or distribution, i.e. for the following Purposes of Usage: 
1. Trading Applications
1. New Original Work Applications
1. Reference Price Based Systems
1. Index Calculators


### Trading Applications
Trading Applications use Data for the purpose of generating quotations, routing and/or executing transactions semi-automatically or automatically. They include, but are not limited to, applications for algorithmic trading, program trading, smart order routers, and the automated monitoring of trading based activities. Examples of “trading based activities” are “black box” trading, order pegging including reverse pegging, mid-point and bid/offer pegging, limit order pegging, smart order routing, arbitrage, order management system, market making, execution management, pre-trade risk checks, risk management, electronic order flow, P&L and liquidity management.

### Index Calculators
Index Calculators are applications using Real-time Data for the purpose of calculating indices.

### New Original Works
New Original Work means any work that is created partly or entirely based on Data but does neither allow deducing Data by any means nor can it be used as a substitute for Data. Only the use of the Data for generating the New Original Work constitutes Non-display Information Usage. Examples of “New Original Work” include but are not limited to applications to calculate spread-betting, CFD’s (contracts for difference), Option pricing, Structured Products pricing. The User owns all proprietary rights to New Original Work created by or for User’s Group as far as the Licence Fees for Non-display usage are paid to the Supplier.

### Reference Price Based Systems
Reference Price Based Systems means any trading facility using the Data for price referencing for trading purposes. The term trading facility includes, but is not limited to multilateral trading facilities (MTF’S), organized trading facilities (OTF’S), alternative trading systems, dark pools and systematic internalization systems (SI’s). NonDisplay Licence Fees shall be remunerated cumulatively if User runs multiple systems (identifiable by but not limited to MIC codes). 


## NYSE

### Category 1
Category 1 applies when a data recipient’s Non-Display Use of real-time NYSE Market Information is on its own behalf as opposed to use on behalf of its clients.

### Category 2
Category 2 applies when a data recipient’s Non-Display Use of real-time NYSE Market Information is on behalf of its clients as opposed to use on its own behalf.

### Category 3
Category 3 applies when a data recipient’s Non-Display Use of real-time NYSE Market Information is for the purpose of internally matching buy and sell orders within an organization. Matching buy and sell orders includes matching customer orders for data recipient’s own behalf and/or on behalf of its clients.

This category applies to use in trading platform(s), such as, but not restricted to, alternative trading systems (ATSs), broker crossing networks, broker crossing systems not filed as ATSs, dark pools, multilateral trading facilities, exchanges and systematic internalization systems. 

Examples of Non-Display Use are, but are not limited to:
* Any trading in any asset class
* Automated order or quote generation and/or order pegging
* Price referencing for algorithmic trading
* Price referencing for smart order routing
* Operations control programs
* Investment analysis
* Order verification
* Surveillance programs
* Risk management
* Compliance
* Portfolio Valuation 


## CME
Non-Display Use: non-viewable use of Information in any system, process, program, machine or calculation other than in order to display or distribute Information for display. Such use may include, but is not limited to, calculation of P&L, portfolio valuation, order processing, use within Automated Trading Systems and automated order routing.

Automated Trading System: any system or computer software operated by a Licensee Group entity that generates and/or routes orders electronically with no, or only de minimis, human action involved in generating, sending and/or verifying orders.

### Automated Trading
CategoryA: Automated Trading Usage Category: Non-Display Use of Information by a Licensee Group entity in Automated Trading Systems for any of the following three uses:
1) Trading as a principal - Use of CME, CBOT, NYMEX or COMEX Information to trade as a principal on a CME Group exchange and for all other Information, trading as a principal;
2) Facilitating client business – Use of CME, CBOT, NYMEX or COMEX Information to facilitate client business on a CME Group exchange and for all other Information, facilitating client business; and/or
3) Smart Order Routing – Trading as a principal and facilitating client business, using Information on an execution venue other than a CME Group exchange.

The use of an execution management system/order management system to facilitate the Category A activities is permitted under the license.

### Internal Order Processing
Category B: Internal Order Processing: Non-Display Use of Information by a Licensee Group entity within electronic systems or computer software that internalize orders in full or in part, in order to determine the entry or non-entry of orders.

### Other Internal Non-Display Usage
Category C: Other Internal Non-Display Usage Category: Non-Display Use of Information by Licensee Group within electronic systems or computer software operated by a Licensee Group entity for any of the following uses:
1. Risk management;
1. Research and analysis;
1. Fund administration;
1. Portfolio management; and
1. Other use approved by CME in writing.

### Derived Data
The creation, calculation, issuance, distribution, settlement, maintenance or support of any derivative works, including, but not limited to: indexes, exchange traded products (ETP) (e.g. exchange traded funds (ETF), exchange traded notes (ETN)), quotes, price assessments, spot or amalgamated prices or values, ratios, curves, surfaces, charts, certificates, warrants, contracts for difference (CFDs) and other leveraged products, ETP values (e.g. indicative optimized portfolio values (IOPV), net asset values (NAV or iNAV)), any analytical reference figures or values calculated from Information for purposes of fund administration or portfolio management services, pre- and post-trade risk management services, or valuation services.

Licensee agrees that the Products must be created as a result of a material calculation, modification, manipulation, alteration, or change to the Information or any portion thereof, whereby: (i) the original values of the Information are no longer discernible; (ii) the Products cannot be used as a substitute for the Information; (iii) the Information may not be readily reverse engineered from the Product as CME may determine in its sole discretion; or (iv) the Information is used in whole, or in part, in conjunction, aggregation or combination with other Information or data to process, develop, create, or otherwise calculate a price or value. CME reserves the right to determine in its sole discretion whether a Product meets the requirements of this Section 2.4.


## NASDAQ
Non-Display is any method of access that involves access or use by a machine or automated Device without access or use of a Display by a natural person or persons.

### Includes:
* Automated Trading
  * All automated trading programs, applications, and scripts. Nasdaq recognizes that many programs including, but not limited to workbook software and applications and third party software and applications with auto-quoting/pegging (e.g. Microsoft Excel, GoogleDocs, Numbers for Mac or other third party software) may be utilized to implement an automated trade, and such use would be considered Non-Display. Other similar use cases would also require payment of the Non-Display license.
  * Orders that are created or delivered via an automated order handling logic
  * Automated conditional orders, or complex order chain building whereby an algorithm responds to certain pre-set conditions
  * Automated order/quote generation and/or order/quote pegging
  * Price referencing for use in algorithmic trading
  * Price referencing for use in smart order routing
* Program Trading and High Frequency Trading
  * The use of automated programs to trade instruments
* Order Verification
  * An Order Verification program that calculates estimated costs
  * An Order Verification program that provides warning/informational messages such as an order at a defined percentage threshold away from the quote
* Automated Surveillance Programs
* Risk management that encompasses auto stop loss/position exiting functions
  * Risk management, the process of identification and analysis of investment decision making, occurs whenever a person, bank, or other such interested party analyzes and attempts to determine their potential gain or loss and takes the appropriate action depending on their investment objectives.
  * Automatic order cancellation, or automatic error discovery
* Clearing and settlement activities
* Account maintenance (e.g. controlling margin for a customer account)
* Hot disaster recovery
* Trading Platform - in this context- shall mean any execution platform operated as or by a registered National Securities Exchange (as defined in Section 3(a)(1) of the Exchange Act), an Alternative Trading System (as defined in Rule 300(a) of Regulation ATS), or an Electronic Communications Network (as defined by Rule 600(b)(23) of Regulation NMS).

### Excludes:
* If an application is updating a portfolio and exposes such information on the display, this use is not considered Non-Display.
* For example, calculating VWAPs or other derived information for use in a Display is not considered Non-Display.
* If an application is updating a risk management officer on a trader’s position and exposing that information on a display, this is not considered Non-Display (provided there are no automated risk management/position exiting functions).
* Authorization and entitlement
* Transportation and cold disaster recovery servers – Distributor needs to identify and show that servers used in this process are only used for transportation of market data or trades, and are not utilized for any other fee-liable purpose identified above. Further, disaster recovery servers utilized in a cold environment are non-fee liable, but hot disaster recovery servers are fee-liable because they are typically optimized for load balancing.
* Devices [or servers] used in the transportation, dissemination or aggregation of data (distribution) are not considered Non-Display. The Distributor should be able to identify such Devices that exist within the market data infrastructure and identify how many Devices are used for distribution separate and apart from the Devices that are used for the reasons listed above.


## LSE

### Trading Use
Where appropriate, Customers are required to classify use of data in non-display ‘trading based activities’.

Examples of ‘trading based activities’ include but is not limited to usage of Data as: semiautomated or automated order/quote generation; order pegging including reverse pegging, mid bid / offer pegging, limit order pegging; price referencing for trading purposes (excluding in the operation of an ATP); smart order routing to facilitate trading; arbitrage; order management; execution management, pre trade risk checks; electronic order flow and liquidity management system; market making; ‘black box’ trading; program trading; algorithmic trading; operating multilateral trading facilities/dark pools, systematic internalisers.

Non-Display Usage Licence Charges are applicable also if in conjunction with the display of Data.

All Customers are required to complete, as appropriate, the type and level of London Stock Exchange real time data used for non-display purposes:
* Principal - Customers whose internal Non-Display Usage is for the purpose of (or includes) trading based activities as ‘principal’.
* Client Facilitation - Customers whose internal Non-Display Usage is for the purpose of (or includes) trading based activities to facilitate customer business.
* Trading Platforms - Customers whose Non-Display Usage is for the purpose of (or includes) the operation of trading platforms including but not restricted to systematic internalisers / multilateral trading facilities.

### Other Applications Usage
Applies to non trading-based customer activities, including but not limited to: risk management, quantitative analysis, fund administration, portfolio management.

Other Application Usage Licence Charges are applicable also if in conjunction with the display of Data.


### Indices/Benchmarks


