**Michelle**

Any objections to the minutes of last month's meeting? [No objections]

Agenda items:

Data types - we covered some previously, we want to expand on different data types and contract types that might bring up different activities

I mentioned that we'll look at reference data, but are there other types? We want to make sure the model covers every data type.

Laura, you are more familier with other types of contracts, how do you see them differing from exchange agreements?


## TOPIC: Reference Data Licensing Patterns

**Laura**

People have different definitions of reference data at different firms. I'm thinkin of it as a wide bucket, generally static, not real-time data, a very broad definition.

Things we haven't covered with excchange data?

Can afiliates use the data, and can we distribute to them? We see that in our reference data agreements. Reference data distribuors think of internal Fidelity affiliates as different entities.

Also derived data, can the data be used to create an index, and can it be used to create an index that forms the basis of an investment product?

Now we're seeing licensing that puts lots of restrictions around creating a product out of reference data.


**Michelle**
Do you see licenses for ICB or GICS?


**Laura**
We do have licenses for those and similar.

Needs enhanced licensing, that's new. Industry and sources of revenue - they're putting restrictions around what we can do around creating internal and external indices.


**Mark D**
Yes, it's an add on license that we need.

Index licensing in place with Refinitiv back when it was Reuters.


**Michelle**
Specifically for reference data?


**Mark D**
No, for all kinds of data. Reference data comes in with end-of-day bulk data.


**Michelle**
What would be useful would be to pick out of it what would be useful for modeling data rights.

Laure mentioend retail, custody, and buy-side. Do we need more around the scope of where data can be used or shared. Do those things need to be incorporated into the standard in order for us to identify and eforce rights?

Any key points to highlight? anything not covered by the standard at the moment?


Mark
Some have come up. Having the right to create derived data is something we've discussed.

Indices come up. If it's not included in the rights then it's something you have to include if it's something you want to perform.


**Michelle**
I think we can already model index creation?


**Caspar**
Yes

**Michelle**
Is it different in other contracts?


**Mark D**
Two layers: 

One is the providers - Refinitiv, Bloomberg. They put rights around use of the data they collect. Then there's the exchange rights we have to consider.

The picture is always changing in the case of exchange rights. CME now requires an MDLA. It's a moving target whether it's an index or another security type. 

We can't just look at the Refinitiv or Bloomberg list, we must look at the exchange data that's underlying the index.


**Emily**
Can i go back half a step? Can we check what we mean by reference data? I mean anything that's not price data. I expect reference data to be not real-time. Is that how we think about it?


**Laura**
Those are the two key characteristics.  How finely do we define the other characterics? Market data is real-time pricing.


**Emily**
Shout out if anyone has a definition that differs. If that's it, then there are lots of subcategories. And if that's right, I couldn't think of any license terms that would appear in reference data that don't appear in real-time market data licenses. All of the licensing activities are things we've already considered with respect to real-time.


## TOPIC: Service Facilitators

**Laura**
People are using more calculation ageents. We need something that tells us if we need to engage the vendor. Some vendors are clear. If you're Bloomberg, it's 60 questions and a TTPA


**Michelle**
Even if you're using a calculation, you're still the sponsor.


**Emily**
Is that wehre I've created an index and distributed it to an external party?


**Michelle** 
I was thinking more of the case where you've outsourced to a third-party calc agaent who's distributing. But as you're the sponser/owner of the index, you have to pay the distribution fees. There are a few exchanges moving in that direction.


**Emily**
I'd call them modelled outsourcing arrangments. We need to come up with the most general definition for that actor covering:
- caluclation agent
- managed hsoting provider
- hosting services
- Goldman Sachs host cloud
- anywhere you outsource a componenet of the work

Instead of me doing it, I'm paying.


**Mark**
We have service facilitator


**Caspar**
We have licensing agent and service facilitator. It's in the party roles section.

A service faciliator is shown as recieving and delivering data.

A licensing administrator is shown as as providing rights.


**Emily**
Would the be the right umbrella term for someone who creates data on my behalf?


**Caspar** 
Service facilitator, I think. We need to keep things really crisp.


**Mark**
Do we definite different functions of the service facilitator?


**Caspar**
Currently there are scope notes. We don't mention "calculation agent" as a concreate term in the vocabulary. Maybe we should to find an example where the model breaks?


**Laura**
We'll continue to see things evolve.


**Michelle**
Perhaps we could look at a couple of contractual clauses.


**Laura**
I was looking at one recently and can send it on.


**Laura**
In summary, it sounds to me like we've got what we need in the spec to describe reference data. Mayybe we want to double check the use cases of creating an index or an investement product. They're coming after you more for fees for that.


**Michelle**
We'd like to go through the different data types. The thing we need is examples. Does anybody have exmaples like ICB or GICS? If they don't raise any new patterns, we could move on from this topic.

## TOPIC: Reporting Demo

[Mark provides a demo of reporting]

## TOPIC: Counting Users

**Mark**
If we look at the index construct, where there are no declarations, you're licensing by location, by the data, by the number of users, and there's no reporting while you're within thse bounds, could ODRL handle the case when you want to add more users at a location? Within the bounds, and breaking the bounds, so going to the IP provider to get the additional rights.


**Caspar** 
As long as there's no additional negotiation, the systems can manage it. Ben is keen on treating these as offers. 


**Michelle**
What is meant by offer?


**Caspar**
If we think about an exchange policy that's not yet assigned, it's an offer


**Michelle**
Mark's example was a number of users of an index at a location.


**Caspar**
It would require you counting users against your contracts.


**Michelle**
Thanks all for your contributions today.


