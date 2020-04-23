# License
The CME Category A License: Automated Trading Usage Category.

The interpretation presented below is a work in progess. It's presented solely as an exploration of automated rights management, and intended to provoke debate.

### License Documentation
We need five documents from the CME to understand this license:
* The overarching guide to the documentation: https://www.cmegroup.com/market-data/files/information-license-agreement-ila-guide.pdf
* The majority of the terms of the license are available in the Information License Agreement: https://www.cmegroup.com/content/dam/cmegroup/files/download/information-license-agreement-sample.pdf
* The specific terms relating to non-display usage: https://www.cmegroup.com/content/dam/cmegroup/files/download/information-license-agreement-schedule-4-sample.pdf
* The fee schedule: https://www.cmegroup.com/content/dam/cmegroup/files/download/cme-market-data-fee-list-apr-2020.pdf
* Reporting requirements: https://www.cmegroup.com/content/dam/cmegroup/files/download/information-license-agreement-schedule-3-sample.pdf

# Actions
### Allowed Actions
The key actions the consumer can take are  specified in [Schedule 4](https://www.cmegroup.com/content/dam/cmegroup/files/download/information-license-agreement-schedule-4-sample.pdf). We’re after Category A: Automated Trading Usage. 

Three usage rights are defined: trading as a principle on a CME Group exchange; trading for clients on a CME Group exchange; or doing either of these on another exchange. If we were being literal, we would define four actions here:
1.  Trading as a principle on a CME Group exchange
2.  Trading as a principle off a CME Group exchange
3.  Trading for a client on a CME Group exchange
4.  Trading for a client off a CME Group exchange

But we can then model these as just two actions: **trading as a principle** and **trading for a client** which we could then constrain by venue: on or off a CME Group exchange.

But the venue doesn’t actually seem to matter; we’re allowed to trade anywhere. So, we can drop the constraint.

Equally we could roll up (aka superclass) trading as a principle and trading for a client under the umbrella term of **automated trading**. 

>So let's create a permission with the identifier :P1 that allows this:
>```
>   :P1     a               odrl:Permission .
>   :P1     odrl:action     [ rdf:type md:AutomatedTrading ] .
>```
>What does this mean? Just that :P1 is a permission that allows actions that are of the type md:AutomatedTrading.

The base license (aka the [Information License Agreement](https://www.cmegroup.com/content/dam/cmegroup/files/download/information-license-agreement-sample.pdf)) allows an additional usage right: to create limited derivative works solely for internal business purposes. This is clearly a **derive** action where the **use** of the output of the derivation is contrained to **recipients** who are **internal** to the licencee .

>Let's create another permission that allows us to make derivations
>```
>   :P2     a               odrl:Permission .
>   :P2     odrl:action     [ rdf:type  odrl:Derive ] .
>```
>But what can we do with the output of the derivation? We can use it, but only if the recipient of the output is internal to the licencee. So let's create another permission that expresses this:
>```
>   :P3     a           odrl:Permission .
>   :P3     odrl:action [   rdf:type  odrl:Use ;
>                            odrl:recipient   [ rdf:type  md:Internal ]
>                 ] .
>```
>What does this mean? It's a permission to use the output of the derivation so long as the recipient of the data is internal. 

### Disallowed Actions
The [Information License Agreement](https://www.cmegroup.com/content/dam/cmegroup/files/download/information-license-agreement-sample.pdf) is clear that the licensee cannot **distribute** or **grant use** of CME's data. In addition, [Schedule 4](https://www.cmegroup.com/content/dam/cmegroup/files/download/information-license-agreement-schedule-4-sample.pdf) makes it clear that this license offers only **non-display use**, which precludes **displaying** the data.

>We can model this with a prohibition. Let's give it the identifier :PR1.
>```
>:PR1   a           odrl:Prohibition ;
>        odrl:action [  rdf:type  odrl:Display ] , [  rdf:type  odrl:Distribute ] , [ rdf:type  odrl:GrantUse ] .
>```
>So actions of type display, distribute, or grant use are prohibited.

The burden of prohibitions on the derived data are a little lighter. You can't distribute it. So let's create a new prohibition :PR2
>```
>:PR2   a           odrl:Prohibition ;
>        odrl:action [  rdf:type  odrl:Distribute ] .
>```

# Assets
So far we haven't explicity specified the data that these permissions and prohibitions control. Let's do it now. For this example, I'm going to chose one of CME's **products**: the Eurodollar Futures Contract.

### Resources
The Eurodollar Futures Contract is our underlying **resource**. There are a few things we can say about it. It has a **provider** - the CME. I'm also going to say it's a **service**, which has a **code** and a trading **venue** (I may be using the wrong terms here). There's also something we can say about its nature: it's **dynamic**, endlessly changing.

>Let's call the resource :R1
>```
>:R1    rdf:type      md:Resource .
>:R1    rdfs:label        "Eurodollar Futures Contract" .
>:R1    md:provider         <https://permid.org/1-4295899615> . # Identifier for CME
>:R1    md:service      [  a           md:Service ;
>                               md:venue  [   a               md:Venue ;
>                                               rdfs:label    "Globex" ;
>                                               md:operatingMic "XCME" ;
>                                               md:mic      "GLBX"
>                                           ] ;
>                               md:code   "GE"
>                           ] ;
>:R1    md:contentNature  md:Dynamic .
>```
>NOTE: this would look a lot nicer, and be a lot safer, if we had globally unique identifiers for services and venues like we do for providers.
> To support interoperability, we can also say that this resource is a dcat:DataSet and a  prov:Collection so:
>```
>:R1    rdf:type    dcat:DataSet ,  prov:Collection .
>```

There's another version of this resource that differs in its **content nature** (and, potentially, on pricing). It's the **end-of-day** summary, so it's **static**. It doesn't change.

>Let's call the resource :R2
>```
>:R2    rdf:type      md:Resource , dcat:DataSet ,  prov:Collection .
>:R2    rdfs:label        "Eurodollar Futures Contract" .
>:R2    md:provider         <https://permid.org/1-4295899615> . # Identifier for CME
>:R2    md:service      [  a           md:Service ;
>                               md:venue  [   a               md:Venue ;
>                                               rdfs:label    "Globex" ;
>                                               md:operatingMic "XCME" ;
>                                               md:mic      "GLBX"
>                                           ] ;
>                               md:code   "GE"
>                           ] ;
>:R2    md:contentNature  md:StaticEOD .
>```

It's a little difficult to identify the output of the derivation. It doesn't exist yet! So I'm going to see if I can get by without explicitly naming or describing it.

### Timeliness of Delivery
The permissions that control the use of market data are highly sensitive to the speed at which that data is delivered. Data delivered in milliseconds is far more valueable than data delivered in minutes, hours, or months.

In the language of ODRL, the assets that our permissions control are refinements of the underlying resource. For maket data, that will usually include specifying the **timeliness of delivery**.

The [Information License Agreement](https://www.cmegroup.com/content/dam/cmegroup/files/download/information-license-agreement-sample.pdf) enumerates how the CME sees it. **Realtime** data is data recieved within ten minutes of **time of issue** (by the market). **Delayed** data is recieved between ten minutes and eight hours of time of issue. **End-of-day** data is **embargoed**, and make available at **market close**.

So we have three assets here:
1. The Realtime Eurodollar Futures Contract
2. The Delayed Eurodollar Futures Contract
3. The End-of-Day Eurodollar Futures Contract


Unfortunately, it's surprising difficult to get computers to handle time and time periods. Anyone remember the millenium bug?  So bear with me on this one.

>Let's call our three assets :A1, :A2, and :A3. 
>First, realtime:
>```
>:A1     a                            odrl:Asset .
>:A1     md:resource                  :R1 .
>:AI     md:timelinessOfDelivery      [   a                   time:ProperInterval , md:Realtime ;
>                                       time:intervalEquals [   a                   time:ProperInterval ;
>                                                             md:timeReference  [ a   time:Instant , md:TimeOfIssue ] ;
>                                                             time:hasXSDDuration "PT10M"^^xsd:duration
>                                                           ]
>                                     ] .
>```
>Then delayed:
>```
>:A2    a             odrl:Asset .
>:A2    md:resource         :R1 .
>:A2    md:timelinessOfDelivery   [   a         time:ProperInterval , md:Delayed ;
>                   time:intervalAfter  [   a           time:ProperInterval ;
>                               md:timeReference  [ a   time:Instant , md:TimeOfIssue ] ;
>                               time:hasXSDDuration "PT10M"^^xsd:duration
>                                
>                             ] ;
>                   time:intervalBefore [   a           time:ProperInterval ;
>                               md:timeReference  [ a   time:Instant , md:TimeOfIssue ] ;
>                               time:hasXSDDuration "PT8H"^^xsd:duration
>                             ]
>                   ] .
>```
>Finally, end-of-day:
>```
>:A3    a             odrl:Asset .
>:A3    md:resource         :R2 .
>:A3    md:timelinessOfDelivery   [   a                   time:ProperInterval , md:Embargoed ;
>                                       time:after      [   a                   time:Instant, md:MarketClose ;
>                                                             time:inDateTime   [ a         time::DateTimeDescription ; # Monday to Friday?
>                                                                         time:hour     "16"^^xsd:int ;
>                                                                         time::timeZone  <https://www.timeanddate.com/time/zones/ct>
>                                                                       ]
>                                                           ]
>                                     ] .
>```

Now we know the assets that our license controls, we can take a quick look at how the CME sells them to get a sharper idea of the policies and permissions we need.

# Policies and Permissions
By looking at the [fee schedule](https://www.cmegroup.com/content/dam/cmegroup/files/download/cme-market-data-fee-list-apr-2020.pdf) we see that only realtime data is charged for in the context of automated trading. That kind-of makes sense. Trading only with delayed data might be problematic! But let's support it for now.

So we have one charged-for **offer** that allows automated trading over realtime, delayed, and end-of-day data; and one free **offer** that allows for automated trading over delayed and end-of-day data. 

Each offer provides the two permissions we discussed above - the one that allows for actions of the type automated trading, and the other for actions of the type derive. But the permissions in the two offers **target** a slightly different set of assets. Only the first offer allows use of realtime data. So we actually have four different permissions.

>The permissions in the first offer cover realtime, delayed, and end-of-day data. So:
>```
>:P1     a               odrl:Permission .
>:P1     odrl:action     [ rdf:type md:AutomatedTrading ] .
>:P1     odrl:target     :A1 , :A2 , :A3 .
>```
>... and ...
>```
>:P2     a               odrl:Permission .
>:P2     odrl:action     [ rdf:type  odrl:Derive ] .
>:P2     odrl:target     :A1 , :A2 , :A3 .
>```
>The permissions in the second offer cover only delayed and end-of-day data. So they need new identifiers, :P3 and :P4:
>```
>:P3     a               odrl:Permission .
>:P3     odrl:action     [ rdf:type md:AutomatedTrading ] .
>:P3     odrl:target     :A2 , :A3 .
>```
>... and ...
>```
>:P4     a               odrl:Permission .
>:P4     odrl:action     [ rdf:type  odrl:Derive ] .
>:P4     odrl:target     :A2 , :A3 .
>```

We can do the same trick with the prohibitions, and then specify the two offers:

>Let's call them :T1 and :T2
>```
>:T1    a               odrl:Offer ;
>:T1    odrl:assigner     <https://permid.org/1-4295899615> ; # CME
>:T1    odrl:permission   :P1 , :P2 .
>:T1        odrl:prohibition    :PR1 .
>```
>... and ...
>```
>:T2    a               odrl:Offer ;
>:T2    odrl:assigner     <https://permid.org/1-4295899615> ; # CME
>:T2    odrl:permission   :P3 , :P4 .
>:T2        odrl:prohibition    :PR2 .
>```

# Duties & Obligations
Of course, none of this comes for free. To exercise these permissions we have some **duties** to fulfill. 

Some obligations relate to any data provided by CME: keep a record of access **controls**; **accept** an audit if the CME requests one.

Other duties are more closely tied to the specific permissions agreed: **report** on usage; **attribute** ownership; and, of course, **pay**.

But they all share a similar structure. They require an action to be taken. The actor can be called the **debtor**; the beneficiery, the **creditor**.

Duties become **active** at different times. As we're working in a subscription model, many of the duties we're talking about become active based on a periodicity - usually monthly - which we can augment with a **count**: the number of times within the **time interval** that the action must be taken. Sometimes, duties provide a grace period in which the action can be taken (like a credit policy does for payment). We can call that the **deadline delta**.

If we don't specify these things, then the duty becomes active immediately on accepting the offer and creating an **agreement**.

Let's start with audits.

### Audits
The [Information License Agreement](https://www.cmegroup.com/content/dam/cmegroup/files/download/information-license-agreement-sample.pdf) provides for two mechanisms by which the CME can launch an audit of a consumer. The first is on the basis of thirty-days **notice**. The second can be launched immediately, but requires **reasonable suspicion**. Each need only be accepted once per year.

> Let's call the first of these :O1 - Once a year, accept an audit by the CME on thirtly days notice. So the action is to accept an audit; the creditor is the CME; the time interval is a year; the deadline delta is thirty days; and the count one.
>```
>:O1    a           odrl:Duty ;
>:O1    nl:creditor     <https://permid.org/1-4295899615> ; # CME
>:O1    nl:hasDeadlineDelta [  a                   time:ProperInterval ;
>               md:timeReference    [ a   time:Instant , md:TimeOfNotification ] ;
>               time:hasXSDDuration "P30D"^^xsd:duration
>             ] ;
>:O1    odrl:timeInterval [ a           time:ProperInterval ;
>               time:hasXSDDuration "P1Y"^^xsd:duration 
>             ] ;
>:O1    odrl:action     [ a           md:AcceptAudit ;
>               odrl:count      "1"^^xsd:int
>             ] .
>```







