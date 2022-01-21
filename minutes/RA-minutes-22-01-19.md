# CG Reference Architecture
*15th December, 2021*



## TOPIC: Supported Flow: Enforcement (Slide 1)

**Ben WS**  
I'll talk to this [presentation](https://github.com/w3c/market-data-odrl-profile/blob/gh-pages/presentations/RefArch-22-01-19.pdf)

At this meeting, I intend to focus on the far right hand side of the diagram: the enforcement side of this right automation project, which I think is probably the least known and least understood. The actual automated enforcement of **Mark**et data licenses still remains a bit of a mystery.

## TOPIC: It's Policies All the Way Down (Slide 2)

**Ben WS**  
I want to make a rather bold prediction: there are only three things that we need to share across the supply chain and that they are the three types of policy: Request, Offer, and Agreement. I'm going to start using the terms Policy in this presentation in a way that possibly bends their definition so far that it breaks. So will people please keep an eye on that and see whether I'm actually introducing new artifacts.

**Ben WS**  
I'm going to talk through one example: redistribution. It's interesting because there are a lot of duties and protections built up around redistribution. It's also a significant area of compliance failure. So, if we can automate compliance in redistribution use cases, we're making significant progress. 

**Ben WS**  
If this presentation goes well, at our next meeting we could go down a level of detail and step through a realistic and authentic use case around consent. But today, I'll run at quite a high level just to introduce the concepts I think are required to decide whether a data transfer is valid. 

## TOPIC: Need to Know (Slide 3)
**Ben WS**  
I'm imagining that there's an Agent (or system), which I'll call the Redistribution Agent, buried deep within a bank that wants to redistribute data. It's going to need to surface these three pieces of information: the user who wants to execute the distribution permission; the identity of the recipient; and the identity of the asset that's being transferred.

**Mark**  
There may be another use case that restricts the recipient's use of the data. Here it's simply permission to distribute.

**Ben WS**  
Mark, you raise a very good point and have let me off too lightly. I was trying to simplify the use case. But you're right. For a properly comprehensive compliance scenario, we would need to know what we can allow the recipient to do with the data.

**Mark** 
Those restrictions could be tightly or loosely coupled.

## TOPIC: The Request (Slide 4)

**Ben WS**  
We can package up the three data points in a request -  a Request Policy. It contains a single permission that has the action "Distribute"; uses the recipient constraint to specify the receiver; and uses the target property to specify the asset to be transferred. And it gives us the identity of user wishing to make the transfer.

**Ben WS**  
So the Redistribution Agent hits the Validity Service with this request. The Validity Service then requests compliant permissions from the Compliance Service. It's saying to the Compliance Service: I've had this request - are there any permissions that allow the distribution of this asset by this user? 

## TOPIC: The Compliance Test (Slide 5)

**Ben WS**  
The Compliance Service comes back and says: OK, I can find two permissions that would allow this distribution. (This I'm now calling it now a Compliance Test.) 

**Ben WS**  
The first permission is a really simple one. It just says you're allowed to distribute this asset without duties or constraints. It's a dream of a **Mark**et data license. The second permission has a consent and a disclaimer duty. 

**Ben WS**  
So, the Validity Service must now check whether these permissions are valid. (This I call the Validity Test.) The permissions can only be executed if they are valid. At our last meeting, we had a look at a state diagram for permissions.This shows the the states that a permission can be in.

**Ben WS**  
It starts in an Inactive state. If it meets the activation condition - often a temporal constraint - it becomes Active. If it's part of an Agreement policy, effectively supported by a license between a data provider and a data consumer, then it goes into the Invalid state. To reach the Valid state it must pass the Validity Test: are all the duties associated with this permission fulfilled and the constraints satisfied. The rest of this presentation explores how we can check this. 

## TOPIC: The Validity Test I (Slide 6)

**Ben WS**  
The validity test for P1 is trivial. There are no duties and no constraints. It is therefore a valid permission. The validity service can respond to the request from the redistribution agent saying: P1 is a permission under which you can do that distribution, and it's valid, so you can go ahead and distribute the asset. It's a compliant redistribution. 

## TOPIC: The Validity Test II (Slide 7)

**Ben WS**  
The case of P2 is more complex because it's got duties associated with it. With P2, we have to check that the consent and disclaimer duties are not in the Unfulfilled state. Again, there is a state diagram that describes the deontic state of a duty. It can be inactive, then, when it passes an activation condition, it goes into the Unfulfilled state. When it's fulfilled (i.e. the Action descrbed by the duty is successfully executed), the duty goes into the Fulfilled state. 

**Ben WS**  
To reach that state, if it's a disclaimer duty, you have to attach the disclaimer to the transfer. If it's a consent duty, you have to check that the consent for this distribution to Black Rock is in place or else reques it. 

**Ben WS**  
How then does the Validity Service decide what is the state of the permission itself? It's not some all seeing eye; it doesn't do much - all it does is make validity checks. 

**Ben WS**  
So, it has to do is call out agents operating in the bank's infrastructure to make sure that these duties have been fulfilled. In order to be able to do that it needs to know which agent to to ask. And  it can do this because the agents have to register their capabilities with the Validity Service.

## TOPIC: Agent Registration (Slide 8)

**Ben WS**  
Here are two examples. Agent A1 knows how to fulfill disclaimer duties. If you tell it to stick a disclaimer on a transfer - that's what it will do. That's its job. So it advertises itself as having the ability to enforce disclaimer duties. 

**Ben WS**  
The second agent, A2, knows how to fulfill consent duties. This agent might not exist in the bank's infrastructure but in that of the exchange - or with a licensing service provider like Data BP. In the context of exchange data, consents are often decided not within the bank but by the data originator. This agent advertises the fact that it can check and request consent duties.

**Ben WS**  
These capability descriptions rely  on the Market Data Profile and have the same level of expressivity. So whatever we can express in a policy, we can express in these capabilities. So now the Validity Service knows which agents to ask. 

## TOPIC: Agent Requests (Slide 9)

**Ben WS**  
And again, I'm using a request policy to make the enquiry. The Validity Service is using a Request Policy to say: I've got this duty here at the moment that, as far as I know, is unfulfilled. It's an attached disclaimer duty. Will you please attach this disclaimer and come back to me and confirm it's been done. 

## TOPIC: Agent Responses (Slide 10)

**Ben WS**  
A1 fulfills the duty and comes back with an Agreement Policy stating that this duty is now in a fulfilled state. So the validity service knows that the Duty has been fulfilled and that's now part of its calculation as to whether the distribution permission is valid. 

## TOPIC: Which Agent?

**Nigel**  
I had a question about the consent duties. If you can obtain consents from multiple entities, how do you indicate on behalf of which entities this particular agent can provide consents?

**Ben WS**  
That's a really good question. Luckily, I think I know the answer. The consent duty has a Subject and an Object, both of which specify Parties. The former must provide the consent to the latter. We can use exactly the same mechanism in the capability description. An Agent can say: I can handle consents from the CME.

**Nigel**  
Effectively, you advertise the list of parties for whom you are competent to provide consents while the governing permission indicates from whom the consent is required.

**Ben WS**  
Yes. 

**Caspar**  
The same example would work for obtaining consent to use, for example, a third-party calculation agent. We already capture the same Subjects and Objects in the contracts. 

## TOPIC: Asynchronous Responses

**Caspar**  
I think we can orientate this in a slightly different way if we deal with post facto validity checking. Some of these approval process can take quite a long time. I can see two models. One where the Validity Service can delegate through these agents. And a second, where you could have a profile for a particular desk or business unit. They would have a suite of agents that would be bound to fulfill these duties and either report synchronously or after the fact.

**Caspar**  
These agents are going to need to have their activities recorded as provenance for any post-facto validity check. And that's a different type of response.

**Ben WS**  
Thanks **Caspar** - that's two really important points. My example has been synchronous request/response. I wanted to simplify it. In some work that you and I did previously, we introduced the notion of an agent being able to say: don't worry, assume that this is fulfilled, and I will provide evidence later. The calls become asynchronous, and we're effectively checking validity post facto. 

**Ben WS**  
That takes us to your second point, which is that agents should be generating provenance information about the activities that they've taken. 

**Ben WS**  
The model I shown is ex ante: we're checking validity before allowing the transfer to happen. But the model is certainly flexible enough to say okay, that's too expensive, we can loosen it and just say, with some agents, that we'll assume that you're doing this correctly, and we're going to check the the provenance information you create later to ensure this was a valid transfer. And if it wasn't, we'll flag it.

**Caspar**  
Yes, and also I think these requests will be idempotent, so we have some resiliency there too. Would they all be?

**Nigel**  
Not all duties. It may depend what the duties are. If for example, the duty is to make a payment of some kind. That's not an operation you want to repeat multiple times!

**Ben WS**  
But the Validity Service is delegating responsibility. So when it's calling an agent, all it's saying is give me the status of this duty. If it's a payment duty, it's just checking that the payment has been made.

**Nigel**  
That makes sense, and will probably work for most cases. But I'm wondering if there are cases where this is transactional. Pay by use?

**Ben WS**  
I'm hoping that the transactional nature of some interactions can be hidden behind the facade of an agent, so that the Validity Service doesn't care. Then all of these interactions can be indempotent. Maybe that should  be a design criteria for us going forward?

**Nigel**  
If you're going to do it that way, then this has to be explicit in terms of how agents need to behave. It certainly simplifies this part of the interface.

**Ben WS** 
Yes, it is all a matter of where we put the complexity.

**Nigel**  
Yes, it doesn't might magically disappear.

## TOPIC: Are These Really Policies? (Slide 10)

**Ben WS**  
Finally looping back to the use of requests and agreements in these interactions between these components. I have an intuition that I'm using them in the right way. But I also feel like I'm getting too much for free. I can persuade myself either way. Did anyone feel like I was cheating?

**Nigel**  
My one concern there is allowing any concepts covered in the standard into these interactions. Does that ever have side effects? Or do we have to be explicit about what you can and can't put into a request.

**Ben WS**  
So the semantics of policies are defined fairly tightly both by ODRL central and our profile: both what is allowed in a policy and its structure. I'm not in any way bending those rules. I'm just wondering if I'm bending the spirit of the law by saying I can use a Policy to send a Request to an Agent. 

**Mark**  
Traditionally we think of ODRL as expressing either an Offer (i.e. a potential arrangement) or an Agreeement backed by a contract between two parties. These responses do look like an agreement between two parties even if they're not backed by a physical contract. The spirit matches. So then there's the request. Is that like a the party that is not the content originator making an offer? 

**Nigel**  
An invitation to treat as it were?

**Mark**  
Yes. I'm trying just trying to see how the requests fit into the spirit of ODRL. It's like someone coming to a data provider and saying: can you offer me this?

**Ben WS**  
I see that pattern appearing a lot. So if you had a trading desk that wants to create some indices and wants to ask their **Mark**et data administrators: can I do this? They're goint to make a request: I want a permission to derive indices over these datasets. Then the **Mark**et data managers can see if there are any agreements or offers in place.

**Mark**  
And if not, can we construct one, a request, that we propose to a data provider.

**Ben WS**  
Yes.

**Pavel**  
And I think now we are basically back to the original picture of the policy types you presented at the beginning. A request and offer differ becuase the offer may include much more detail but include what I requested. 

**Aleksa**
I think this this is in line with what we discussed before. **Caspar** raised some good points about the asynchronicity of these calls. 

## TOPIC: Too Many Answers?

**Aleksa** 
It may be worth considering the possibility that multiple agents could deliver decisions that are at odds with each other if they are fully distributed.

**Ben WS**  
My simple answer to that would be so long as one of them tells me that the duty is fulfilled, I can go with that.  

**Aleksa**
Yes. Intersting to see in your example that there were two permissions compliant with the request but one is all I need. Perhaps that will help drive some efficiencies later.

**Ben WS**  
Yeah, in all the possible combinations. I only need one valid permission to do what I need to do.

## TOPIC: Migration
**Adam**  
As you're walking through this, and because I deal with migrations every day, I'm picturing this state of the industry when there are a few providers at first who are supplying these digital licenses. And there are lots of providers who aren't.  So you've got this bifurcated process. 

**Adam**  
So you'll still have your **Mark**et data administrators plugging into some system. If I'm a bank, my ticker plant is going to be polling the electronic providers on some batch basis, probably a nightly job, for contract changes and things like that.

**Adam**  
And then there's probably still some kind of IPA process that validates these changes. lf I'm a provider and I change pricing, it's like a corporate action, you don't automatically affect the price change. 

