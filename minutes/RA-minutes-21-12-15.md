# CG Reference Architecture
*15th December, 2021*

**Ben**  
I thought I would give an overview of some of the key issues that I see in developing this reference architecture, some of the things that we can do together, and some indication of what the scope might be. And I'm going to take a very ODRL centric view.

## TOPIC: Supply Chain Artifacts (Slide 2)
**Ben**  
What does a supply chain need to share? And what does a supply chain not need to share? I want to try and draw that distinction so that there's a degree of freedom in implementation, but also constraints because some concepts and data needs to be shared across the supply chain. 

I think it's clear that policies of a certain type are being shared along the supply chain. But we've not really gone into detail about what exactly the semantics of these different policies are. 

I think it's absolutely critical to a reference architecture that that we do agree on these semantics. At the moment, there are three types of policy. It maybe that that we need more but I've only needed three so far. The one we've been focused on is the Agreement policy between a data provider and a data consumer. This contains the permissions that can be exercised. 

What an agreement policy is doing is modeling the rights assignment between a data provider and a data consumer. And the way it models that rights assignment is by translating that rights assignment into a set of permissions, prohibitions and duties. And I think we're pretty clear on what that does. 

Now there's a different type of policy and it's called a Request. And to put it really,simply, it models data use cases. What it's trying to capture is the idea that there's somebody at a trading desk, who says, I want to take these three data sets, I want to generate indices off them, and I want to share those indices with my customers. So effectively, it's a request for a set of rights that will allow a particular data use case to be satisfied. We call that a Request policy. 

And then there's another type of policy that we call an Offer policy. And, again naively, it models data products. Effectively it says, I am a data provider, and I am willing or offering this set of permissions, permissions duties and prohibitions for you to exercise if we can turn this offer into an Agreement. 

When I say an Offer policy models a data products, I mean only that it models the rights assignment offered by data product.  There's all sorts of metadata that goes into defining a product that we're not interested in. We're focused on the rights assignment that the products offering. 

So three types of policy. 

In a sense of policy is a way of gathering together a set of rules and contextualizing them with a certain semantics. So for all the rules gathered together in agreement, the implied semantics are that you are allowed to execute these rules. They are executable. Whereas in a Request policy or an Offer policy, the rules are not executable. 

In one, you're asking for the set of rules. And in the other, you're offering a set of rules. And those are the semantics of policy, which we probably need to sharpen up. And we probably also need to think about other any other types of policy that we need to support the kind of use cases that we're looking at now, I haven't come across them. So it's possible it is only three. That would be fantastic news. 

We know that these policies are being shared across the supply chain. So a data consumer may well share an a Request policy with a data provider. The data provider might respond with an Offer policy. Agreement policies are shared between providers and consumers. So we know that these policies need to be understood along the supply chain. 

## TOPIC: Organisation-level Functions (Slide 3)
**Ben**  
Let's try another lens and look at the functions within a single organisation that we want to support. It seems to me that there are three main ones. that we're trying to support. 

The first is policy creation and maintenance. And it seems to me that there are four key use cases in this space: creating policies, validating policies (which might include a lawyer's input), publishing policies, and then managing the life cycle of policies. 

The next key function that I've come across is decision support, where effectively, we're offering support primary to Market data managers dealing with requests and questions on Market data. And the example I keep using is that of a desk that wants to generate indices and share them with their customers. Are they allowed to do it? 

So we need to check if there are agreements in place that satisfy that use case. And if not, are there offers there that would support that use case? So it seems to me the key use cases here are:
1. Importing policies, because we need the policies in the system
2. Allowing users to create requests. It's an open question as to which users you allow to create requests.
3. Deciding requests. I don't mean making the final decision. But the software can say, this is allowed or this is not allowed. There may be lots of business reasons why even if it is allowed, you might not then fulfill the request. But certainly on the level of whether this is allowable or not, the software can make those decisions. 
4. Permissioning a user. So if the request comes in, and you can see we've got all of those agreements in place, it's all within budget, it's within the trading mandate, I'm going to add these permissions onto the user. And so permissioning users is a use case here.

The third, and perhaps final, function is enforcement, where we are actually ensuring that the permissions, prohibitions, and duties associated with an Agreement (which we've now associated users) are actually being enforced and there's no non-compliant use of the data. 

And again, I tried to list the use cases. I was kind of surprised to only came up with two:
1. Access control - that's obvious: you're going to check compliance around access. 
2. Redistribution is the other big use case. The question of whether I am allowed to redistribute this data to my customer seems different from the access control use case. 

But after these, I couldn't come up with any others. So that's an open question.

**Nigel**  
Where do you see reporting sitting? It's an attribute of the Agreement and presumably there's an engine that supports your reporting obligations in some way. 

**Ben**  
At this high level, I'm assuming that when a validity test is done, and we'll come to what those are, it checks that reporting is in place, and that this access is being reported. So that the decision as to whether or not this permission is valid includes checking all the various duties that might be in place. 

**Nigel**  
So a part of enforcement is actually validating that the terms of the agreement have been met?

**Ben**  
Yes, exactly. So there's a lot of complexity hidden behind the enforcement box.

Here it may be that we can only come up with two use cases, which would be great. We can represent them as flows or simple sequences diagrams. 

## TOPIC: Supported Flows (Slides 4/5)

The simplest one:
1. Data User publishes a Request to a Market Data Manager
2. Market Data Manager then makes a decision as to whether or not to support the Request.
3. They then permission the User
4. The User accesses the data. 

So a fairly fairly simple picture of what we want to support. We  want to guarantee compliance throughout this flow. This particular one is intra-organization.

## TOPIC: Compliance Check (Slide 6)

To do so, I want to point out that we make two types of check. The first one is the check done in deciding the Request. Here we match the Request against his existing Agreements (or Offers). It's actually a very simple and well known test: a subsumption check. All we're doing is checking that the graph that describes the Request is contained within the graphs provided by our Agreements (or Offers).

**Mark**  
You mentioned Offers and Agreements. Surely, a Request is compliant if contained within an Agreement and could be compliant if contained within an Offer, but only if that Offer were made into an Agreement?

**Ben**  
Thanks for asking that Mark. To me, you are speaking to the second type of test that we need to do: is this Permission valid - can it be exercised? To which (part of) the answer is: only if it's belongs to an Agreement. But this first test is answering a different question: do I have any policies that satisfy the Request. If I do, then the question of whether I can actually execute the Permissions is covered by the second test, which I will describe in a moment.

**Ben**  
If the result of the first test is an Offer policy, then we have a decisions to make: do we want to turn this Offer into an Agreement?

**Mark**  
So the first check is simply, is this something I can do in theory?

**Ben**  
Yes, exactly. To know whether I can do this in practice, I need to make the second test: check the deontic state of the rule. In the presentation, I've provided two state diagrams for discussion covering Permissions and Duties. We'll likely need another one for Prohibitions.

## TOPIC: Validity Check (Slides 7, 8)

**Ben**  
So we need to be able to get that state. Casper suggested the idea of Agents to manage local state, whether that's a reporting component, a payment system, or a service that attaches attributions or disclaimers. Then a system like the Policy Store (which understands the full policy) orchestrates the Agents to ensure that only compliant activities are allowed.
 
Agents are pretty low level and have strictly defined competencies. For example, we could have a request from a redistribution agent to share some data with a third party.

I'm going to use our Request policy terminology. I'm not totally convinced that in this context it means exactly the same as the Request policies we talked about earlier. I think it is. But again, this is something we'll need to bottom out. 

So the redistribution agent is requesting permission to distribute a specified Asset to a specified recipient. The policy store can identify the required permission from existing Agreements, check the status of any associated duties and constraints (perhaps by interacting with other Agents) and, if the permission is valid, can return a new Agreement policy saying this is the permission under which you can make the transfer, it's valid, so you can go ahead and make the transfer.

**Mark**  
One quick comment there. So, conceptually, I've always thought of ODRL as expressing the rights assignments in contracts - real contracts. But what I think you're describing here isn't a contract, saying, yes, you're approved to distribute that data to that individual. There's no piece of paper in a filing cabinet somewhere with the approval. Is the approval itself the artifact? And I guess a question that I think is worth exploring is whether that artifact is equivalent to your new Agreement. If it is, and it well may be, we have moved beyond how we've been traditionally thinking about ODRL as expressing the rights assignment in a contract.

**Ben**  
Right now, I'm assuming they're the same thing. But I think there is a really interesting discussion to be had whether they really are the same. Whichever way we jump, they're things that need to be interchangeable between organizations.

Coming back to the example, our redistribution agent is advertising what it's capable of doing. And what it's saying is "I am capable of enforcing attached disclaimer duties. So if I tell you, it's done, you can believe me. And also, just for interest (though there's nothing I can do about this), I want to track whether the consent Duty has been fulfilled or not. So please keep me updated on it." 

And there's another Agent, a consent agent, that's advertising its capability to enforce consent duties for this Asset.

It may well be that Data BP offers agents like this, which are capable of confirming that a consent is in place with an exchange. So the Policy Store can publish a Request containing the consent duty to that Agent and hopefully receive an Agreement back. 

We've only got two minutes left. Any reaction to this type of approach?

**Nigel**  
Seems like a standard microservice architecture model. You're essentially defining a small set of interfaces that would need to be consistently presented by anything that's going to play a part in the reference architecture. I mean, it sounds sensible. Part of it is making sure that we've identified all that an agent needs to advertise in terms of capabilities. But that, I suspect, comes from the duties we see in the (license) Agreements that we have in place.

**Ben**  
Yes - I think they do. Do you think we've missed anything really big out? There's anything comes to mind? Casper, what's your sense?

**Caspar**  
On the enforcement side of things, you would need some way for Agents to advertise their capabilities. You know, I can see these Agents being being nested or chained. 

The point of the Agent model is that they have limited agency but maximum autonomy.

The result might be an email sent to a human being who then manually does something. So we want this facade over these things. 

Some of these agent models could be at a much higher level. So for, for example, if you have a single agent responsible for structured product products and indices, they'd have multiple Agents underneath them to manage consent and reporting. So I would like to see these agents being able to communicate their abilities to each other. That could be baked into the spec. 

Then there's a similar notion there that would apply inter-firm. It would be the same sort of mechanism. It could be similar to how a useragent in a browser negotiates content type with a server.

**Ben**  
I'm aware that we're completely out of time. I will send an email out with this presentation attached. What would be really good would be if people could look at the set of use cases. If there are any that are missing, let's add them - and any additional user flows that we want to support.

**Nigel**  
Particularly in the context of decision support and the permissioning of users, some of the steps required are going to be quite time consuming. And they're going to be in a sequence. So there's a workflow aspect to this. So might the interfaces need to be  transactional or retain state? But you don't want them to be blocking. I think we need to think a little about this. Is there a workflow element? That might impact on the design of these interfaces.

