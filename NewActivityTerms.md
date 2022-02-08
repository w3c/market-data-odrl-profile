# New Activity Terms
A list of activity terms (actions and purposes) found in market data licenses


**Access** | - 
----------------|------------
Data Set Type | 
Context | 
Scope Note | We always tie access to an Action. If there's no further restriction on the Action allowed, perhaps this is just `md:Use`


**View** | -    
----------------|------------
Data Set Type | Exchange Data , Research Data
Context | 
Scope Note | Same as [md:Display](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#display-0-9) action


**Download** | -    
----------------|------------
Data Set Type | Exchange Data, Research Data, Alternative Data
Context | Download vs. View (on a terminal)
Scope Note | Both an action and a unit of count
Suggestion | Subclass of View?


**Print** | -    
----------------|------------
Data Set Type | Research Data
Context | 
Scope Note | Both an action and a unit of count
Note | Available as an Action in the ODRL Common Vocabulary: [odrl:Print](https://www.w3.org/TR/odrl-vocab/#term-print)
Suggestion | Subclass of View?


**Open and print** | -    
----------------|------------
Data Set Type | Research Data
Context | 
Note | Same as [odrl:Print](https://www.w3.org/TR/odrl-vocab/#term-print) above


**Store** | -    
----------------|------------
Data Set Type | Exchange Data
Context | 
Note | Captured as the [md:Store](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#store-0-9) action


**Copy** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Same as the [odrl:Reproduce](https://www.w3.org/TR/odrl-vocab/#term-reproduce) term in the ODRL Common Vocabulary?
Suggestion | New top level term? Limit scope to documents?

**Reproduce** | -    
----------------|------------
Data Set Type | 
Context | 
Scope Note | Often qualified by the [md:recipients](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#recipients-0-9) contraint (Internal/External party)
Note | In the ODRL Common Vocabulary: [odrl:Reproduce](https://www.w3.org/TR/odrl-vocab/#term-reproduce)


**Reformat** | -    
----------------|------------
Data Set Type | 
Context | 
Scope Note | A change in format, not in informational content
Note | Same as [odrl:Transform](https://www.w3.org/TR/odrl-vocab/#term-transform) in the ODRL Common Vocabulary?
Suggestion | Subclass of Reproduce


**Modify** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Same as [md:Derive](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#derive-0-9) action?


**Create derivative works** | -    
----------------|------------
Data Set Type | Exchange Data
Context | 
Scope Note | Is there an implication that these derived works will be distributed? If so, this is a linked set of permissions.
Note | Same as [md:Derive](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#derive-0-9) action


**Install** | -    
----------------|------------
Data Set Type | 
Context | 
Note | In the ODRL Common Vocabulary: [Install](https://www.w3.org/TR/odrl-vocab/#term-install)
Suggestion | Ignore for now


**Transmit** | -    
----------------|------------
Data Set Type | 
Context | 
Scope Note | Can be qualified by the [md:recipients](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#recipients-0-9) contraint (Internal/External party)
Note | Same as [md:Distribute](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#distribute-0-9) action?


**Redistribute** | -    
----------------|------------
Data Set Type | Exchange Data
Context | Frequently used to indicate distribution to an external party.
Note | Could be modelled as a [md:Distribute](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#distribute-0-9) action with an [External Party](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#external-party-0-9) value for the [md:recipients](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#recipients-0-9) constraint.
```
[]    md:action   [
                      a               md:Distribute ;
                      md:recipient    [
                                          a     md:ExternalParty ;
                                      ]
                  ] .
```

**Display publicly** | -    
-----------------------------------------------------|------------
Data Set Type | Exchange Data
Context | 
Note | We use the [md:displayTypes](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#display-types-0-9) constraint to distiguish between individual display - a [md:Device](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#device-0-9) - and group display - [md:Wallboard](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#wallboard-0-9). But this does not capture the public.
Note | We also use the [md:controls](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#controls-0-9) constraint to require some level of access control. Does the lack of access control give us the public? Probably not.
Note | The [recipients](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#recipients-0-9) constraint  feels relevant here, expecially when tied to an [External Party](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#external-party-0-9).


**Use the content through the internet** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Is this webhosting? Or widgets and mobile phone apps? Does it cover intranets? Is it where Google, for example, displays delayed equity prices?


**Performing analytics** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Covered by the [md:Derive](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#derive-0-9) action?


**Creating internal apps** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Covered by the [md:Non-Display](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#non-display) action?


**Transfer** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Is there an implication that the rights are transfered rather than the data (which would be covered by the [md:Distribute](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#distribute-0-9) action)?


**Decrypt** | -    
----------------|------------
Data Set Type | 
Context | 
Note | 


**Decompile** | -    
----------------|------------
Data Set Type | 
Context | 
Note | 


**Disaggregate** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Is this an Activity or a Constraint on the Asset?


**Merge** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Is this an Activity or a [Commingle](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#commingle-0-9) Constraint on the Asset - or a Transform?


**Quote or paraphrase** | -    
----------------|------------
Data Set Type | Research
Context | 
Note | An [amount](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#amount-0-9) constraint on the Action?


**Publish** | -    
----------------|------------
Data Set Type | 
Context | 
Note | 


**Marketing or promotion** | -    
----------------|------------
Data Set Type | 
Context | 
Note | We treat this not as an action itself, but as the purpose for which an action (e.g. `md:Display` or `md:Distribute`) is taken. 
Note | Effectively we treat marketing as a [md:purposes](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#purposes-0-9) constraint on an action.


**Sell or license** | -    
----------------|------------
Data Set Type | 
Context | 
Note | We presently model the selling of data as a compensation duty on a permission. But I'm unclear how we could prohibit it without its own action/activity.


**Disassembled** | -    
----------------|------------
Data Set Type | 
Context | 
Note | 


**Hyperlink** | -    
----------------|------------
Data Set Type | 
Context | 
Note | 


**Verify** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Same as Validate?


**Validate** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Is the context validating prices? That might be an activity used to specify a purpose.


**Alter** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Same as [md:Derive](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#derive-0-9 action) action?



**Adapt** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Same as [md:Derive](https://w3c.github.io/market-data-odrl-profile/md-odrl-profile.html#derive-0-9 action) action?


**Translate** | -    
----------------|------------
Data Set Type | 
Context | 
Note | In the ODRL Common Vocabulary: [Translate](https://www.w3.org/TR/odrl-vocab/#term-translate)


**Administer** | -    
----------------|------------
Data Set Type | 
Context | 
Note | 


