### Ben WS  
Any objections to recording the meeting to generate the minutes? [No objections]

### Michelle  
Any objections to the record of last month's meeting? [No objections]

### Laura  
Given that this automated transcription will be very verbose, would it be a good idea to have one person note any actions arising? We could bring someone along to the meeting to do this.

### Nigel  
I think that is a good idea to write. If we can find someone who has a little bit of context around this and is prepared to sit in on the calls and take notes, because that would help immensely in terms of getting the stuff done and keeping the working group focused on what they're supposed to be focused on.

### Michelle  
Perhaps we could share this task across the firms.

**ACTION: Laura to suggest a candidate for next month's meeting.**

**TOPIC: Publication of the standard**

### Ben WS  
I have a call almost immediately after this meeting with the W3C to arrange publication. So it should happen this week.

### Nigel  
Will the W3C publicise it in any way?

### Ben WS  
No. We'll have to handle any publicity.

### Michelle  
Okay, perhaps we could jump to that point. 

**TOPIC: Publicity**

### Mark  
 I did just send the group the wording of the proposed LinkedIn announcement. Chime in if you have any comments or concerns.

### Michelle  
When are we looking to publish it? When do you need feedback by?

### Mark  
If we're going to publish this week, we could send sent the announcement early next week. 

### Michelle  
OK - get comments back by the end of this week. You'll post on LinkedIn and then we just need to share it.

**TOPIC: Beyond Market Data**

### Marthe  
I discussed with some people at Amazon Data Exchange what kind of licenses we see. There's no  specific agreement that covers alternative data. But although each subscriber is drafting a contract, they're often very similar. So I think we have similar patterns rather than just one type of license. 

My colleagues are going to try to send me some examples that I could share.

When I get those examples, should I just share them with everyone or present them at the next meeting? 

### Ben WS  
Best share them on the public mailing list.

### Michelle  
**TOPIC: Patterns Book. Mark, Ben, do you want to update us on how the pattern book meeting went?**

### Mark  
We're going to show you the kind of the pattern approach that we're putting together. We spent most of the time working on a specific use case. Ben has ported that over into a draft pattern.

The goal will to describe each pattern in four sections: a description; a definition; a code example; and then a validation script using SHACL. 

We'll continue to meet in the off fortnight for the foreseeable future to build out the document, adding use cases one by one.

**ACTION: Mark to setup regular monthly pattern-book meeting.**

### Ben WS  
[Describes pattern](https://w3c.github.io/market-data-odrl-profile/patterns.html#attribution-duty)

### Nigel  
There's another validation use case: as a consumer of an ODRL document from a third-party, you might want to check that its a valid document using some some suitable standalone tool.

### Laura  
Just to clarify: you'd want to validate a third-party ODRL license to make sure that it's following the rules.

### Ben WS  
**TOPIC: Beyond Market Data**

### Michelle  
Laura, Marthe, and myself will have a an interim session to discuss this and feed back to the group. But would it be worth taking a few minutes now as it raises quite an interesting question: a lot of relevant licenses are  proprietary.

Can we extract from them sentences that describe the same thing? So as an example, for derived data, I can just take public agreements that we can all access, like exchange agreements, and see things like: new original works, second generation products, originally computed figures. There are all sorts of different descriptions of similar things. 

I'm starting to collect similar types of descriptions from non-exchange agreements as well. Perhaps doing this will help us add color to the language without disclosing proprietary information.

### Nigel  
To identify underlying concepts which occur in in the different kinds of contracts?

### Michelle  
Especially when there's sort of nuances or variations on similar themes.

### Laura  
Yes, I'm willing to go through some licenses and contribute some examples. Even if it's manually right now, I'm trying to make this stuff more visible to the people who use the data downstream.

Because one of the challenges in our industry is having the license restrictions go with the data. So now, with all the technologies involved, it's difficult. Things just proliferate. So we need to be able to remind folks in a way that there are restrictions around these use cases. 

### Michelle  
Yeah, it's quite surprising when you start to do it. I see a lot of it but it still surprises me some of the different variations. Is there anybody from anywhere else who could join us? That might be able to sort of pick up some information as well? 

### Caspar  
I can ask.

### Ben WS  
Elizabeth P said she'd like to join such a conversation.

### Michelle  
Also we could discuss what alternative data is and what othe categories of data there are. 

Alternative data is just one type of data really, and when you start to break it down, you could probably classify some existing market data as alternative data as well. It's just the way it's procured and the fact that is not necessarily from a mainstream vendor. So I think it would be good to have a session with a few people from different houses to give us a bit of variety there and talk about what the different categories are, and maybe we can categorize it.

### Ben WS  
That would be really useful.

### Nigel  
I think it would be a very good idea, because I think the real problem with alternative data is it isn't actually a concept. It's an anti concept. It's data that doesn't fit anywhere else. So it's very hard to codify rules around stuff that doesn't fit the pattern. That's not a good starting point for a definition. 

So I think what you need to do probably is probe around in that space and identify underlying collections of data that you might be able to treat as things and then I think we've got a much better chance of making some progress in terms of picking out those concepts and actually extending the model in some way.

### Michelle  
Yeah, and we can perhaps define concepts under each one of those categories, but we'll try and keep them broad, because I think, you know, we've got like exchanging real time data versus research or publications and things like that. It doesn't need to be too many categories. Okay, we'll I'll set up that group. I'll put an email out to everybody and see if there are any, any other houses that would be willing to participate.

**ACTION:  Michelle to set up meeting to discuss definitions of and licensing patterns in data beyong exchange data.**

**TOPIC: Reference Architecture**

### Caspar  
I caught up with ### Nigel and Alexa to discuss the broad approach. ### Nigel's been doing doing some work internally looking at this and basically kind of nailed down what the actual deliverable here is.

I think it's worth at least initially keeping this really quite high level. As we were doing, We're doing a functional decomposition to identify roles responsibilities. 

The concern I have is that the scope should cover the supply chain. So this is a reference architecture that spans everything from source to sink: exchanges, data providers/carriers, and consumers. 

When I started looking at the existing systems we have internally and breaking those down what became apparent is we we use them in quite different ways depending on which hat we're wearing. And there seemed to be quite a good fit with the notion of party roles.

I think it is probably a really good idea to try and engage with the carriers and the exchanges. And even service providers to see see how they fit into this picture. 

Then in broader terms we discussed guidance around the reference architecture leading towards easy integration with existing systems. And overall, there should be an evolutionary path for reference architecture adoption. 

Perhaps the path forward with this is to look at entitlements enforcement, and how that could be. How a policy store could control that as an overlay on top of existing firm systems before considering usage rights. 

### Nigel  
My sense is it's fairly early days at the moment on this but I tend to agree with Casper that we do need to take account of the different roles. A lot of what I've been looking at has been from a consumer-centric perspective. So I have a good view of what the actors are in that and the interactions between the various functional elements of a reference architecture but from a supply chain point of view, I have much less visibility into what the process looks like. If you are a data vendor in particular. We do some origination so we've got some ideas around that side of things as well. But it would be useful there I think, to have some input from people who are trying to do this on the exchange side, just to make sure that we've got the right the right objects in our data model and that we have the right concepts. 

We understand how the objects interact with one another - what information they need to exchange - and we can get this into a sort of block diagram structure that everyone can understand that explains effectively what the interfaces between the objects are, what information gets exchanged, what kind of queries you can do from one component to another. And then once you've got the abstract architecture, you can get into deciding okay, how is a physical implementation of this going to work. 

### Caspar  
I think that this necessarily needs to be top down. But as we get more towards  implementation details, discussions around around state are going to become really important. 

In terms of keeping everyone engaged and ensuring that we we consider all the parties in the supply chain, we can make this high level functional decomposition driven from a data requirement perspective. You can look at this in terms of, say, the policy. So what kind of data does it need to make any one of these decisions, and then map that over to the roles and responsibilities of existing systems. 

I'm keen to see if there's kind of generic patterns so that all consumers have a similar set of concerns. Whether it's an intermediate bank that's actually passing it on or whether it's a carrier vendor. And then similarly, are there patterns, say when we're structuring a product as a producer, is that somehow similar to some of the patterns that exchanges might see.

### Ben WS  
I was wondering Casper, if you've got a clear answer to what we should be looking to standardize and what we leave to be implementation specific. 

### Caspar  
Yep. So we, you know, systems across the supply chain must speak the same language that's, that's a kind of a baseline. We are able to express quite a lot of complexity using ODRL. I think a lot of what we would want to communicate across the supply chain is kind of already available within the spec in various places. 

And anything around reporting metering, stuff like this, it's kind of Provo-Oe provenance ontology is already baked into adrl. We're extending some of those base classes such as entity in various places. There's a natural fit there. It's rather nice in the fact that there's a non ontological form that will set quite happily over existing relational databases, things like that. So for firms looking to kind of get a front foot on on implementing this or anyone sort of building or retrofitting existing systems today, we should be able to provide some early guidance, how you can start sort of building systems that would, you know, would work in an OD RL ecosystem. It's, I think it's it's mainly work out the data flow. Find the correct ontologies to express that in and then and then start defining the API's for the communication between those parties. Taking our existing systems as a as a frame of reference, I think is a great starting point, but it shouldn't mandate that anyone actually has to have those systems. It's literally a bunch of interfaces. I think, is the the main sort of deliverable here.

### Ben WS  
Okay, that makes sense.

### Nigel  
Yeah, I agree.

### Caspar  
And so, basically, I think next next steps would be ### Nigel, myself and Alexa to continue the discussion that we've been having so far. But as a kind of really important point is to make contacts and exchanges, service providers carriers, anyone, anyone else who could provide some color on the current workflow? And you know, how they see themselves sitting in this

### Mark  
Casper, if I was talking to an exchange, how would I give them that? What's the elevator pitch that says, Hey, you want to come participate in this conversation?

### Caspar  
We'll do the work for you. Tell us what you need.

### Nigel  
Well, part of it is we're trying to define here a reference architecture and that might influence the shape of future products from various parties. And it is your duty to influence that and help shape that architecture so that it most closely meets your requirements. 

### Michelle  
Your clients are interested in having that conversation.

### Ben WS  
I think what you've described ### Nigel, is a marmite benefit. Some exchanges might love the ability to do that. But some exchanges might be concerned that someone is designing a reference architecture that could influence their product creation processes.

### Caspar  
That's that's also a reason to join them, isn't it?

### Nigel  
It makes it clear. This is a conversation you probably want to be part of.

### Michelle  
So you're going to put that elevator pitch out to the public group, Casper, so that we can try and encourage some of the members who fit into those categories to join us and

### Caspar  
That's a great starting point. Yeah.

### Michelle  
**ACTION: ### Caspar to invite more members of the CG to join the reference architecture discussion.

**TOPIC: Errata**

### Ben WS  
**RESOLUTION: Accept updates to the Subject definitions as defined in [Issue 29](https://github.com/w3c/market-data-odrl-profile/issues/29)**

**RESOLUTION: Accept updates to the Historic data definitions as defined in [Issue 30](https://github.com/w3c/market-data-odrl-profile/issues/30)**

### Nigel  
Data sets could have both temporal and timeliness-of-delivery constraints because you could have historical data that was recorded from delayed data. And you could have historical data that's been recorded from real time data, for example. 

Transcribed by https://otter.ai
