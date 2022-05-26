## TOPIC: WFIC

**Michelle**  
We've talked about the WFIC event in October. There's an appetite for a more technical stream that explains the nuts and bolts of how all this works together.

**Gavin**  
Mark Bird and I have talked about in the past. I'm still sounding out folks here at TMX to see to what extent we as an exchange might be able to participate. I think it would be well rounded if we had an exchange perspective on ODRL. So I'll keep you posted on that. We might be able to participate if we're invited.

**Ben WS**  
I think an end-to-end demonstration, running all the way from data originator, through data vendor, to data consumer would make a very powerful demonstration.

**Gavin**  
I agree. We'll keep you posted on that.

## TOPIC: Actions From Our Lat Meeting

**Michelle**  
To summarise the actions from our last meeting: Laura and I are looking at reference data contracts. We also highlighted industry classifications to see if there are any unusual or different rights that occur in those types of agreements. We also talked about the use of benchmark data for index creation. Laura was going to look at some use cases for that. But one of the issues that was raised was how we cover off things like affiliate rights and contract scope. For example, some contracts are restricted to the buy-side or sell-side. Do we want to model this?

## TOPIC: Contract Scope

**Ben WS**  
I think that's that is very much something that we can model. We can make a distinction between the licensee who actually signs the contract and the additional assignees that they then put on the list of affiliates they provide to the exchange. We can also put duties on these permissions so that if you want to add a new organisation to that list, then you have to get the consent of the exchange. But we're certainly not making distinctions yet between buy side and sell side. But if there are some common distinctions, it would be very easy for us to to add them. We've got the mechanism to make the distinctions; we just don't have the terms to state them.

**Michelle**  
Yeah, because it's a restriction on where the data or the services can be used. You need to really understand this as part of understanding the rights. So we should start to capture that information.

**Ben WS**  
We could begin to make a list now of the common terms or common distinctions that specify a contract's scope.

**Michelle**  
The ones that I see quite commonly, which Laura was mentioning, are the distinction between buy-side and sell-side, custody, and enterprise.

**Ben WS**  
Forgive my ignorance but what does custody mean in this context?

**Michelle**  
That was one that my sourcing team highlighted. It's function within a bank.

**Mark D**  
So we saw it first from Bloomberg in their static data license. Much to your point, **Michelle**, there's a buy-side/sell-side distinction. By site. I've never seen an exception in our context where buy-side was anything other than our asset management division. So sell-side would largely make up everything else except for our transaction bank, which does the custody type work. So custody appeared there. But I've not seen it show up in any other context.

**Michelle**  
No, I haven't. But I think that the key requirements is to narrow down the scope of where the services can be used.

**Mark D**  
There is more of an external reporting element in that custody business that they probably have in mind when they ring fenced it.

**Mark**  
I've seen some licenses that simply state that the license covers you and your majority owned or wholly owned affiliates. And I've seen other licenses that say that you must explicitly list any affiliates. Is that a distinction that we support in ODRL today?

**Ben WS**  
Today, we just assume that someone's going to make an explicit list of affiliates.

**Mark** 
It's definitely an operationally intensive activity to just maintain those affiliate lists. Big companies have hundreds. It's a challenge.

**Ben WS**  
So in a sense, if, I mean, the way I think about it is it's a sort of data management issue. And it's not specifically about our service. If we say the assignees are all the affiliates of this organisation. Then the if you you know, if you've got a list of the affiliates, and you can automatically associate them with that. With that with that set of permissions. I don't think it's something it's data management, not part of the standard itself if you see what I mean.

**Michelle**  
It's a question of who a policy applies to. It is very relevant. Can we distinguish between the different affiliate descriptions like majority-owned or wholly-owned? Are we able to apply that?

**Ben WS**  
Not at the moment. As I said, we've got the mechanisms to support it. We just don't have the terms at the moment.

**Mark D**  
It is a licensing restriction that we live with. So either at a legal-entity level, which is what we're talking about here, or at the division, departments, or business type level.

**Michelle**  
Sometimes, the affiliates have slightly different rights from the signing body. So you have to make that distinction. 

I think these distinctions are critical when looking at your rights. If you have the policies, you have to know who they apply to. We need to check this just to answer the common question: can I use this data? So it would seem to be quite an important part of ODRL.

**Mark** 
I agree. If we're moving to a world where computer systems are making automated entitlement decisions, it seems a little weak to presuppose the user making the access belongs to an approved organisation - or an approved part of an organisation. The computers should be checking it.

**Ben WS**  
Yep. I will add some affiliate definitions that cover complete ownership and majority ownership. We could use a structure that allows the policy writer to specify what level of ownership defines an affiliate. 

I'll also introduce the concepts of buy-side, sell-side, and custody into the standard. I assume these three are mutually exclusive.

**Michelle**  
Yes. And then you have Enterprise.

**Ben WS**  
What does enterprise mean in this context? Would it be fair to say that buy-side/sell-side and custody are all subclasses of enterprise?

**Mark D**  
We're getting into slippery situation with enterprise because I've seen divisional enterprise licenses. So you could look at enterprise saying, well, it would be all divisions globally. So the global entity is covered everywhere. But I've also seen an enterprise license that only applies to a specific division, say our wealth management business or our investment banking division, but enterprise wide, which would be more of a geographic coverage more so than a business functional coverage.

**Ben WS**  
Okay.

**Mark D**  
It's unfortunate, but true.

**Ben WS**  
So within the scope of what we've just said, I think I can define some vocabulary and some rules. Is there anything beyond that scope that we should look at now?

**Michelle**  
It depends what level you want to go down to. A lot of licenses can go down to a quite granular level in terms of lines-of-business and department.

**Ben WS**  
I think I'll just produce some examples to cover those. Because I don't think we can standardize the descriptions of lines-of-business.

**Mark D**  
Yes, that gets very vendor specific. Future scope, possibly.

**Ben WS**  
What's your sense **Caspar**?

**Caspar**  
I'm aware of the buy-side/sell-side distinction in licensing - though not of the custodian issue.

Some of these questions start to create requirements for external dependencies. An affiliate may be wholly owned today but not tomorrow. So that state needs to be managed. I'm starting to think of all the data sources we're going to need for this. 

And again, we've seen contracts in which specific divisions are named. What we'd take is an identifier from a contract and map that on to a departmental code, which would be more stable against reorganisations. But that obviously doesn't tie into anything available in contracts today. 

**Michelle**  
Yes, licenses can refer to generic business structures because banks don't always share their actual business structures. 

**Caspar**  
Then there are desk specific licenses.

**Michelle**  
And individual use.

**Michelle**  
Any further comments on that discussion? 

Okay, so for the next item Ben is presenting a deep dive on duties.

## TOPIC: Duty Scope

**Ben WS**  
Now we're writing code around these these duties, I wanted to update the group with what we've learnt and to share a dilemma.

This is an example of some machine learning running over a contract. It's reasonably accurate at picking up duties. So here we get an indication that it's a duty; here we see who is the subject of the duty - the licensee; what's the action they have to take - pay; what is it they have to pay - fees; who do they have to pay - the CME; they have to pay within 30 days and the time references is receipt of an invoice. So the system can identify this kind of duty quite accurately. 

Here's another example - a duty where you have to identify and record your use, and you have to do it per device. So it's picking up the reporting duty. But this success brings a dilemma. There are lots of duties that I would argue we're not particularly interested in and that we don't want to represent - certainly not at this early stage. 

Here we have a duty to maintain internal controls, which is fine. That we want to capture. But here, for instance, are some duties that we're trying to teach the ML not to pick up: you must pay fees for unlicensed use of information. Now, we're off the best path here. We're on the "what happens when it all goes wrong" path. 

Here's another one: licensee shall use all reasonable efforts to assist CME in the prevention, identification curtailing of unlicensed activity. It's another duty but, you know, do we really want to capture at this level of granularity? Again, it's off the golden path.

Now my my sense is that we probably don't. What we're really focusing on is the path that keeps us compliant - not what happens when we fall off. I think the scope of the latter is too large. And when things go wrong, that's really when you should be moving away from an automated system and towards your market data experts and lawyers!

What do others think?

**Mark D**  
That makes sense to me. I don't think we're looking to pollute our systems with willful blindness type items. We need to focus on the actions that are clear. 

**Caspar**  
I think in the two cases you've presented that the term "reasonable effort" makes it too vague to enforce. But there are more concrete examples that we could cover - like late payment. There will be a clear remedy that can be followed and enforced.

**Ben WS**  
I understand where you're coming from. I know that ODRL does have a remedy mechanism built into it. But I think that, in terms of adoption, we should cleave to as much simplicity as possible. Maybe we look at remedies at a later stage. But right now, I worry that if we were to start looking at remedies, the standard would becoming quite complex. And that that will delay adoption.

**Caspar**  
I agree. There's more value in not including all this sort of peripheral complexity at this stage. It need not be on the pathway we demonstrate and prove out.

**Mark D**  
This shouldn't also be a substitute for eyes on the document.

**Ben WS**  
Exactly. Okay, with that in mind, it seems to me that we can say that there are not much more than nine key types of duty that we're primarily interested in. We can quibble about the exact number. We can slowly add duties as we go along. 

But I've been writing code to manage the state of these nine. And it's really made me tighten up the way that we describe duties.

**Mark**  
So, as always, I agree that the end goal of automating entitlement decisions is important. But I think assisting market data admins going about their day-to-day business is also a really important goal. What are what are my duties? How often do I have to report? What do I need to report? I think that's an equally important end goal.

## TOPIC: Activation Conditions

**Ben WS**  
So do I. But in a sense, we get that for free if we can solve the harder problem. Because if we can describe it to a computer then we can certainly describe it to a person. Computers are a lot dumber than people. 

So first of all, there are activation conditions. When does a duty activate? When do I have to fulfill it? It's clearly important that we know what the activation condition of a duty is. And it seems to me they're actually very few of them. 

Some track the state of the world. When a third party becomes a recipient of the data often triggers a number of duties that then need to be fulfilled. 

We won't always want a duty to activate every time an individual from an external party accesses the data. (Though we might for an attribution duty). Sometimes we want a duty to fire only when an external party that is an organisation first receives the data. So it's not firing every single time one of their employees accesses it but does fire when the organisation first accesses it. 

Then there are duties that activate when a new user executes a permission. This might be an internal party - a new affiliate, for example - or a service provider. Then it's quite likely that you're going to have to ask the consent of the exchange.

Some duties like reporting and payment aren't dependent on changes in the state-of-the-world but are triggered on the clock. They activate periodically. So we need to specify the period.

These are the only types of activation condition that I've seen in the nine key duty types.

## TOPIC: Actions from Today's Meeting
**Ben** to suggest means of modelling contract scope.
**Michelle/Gavin** to explore WFIC options

