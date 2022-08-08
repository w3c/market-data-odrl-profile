## TOPIC: Minutes from Last Week

**Ben WS**  
Are there any objections to the minutes of the last meeting? [No]

Does anyone object to the meeting being recorded to help generate the minutes? [No]

## TOPIC: Actions from Last Week

**Ben WS**  
Moving to the action items. We need to plan for WFIC.

I know GS, AWS, and Refinitiv are looking to demonstrate machine readable rights passing through Amazon Data Exchange (ADX) to then be enforced to control redistribution. 

## TOPIC: WFIC

**Caspar**  
Yes, this will follow a demonstration of GS's internal pipelining of data received through ADX.

**Ben WS**  
Nigel, I had a conversation with Michelle about having a non-technical session presenting the work of the community group alongside a more technical demo of automated access control. Does that reflect your understanding?

**Nigel**  
Yes, still interested in those two aspects. I'm working with Simon at GS on what's actually going to be in the WFIC tech track. One of the things we're interested in is a piece about modelling a market data contract using ODRL - a few examples of people actually doing that.

We also need to introduce some teasers into the main event to drive people to join the tech track. Something short and punchy.

**Ben WS**  
Mark, I'm very keen that we integrate data BP into some of these demos because you're the access point for exchanges.

**Mark**  
We'd like to have the content originator participate. To engage them, we probably need something a little more specific about the objective of each presentation. Can we get a paragraph for each demo?

**Ben WS**  
I think there are four things that we're looking to prove out at the moment:
1. the enforcement of usage rights especially around redistribution - duties like consent notification, attribution, and on
2. attribute-based access control - what attributes do we need to pull from a license to check at access-control time
3. the passing of machine readable rights through cloud data exchanges and into consumer systems
4. automating the creation of the content segmentations required by vendors

Is there anything you'd want to add to the list?

**Nigel**  
I think that's quite a realistic scope.

**Mark**  
So in terms of meeting cadence, are we going to organise weekly sessions that interested parties can join?

**Ben WS**  
We've got meeting inflation! Perhaps we should focus our pattern book and reference architecture meetings on deliverables for WFIC.

**Mark**  
OK, so if there were some specific exchanges that wanted to learn more I could invite them to next week's pattern book meeting.

**Ben WS**  
Geoff, is there anything you want to add from the LSEG perspective?

**Geoff** 
If we are looking to get an exchange involved, I think we'd be happy to be considered.

**Ben WS**  
That's fantastic.

**Ben WS**  
Laura, will you be going?

**Laura**  
Yes, I will, along with Trisha and Patricia. So the three of us will be there. 

**Ben WS**  
Fabulous. Is there anything you'd like to speak to at WFIC?

**Laura**  
I'd certainly be happy to bring a licensing practitioner point of view to a panel. 

On a side note, Patricia has taken over our exchange data and exchange relationship management piece. So if we were focusing on moving exchange data around, she might also be keen to join.

**Ben WS**  
Right, moving on from with WIFC. I wanted to briefly talk about two things that we've recently covered in the pattern book:
1. controls and systems
2. white labeling

## TOPIC: Controls & Systems

**Ben WS**  
So to controls and systems.

We've defined two levels of access control: a Closed User Group, in which everybody who has access to the data must be authorized and authenticated; and a Restricted User Group, in which anybody who accesses the data needs only to be identified - so a much a much looser control. 

These can be specified using the controls constraint. 

But line-of-sight also comes into play. This is especially important for vendors. It's often important to specify who is actually providing the access control. So we can add that system provider into the controls constraint. 

It can also be important to know who is controlling the display device. So we can also add a system provided constraint on the Display action. A vendor terminal can then be modeled simply by saying that the both the access control system and the display device is provided by the vendor. 

There's one final constraint that plays a role here: the data host, i.e. who actually stores the data. This plays a role in both web hosting and white labeling, as we'll discus later.

How does this sit with people. Is there something missing?

**Nigel**  
The hosting constraint comes up in in the context of cloud. We certainly have some venues that require notification if you're going to be cloud hosted.

**Caspar**  
Couldn't controls also be modeled as a duties?

**Ben WS**  
Yes. But I'm modeling them as a constraints. So that it's a fact about the world. 

If we were to model them as a duties, they would be actions that somebody must take.

**Caspar**  
So it is simply baked into the licensing world. OK.

## TOPIC: White Labeling

**Ben WS**  
Moving on to white labeling: so the key definition I've used is that white labeling is a form of third-party distribution, where a provider, or, in this instance, a calculation agent or analytics provider, derives a product from an originators data and then allows it to be branded by an external party as if it were its own. 

Does that capture the core idea of white labeling?

**Mark**  
So, just to be clear, how many parties are in this definition? Are there three of four? Is the calculation agent working on behalf of a provider or are they one-in-the-same?

**Ben WS**  
The same.

**Mark**  
OK, so in this instance, the provider is the calculation agent.

**Laura**  
So would this cover the case of Fidelity using an index provider as a calculation agent to create indices?

**Ben WS**  
The key the key distinction here is who owns the IP. If you told the calculation agent how to do the calculation, and simply used them as some qdditional compute, then they'd just be acting as a service facilitator and it wouldn't be white labeling. But if it was their IP, i.e. they had designed the index, and you were branding it as a Fidelity index, then yes, that would be white labeling.

**Laura**  
That makes sense.

**Nigel**  
The context in which I'm most familiar with this is where you see it in electronic trading with platforms like Fidessa or GL Trade. They offer a technology platform for firms that want to offer trading capabilities to their clients. Normally there'd be an integrated market data offering in there as well. The platform is branded by the firm but the execution is performed by technology provider.

You'd then effectively get a white labeling of the market data feeds into into that environment.

**Ben WS**  
One of the key questions for me is whether white labeling is a form of distribution? I've defined it to be a subclass of distribution: a distribution where the person that you're distributing it to is going to present the data as if it were their own.

**Nigel**  
Yep. I think it's a type of distribution.

**Ben WS**  
Now, I came up with some worked examples just to try and test the idea.

**Ben WS**  
This is an example where our calculation agent gets from an exchange the permission to do derivations for the purposes of creating a traded product. These derivations are irreversible and non-substitutive. 

Then we have a next-policy duty, which then controls what the calculation agent can do with those derivations. The exchange allows them to be white labelled. 

Because the derivations are irreversible and non-substitutive, there are no further restrictions on this white-labeling.

But it seems to me that quite often with white labeling, the derived data is neither irreversible nor non-substitutive. Here's a question that has been puzzling me: are CFDs irreversible and non-substitutive derivations? I doubt it. I think the same goes for a lot of those leveraged traded products.

When I look at market data licenses, often there's a little bit of talk about white labeling, with a little impact, but the minute they come to CFDs and those other leveraged traded products, suddenly there is a lot of control coming through the license. 

Is that because the CFDs can be used to substitute for the underlying assets?

**Nigel**  
I think they're also a commonly traded product. And I think the data providers want some way of claiming a share of the revenue that's being generated.

**Ben WS**  
So with things like CFDs, the licenses are a lot more controlling. Now the originator's next-policy only allows the calculation agent to offer their customers a display permission. Furthermore, they must provide a closed-user group and the display technology. So effectively the calculation agent is providing a branded platform.

This is pretty tightly controlled.

**Ben WS**  
How does this interpretation sit with people?

**Nigel**  
I think you've modeled the cases I'm aware of Ben so that looks hopeful.

**Ben WS**  
I think it can stand as a first iteration.

**Nigel**  
Yeah, I think it works. I mean, structurally, it seems reasonable that this is a specialized form of distribution. So I think you've put it in the hierarchy in the right place. And you appear to have something that's expressive enough to describe the scenarios I can think of. So, yeah, that's kind of where you want to be, isn't it.

