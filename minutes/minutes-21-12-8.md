
## TOPIC: Previous Actions
**Michelle** 
We were going to invite all members to a reference architecture meeting.

**Caspar**   
Ben actioned that one.

**Ben WS**   
Yes. Hopefully Refinitiv and Microsoft will be joining those discussions. But we can pick up that later in the agenda.

**Michelle**   
Next, Ben agreed to liaise with the W3C to get the draft profile published.

**Ben WS**   
It's done. It's done. It's done. 

**Michelle**   
**Mark**  was going to circulate a draft of the LinkedIn announcement, which he did. What's the plan for publishing it?

**Mark**   
It should be today. Then I'll email the community group with a link to the post. And if anybody who's wants to could reference it from their personal account, that'd be fantastic.

## TOPIC: Beyond Exchange Agreements
**Michelle**   
We had a get together in which we discussed alternative data but also the wider issue of non-exchange agreements. There are lot of other concepts there and also descriptions of existing concepts. How can we collect them given that we can't share that information or share those licenses given their commercial sensitivity? 

**Michelle**   
And so I started to put together a list of terms from those agreements. Now that we've published the first version of the standard, covering exchange data, we obviously need to start thinking about the next concepts that we need to include in the profile. 

**Michelle**   
So here are some that I just pulled out of various documents. I don't think anything's proprietary and I'd be very happy if people were to add to the list. Some of the terms you can see probably group together and can be covered under some existing terms, but I thought it might be useful to start to document them so that we could identify how we would model these.

**Ben WS**   
I think these are fantastic. It would be useful to say what kind of data these terms cover. Because I suspect something like "install" is probably not from an exchange contract. 

**Michelle**   
None of them come from exchange data actually. But I'll try and add a bit of context. 

**Michelle**   
Laura agreed that we would divide these up. Maybe one of us  look at derived data and the other at redistribution. Someone else could have a look at storage. In this way we can capture greater depth on each subject.

**Michelle**   
Do you see a lot of contracts **John** , is it something that you could perhaps add to the list?

**John**   
Derivative Works - the only thing I would do with that is to create two versions: create derivative works for internal use and create derivative works for external use.

**John**   
If this is a single tiered list, we've got to split that out, otherwise, if you can have branching logic underneath it, yes, you can create derivative works, then is it internal or external? And then branch.

**Nigel**   
And there is some support for modeling that certainly.

**Michelle**   
Okay, well as a starting point, we can start to build the library of terms. Be great, **John** , if you could add some more stuff to it as well. And if somebody from Goldman Sachs could take a look as well. That'd be great too.

**Ben WS**   
How should we share this? Should I create a document on GitHub? 

**Michelle**   
Okay, that would be perfect.

**Atiq**   
That makes sense. Since we started the journey, we're had to make decisions. But I suspect that in a year or two, we're going to make another list and going through the same process. Do we need to keep a record of the terms that we've come across and how we've modeled then. So in future, as terms come up, we know whether we've already dealt with them.

**Mark**   
Redistribute, which I think we have as distribute, is going to come up every six months. Someone's gonna say, Hey, where's redistribution? And we'll have to remember how do we did that.

**Nigel**   
I'm  going to want some sort of glossary of commonly encountered terms and how we've modeled them.

**Mark**   
A pattern, Ben.

**Ben WS**   
I think it's too low level for a pattern. But it reminds me a lot of test cases where we actually come up with these questions we want to be able to answer and then we say, how do we solve them? You know, what are the terms we use in order to answer this question?

**Nigel**   
Yeah. As we add these as examples, and once we decided what the right resolution is for each of them, we can find some way of making that navigable.

**Ben WS**   
Yeah, I'll take that as an **ACTION**.

## TOPIC: Alternative Data
**Michelle**   
I might suggest that we move this to the next call. I'll follow up with Marta about the AWS license approach. And I think Elizabeth Pritchard was also going to give us an update on the alternative data standardized paperwork from FSD. 

## TOPIC: Pattern Book
**Mark**   
So we met a fortnight ago, and split the meeting in half to talk patterns at the beginning and then reference architecture at the end. The pattern book itself, I think, is building out pretty nicely. 

**Mark**   
One thing we spent some time on was the target audience of these patterns. And I think spending a little time on that right now is a good idea. Making sure we all agree on who is going to use this document will set our direction. 

**Mark**   
One way to break this down is to ask if we are writing to a technical audience producing or consuming ODRL or for those actually creating or interpreting license agreements? 

**Mark**   
The latter don't know anything about ODRL, but these patterns would help them construct their analog agreements in a way that makes them readily expressible digitally. 

**Ben WS**   
When I originally wrote the patterns, I aimed them both at those writing adrl policies and the people who are writing code to interpret those policies. And that was, I think, quite a naive, technical approach.

**Ben WS**   
As Laura pointed out, she may well be creating these policies but she's never going to be working at this low level. She is going to be working through an application. She could imagine discussing elements of this document with her developers. But she could not imagine reading it for her own purposes. It's simply too low level. 

**Ben WS**   
So I strongly suspect that in the end this document is for a technical audience. If you are writing code to interpret an attribution duty, this is the document that tells you exactly what you will receive and what you should do with it. But it's not for **Mark** et data managers.

**Ben WS**   
I don't think it will help them.

**Mark**   
I agree. So then, how do we facilitate Laura's conversation with her developers knowing that these patterns are for her developers? What is Laura going to start with? 

**Atiq**   
In the past, we've talked about making a human readable form of all this. We talked about using SHACL to do transformations. Would we ever foresee some sort of common tool that we all start to converge around, which builds that human readable representation? The examples that we put in the pattern book could then be reviewed and validated by their **Mark** et data managers. Then we have a mechanism through which the pattern book bridges the gap from the developers through to the **Mark** et data managers.

**Ben WS**   
I think that that's a really powerful thought. And the question of whether we should standardize the human readable description of these od RL represents representations is for me an open one. And I think the reason it's open I guess it's for two reasons. If something is very uncertain, it's probably not worth standardizing because the dangerous standardizing that is that you actually block innovation. But if you're actually pretty confident about the ground you're walking on, then standardization becomes really valuable. And I don't know whether the human readable representations of these is stable ground or unstable ground at the moment, and I'd be really interested in what the people on the call think. 

**Caspar**   
I've got quite a strong opinion that we can. But only if it's the same natural language that the spec is written in. That way the patterns and the standard validate each other. You really want to be taking the context, the definition, the descriptions directly from the standard. Then it's literally putting some syntactic sugar on top to make it more palatable and rearranging the terms so that they flow like an English language sentence. 

**Caspar**   
I think where this becomes potentially thorny is if you then expand this to other natural languages. I wouldn't, though we certainly have **Mark** et data contracts written in other languages.

**Ben WS**   
Is the way around that **Caspar**  to say that if, for instance, we were dealing with French contracts, we should have a French translation of the original standard and then generate the French language representation of any particular license from that translation?

**Caspar**   
Yeah, because that way you can ensure that you're not going to drift. I definitely think it's doable. But whether we should? 

**Caspar**   
Right now, it'd be incredibly valuable to be able to answer **Mark** 's question and say: if you want to build a contract, you can come here and start actually hacking away at it and validate it. And you can have a domain expert who can look over your shoulder and say: this doesn't read properly.

**Caspar**   
And if we start building these tools, as we get deeper into implementation, it keeps the vendor managers and legal domain experts in the process.  They're able to opine, and we don't start losing people through incidental complexity. 

**Caspar**   
So I think it could be turned into a standard. I take your point that it may be fragile ground. And you don't want to block innovation elsewhere. But I think right now it would be really useful to have this just to facilitate the development of patterns, of the standard, and of SHACL validation.

**Ben WS**   
What do others think?

**Michelle**   
It depends for what purposes you want to turn it into human readable form. So if you're doing it for somebody, perhaps a vendor manager, who wants to be able to see what specifically are the policies associated with an agreement, and these have been validated, then that could be useful, 

**Michelle**   
But if it's a legal person trying to compare it against the legal agreement, I would think it would be quite challenging. So I think it depends on what you're trying to get out of the human readable version. And maybe we need to think about that.

**Mark**   
Is that something we have in ODRL? Could we have a pointer back to relevant part of the physical analog contract? That would be amazing. Do I have the right to distribute this data product? ODRL could could say yes or no. But then we're going to want to double check. We're going to want to see it with our own eyes in the contract.

