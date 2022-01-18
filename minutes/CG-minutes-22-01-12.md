## TOPIC: Previous Actions

**Ben**  
Michelle has provided a whole lot of terms from licenses that aren't public exchange licenses. She and Laura couldn't make it today, but they have an action to further contextualize these terms and to develop a taxonomy of the different types of data managed by FIs. I offered to put Michelle's new terms onto GitHub. They're there now and we'll look at them shortly. John offered to review the terms.

**Jaspal**  
I'm assuming John's has a copy.

**Ben**  
I emailed the link to the mailing list. It's https://github.com/w3c/market-data-odrl-profile/blob/gh-pages/NewActivityTerms.md

**Ben**  
Caspar, you were going to share some examples of compliance use cases.

**Caspar**  
I'll have them for the next meeting.

**Ben**  
I was going to schedule a monthly architecture meeting on the third Wednesday of the month, which I have done. And Mark, you were going to facilitate a call on compliance requirements with one of your customers. 

**Mark**  
I have started that conversation and a couple of with a couple of our clients.

## TOPIC: Beyond Market Data - New Actions & Activities

**Ben**  
Michelle has provided a set of new terms. These don't just come from the licenses controlling exchange data. 
 
### Access

**Ben**  
This is a slightly strange becuase we presuppose access before an Action can take place. I guess we need more more information on the context here. If it's access to use the data, we could apply the Use action. If it's to display the data, we could apply the Display actions. But does this "access" mean something else?

**Nigel**  
I think you're right on that.

**Ben**  
### Download, Print, Open & Print.

**Jaspal**  
Download as opposed to a view on screen. So an export.

**Ben**  
What type of data might these actions control?

**Jaspal**  
It could be any type of research service. It could be a rating service; an alternative data provider; equity research access through a terminal - or through some third party.

**Nigel**  
Bloomberg terminals.

**Jaspal**  
View versus download. That's always a contentious point. If you're restricted within your license to a certain number of downloads, exports, or views, you need to know the distinction.

**Ben**  
So this might actually be a unit of count as well? For example, you're allowed 10 downloads a month.

**Nigel**  
Could be a unit of account. But also a prohibition: view the data but not download it.

**Ben**  
Print and "open and print" - there is the ODRL common vocabulary that defines the term "Print" and several other document-centric terms. Maybe we can borrow terms from that. I assume that "print" and "open and print" mean the same thing because printing something presupposes that you can open it. 

### Store

**Ben**  
We already cover this - there's an Store action in our standard. 

 
### Copy, Reproduce, Reformat

**Ben**  
"Copy" and "reproduce" are probably the same thing.

**Jaspal**  
"Reproduce" can be for internal use or external use or both.

**Ben**  
OK - we can provide those qualifications using the recipient constraint with the values Internal Party and External Party.

 
### Reformat

**Ben**  
I think this is different from "modify" or "create derivative works". There is a "transform" term in the URL common vocabulary which is targeted at changing the format of an asset, not it's informational content. And I guess that's the concept targetted by this term "reformat". 

**Nigel**  
Yeah, I think that would be reasonable.

**Ben**  
I'm going to hold off on modify and create derivative works because there are a whole load of other terms that also seem to be very similar. So perhaps we can take them all at the same time at the end. 

**Ben**  
Install

**Ben**  
This is again covered by the ODRL common vocabulary. 

**Ben**  
Transmit

**Ben**  
I have been assuming that this is the same as a Distribute action. Effectively, you're you're transmitting information from one party to another and that that we would describe as distribute. I don't know if it has any further implications.

**Ben**  
I think we need more context on the use of this term.

**Ben**  
Redistribute 

**Ben**  
I think this is a form of Distribute, where we're saying that the recipient is an external party.

**Nigel**  
Commonly used in that way.

**Nigel**  
Would it be more correct to say in redistribution that the Distributor is not the Originator?

**Ben**  
I think that's true. But I think that the concern around redistribution is that the data is getting to a third party.

**Nigel**  
I agree that common use often means that.

**Ben**  
Display Publicly

**Ben**  
So this is a interesting one. We can constrain Display by Display Type. We have two values. The first is Device, which is a terminal or a mobile phone, that effectively displays to an individual. The second is Wallboard, which is a public display. 

**Ben**  
We can also constrain a Display permission by the access controls that are put around the display. I'm wondering whether its enough to capture the notion of public display by specifying no Access Control constraint and setting the Device to Wallboard. Or do we need an explicit concept of the Public - which we don't have now.

**Nigel**  
Many exchanges do draw a distinction between a board on a wall that's inside the licensee's building and the one that's in Times Square. It is it too crazy to say that it's like internal distribution versus external distribution. One's viewed by the licensee's employees and the other by the public.

**Nigel**  
Yes, it feels like this should be a constraint on the Recipient, but I don't think we've got a way of describing a recipient as the public.

**Ben**  
All we have at the moment are Internal or External Parties. You could say that External recipients with no Access Control implicitly means the public - but that might be a bit of a sleight of hand.

**Nigel**  
Maybe you do need to spell it out explicitly. But this does feel related to a Recipient constraint.

**Ben**  
Use the content through the internet. 

**Ben**  
What I'm wondering is whether this is the same as web hosting, which is a construct that we can model

**Jaspal**  
Probably covers other things like widgets.

**Ben**  
I had not thought of widgets in this context but they may be relevant.

**Nigel**  
Or mobile apps.

**Jaspal**  
Does this also cover intranets?

**Ben**  
Hopefully, we can make that distinction using the recipient constraint and making a distinction between Internal and External users. Because what we're trying to do is minimize the number of terms but maximize expressivity by combining them together. 

**Nigel**  
I think we need more context around using the content through the internet. Because from one point of view, it's effectively just external distribution. 

**Nigel**  
Unless there are some specific conditions on what someone can do if they're taking the data over the Internet. If so, we might need to be able to model it separately. But I don't know if we've got any use cases like that. So I don't know whether we need a special term for it. 

**Ben**  
I think we need more context. I read it as supporting the display stock prices on Google, for example.

**Ben**  
Performing analytics

**Ben**  
This is likely another of those terms that is covered by the derive action. 

**Nigel**  
Seems like a derive. 

**Ben**  
Create Internal Apps

**Ben**  
This is an activity that we've kind of ignored. I think I've ignored it under the assumption that we're working at a level of abstraction where we don't need to identify the fact you're creating an internal app because it is implicit in a Non-Display action. 

**Nigel**  
Yes, for permission to be granted you'd need to be covered by a Non-Display Permission of some kind.

**Ben**  
Transfer

**Ben**  
Again, rather like transmit and redistribute, this may be the same as a distribute action. I certainly use the terms interchangeably.

**Nigel**  
Could be. Hard to say. I mean, there's this notion that if you transfer something, you're giving up your access to it in some way. So there might be a distinction there. But I don't know. Again, it depends on the context it appears in in a contract.

**Ben**  
That's a good qualification. 

**Ben**  
Decrypt and Decompile. 

**Ben**  
That sounds like software. I'm tempted to just say it's out of scope, because we're looking at data not software. 

**Caspar**  
Decompile comes up a lot in derived data and index creation

**Ben**  
Decompiling the algorithm?

**Caspar**  
The Irreversible and Non-Substitutative constraints.

**Nigel**  
This feels more like a shrink wrap license around a piece of software with embedded data content of some kind.

**Ben**  
Disaggregate and Merge

**Ben**  
Whether you can aggregate or disaggregate information is significant to a data vendor. And the way we modeled this was not as a permission (to aggregate or disaggregate) but as a constraint put against the Asset.

**Ben**  
So this constraint effectively said this asset can or cannot be commingled with other data assets. 

**Ben**  
So that covers the merge case.

**Ben**  
And could probably cover the disaggregate case simarlarly. But should we use a Constraint on an Asset to model this, or should we be using an Action on a Permission?

**Ben**  
So rarely do you get an instruction from a data originator on merging or dissagregating that a constraint was a cheap construct to use. But if it's very common, then we should probably upgrade it to a permission. How often do you see that being explicitly stated in licenses?

**Nigel**  
I don't feel like I see that a lot.

**Nigel**  
I suspect it would be for very specialized datasets. I lean towards associating it with the Asset

**Ben**  
Quote or Paraphrase. 

**Ben**  
I guess we see this in research.

**Jaspal**  
Yes. If you want to quote data or content from a report, you need to seek permission from the vendor. Not always, but sometimes. So that's what this is referring to.

**Ben**  
Yes. We do have an Amount constraint that offers the values Substantial and Insubstantial. So effectively, we'd be modeling a quote or paraphrase as a Distribute action with an Insubstantial amount Constraint. I wonder if that is good enough.

**Nigel**  
You could also argue that a paraphrasing is a transform of the information.

**Ben**  
Or even a derivation ...

**Ben**  
Marketing or Promotion

**Ben**  
That's often a purpose constraint. And we already cover marketing as as an activity and I suspect promotion is the same as marketing for our purposes anyway. 

**Ben**  
Sell or License

**Ben**  
Until now, we've modelled selling by simply having a compensation duty on a Distribution permission. That's selling a dataset: you're allowed to distribute it and there's a payment duty associated with that. License, I guess, is something different.

**Ben**  
But if you want to prescribing the selling of data, that's not easy to say. So if we do want to use Sell as a potential prescription, we'll have to turn it into an Activity. 

**Nigel**  
Yes, you can give it away but you can't sell it perhaps. I can imagine we're gonna have to handle that case.

**Ben**  
Disassemble

**Ben**  
 I think that relates to an earlier discussion. 

**Ben**  
Hyperlink

**Ben**  
Now that is a strange and obscure one which I'm going to pass over for now. Unless **Jaspal** you say that hyperlink comes up a lot?

**Jaspal**  
I think we need to get more context. Could be a hyperlink to the source the data or content.

**Ben**  
Verify, Validate

**Ben**  
I'm not sure whether verify is the same as validate. Without context, my assumption would probably be yes. And I also wonder whether this relates to validating prices. If so, that that would be a purpose. I think we'd need to define an activity which is validating prices. 

**Nigel**  
There's often prohibitions on that. 

**Ben**  
Alter, Adapt. 

**Ben**  
These sound document-centric. So perhaps Derive is not the the answer here.

**Ben**  
And that's the list done. Thank you for the discussion. I think it was really useful.

**Mark**  
So what will we do with the synonyms of terms we already have? Is that going to be documented somehow?

**Ben**  
I would like to put the synonyms into the standard itself as examples - perhaps as scope notes.

**Nigel**  
that makes a lot of sense.

Transcribed by https://otter.ai
