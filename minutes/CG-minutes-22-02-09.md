Michelle 
I noticed we didn't have any actions defined from the last meeting. I couldn't see any in the minutes.

Ben WS  
There were no actions.

Michelle  
So today, we want to revisit the new terms. The focus of our discussion last week was on these activity terms. 

Ben WS  
So, this notion of Access. It's not something that we model directly. We presume access as part of any action. We've not added the term. I'd be interested to hear if there's any additional meaning.

Ben WS  
The new term View seemed very similar to the existing term Display.  So I've added a scope note to our definition of Display to say when a view action is permitted, use Display. We're effectively saying they're synonymous - that they mean the same thing.

Mark  
Should we have a synonyms section?

Ben WS  
Yes, it might be helpful if we created a synonyms list.

Ben WS  
Then we came to Download. We discussed its relevance to terminals. You might, or might not, be permitted to download data off a terminal. So, I thought, that downloading an asset might be to Store and Display it with a local application - and we can already express that.

Jaspal  
Yes, simple export.

Michelle
There's another use cases with client portals. So, it's quite a common thing with client portals when clients come in and use data within analytics tools that they might be allowed to view the data within the portal, but vendors might prohibit them from downloading it. 

Ben WS  
Perhaps I should move Download to a top-level action along with Distribute, Store, and Use?

Mark
it reminds me of the distinction in media between streaming services and actually owning the medium. Might ODRL have a distinction like this?

Ben WS  
I don't think ODRL has a Download action, though I take your point. You'd have thought it would have it.

Ben WS  
Moving on: Print, and Open and Print. Both seem to mean the same thing, and I think this sits under the notion of distribution. Effectively, if you print something, what you're really doing is distributing it to additional people. 

Ben WS  
We could also model the notion of Reproduce, which is to copy an asset and then supply it to a party, in a similar way. Then Print becomes a particular version of Reproduce, which is a particular version of Distribute. And that's the key concept that we're controlling here.

Jaspal  
So, the assumption is that the Print action basically is an intention to Distribute. 

Michelle  
Is Share a separate concept?

Ben WS  
I don't think so. I think it's just a form of distribution.

Ben WS  
So, my assumption has been that the intent of the licenses controlling things like printing and reproduction and so on, is not really about your personal copy, but about those you give to other people.

Michelle  
Do you see that one Laura? 

Laura  
Yeah. And I've seen that one before. They're restricted Printing because they see that as wanting to further pass along the results and so that would be a different license in their mind. So, I think that makes sense.

Laura  
What about Download though. There's the Download that an individual user does, for example, when they export data from a Bloomberg terminal that's only for their own use as a licensed terminal user. But then we have other sort of terminals where we have a license to download something and put it in an application that then others can also use. 

Ben WS  
It might simply be a case where we use a recipients constraint on the download.

Laura  
That would sound it Yeah, I think that would do it. Okay.

Ben WS  
So, to Store: we already have that in the standard. 

Ben WS  
Copy seems to be the same as the ODRL term, Reproduce. And again, I put that in the context of distribution, because again, it seemed to me that the purpose of this reproduction is to copy the assets and supply it to other parties. And then print just becomes a subclass of Reproduce. 

Ben WS  
Then there is the concept of Reformat. I read this as converting an asset into a different format either for consumption or for transfer. to third parties. So, it's not like derivation. 

Michelle 
You might have an obligation to get the format checked by the vendor.

Jaspal  
So, it should be formatted in a manner that supports the application that's going to use it. You're not changing the data itself; just the format.

Ben WS  
Yes, and I think I should add a note that says the informational content remains the same while the format changes.

Michelle 
Yes, because sometimes it says you're not allowed to tweak it and then represent it as the original data, but you can reformat it. You could cut a chart out, for example, and put it into a re research document or something like that. And you might have to source it but it because it's still the vendors proprietary information.

Caspar  
Is this like distribute versus redistribute in the sense that it should be format rather than reformat? 

Ben WS  
Yes, probably.

Jaspal  
So, we are formatting for either internal distribution or external distribution. Covered under reproduce?

Ben WS  
It does come under reproduce. So, in fact, now we can do things like you're allowed to reproduce this, but you're not allowed to reformat it. So those kinds of constructs become easy to make.

Michelle  
So, is it a subclass of reproduce? Do you think we need to be capturing any of these use cases then?

Ben WS  
Yes. I think it's the job of the patent book to say: here's a common use case and this is how you model it in ODRL.

Michelle 
But would you like some examples from licenses?

Ben WS  
Definitely!

Michelle  
So perhaps Laura, Jaspal, and I can add some context around it.

Mark  
The chart example, Michelle, I thought that was that was nice. Maybe we take the example of a raw feed that, say, Refinitiv, just puts into a standard format and redistributes as one use-case. And then the chart example. I'm just passing the same information just in a new format. But in a way it isn't. So, it's just it's a visual format instead of instead of the raw format. 

Mark D  
The chart example seems to me more of a copy action. To me, reformatting would be taking what was on a VHS tape and burning it to a DVD. You're not necessarily reformatting something to distribute it, but to consume it in a different way. 

Mark D  
I'm not bought into idea that the purpose of a reformat is for distribution necessarily. Technical concerns might make you reformat something, to use it. But the essence is that the movie is the same. It's now readable in a DVD player versus a VHS player. 

Laura  
That's the most common example. A feed comes in and we must do a certain amount of reformatting of the feed structure in order to consume it into an internal application. So that's probably for market data.

Mark D  
But if we were to then move out of the market data context? If we're receiving research in PDFs and we want to be able to edit them. Can we reformat it to be a Word document instead? I'm struggling to come up with examples of where that would apply say to data or, or other more streaming type content. Is this more of a static research type example? 

Ben WS  
Mark, I think you raise an interesting idea that which is to say, look, is the scope of this term really research documents? Or is the scope much wider and can include real time feeds? Or do we need two different terms. If I enrich the symbology - is that a reformat?

Laura  
You're changing the content. It's not reformatted. 

Caspar  
The core ODRL spec has a Transform action. And its description is used to convert the asset into a different format for consumption or transfer to a third-party system. This covers the manipulation of feeds. So, I think maybe reformat is more on the research side.

Ben WS  
So, you think there are two terms here. reformat for documents, transform for data streams?

Michelle  
We're trying to second guess the licenses here, but perhaps if we have some examples, where it might be differentiated? 

Laura  
Internally we use that the term Transform for feeds. 

Mark  
As to the agreements, it's probably best that Michelle and I get a couple examples. I'll scan ours and see if they use those terms.


