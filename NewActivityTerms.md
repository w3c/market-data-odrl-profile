# New Activity Terms
A list of activity terms (actions and purposes) found in market data licenses


**Access** | - 
----------------|------------
Data Set Type | 
Context | 
Note | We always tie access to an Action. Perhaps this is just `md:Use`


**View** | -    
----------------|------------
Data Set Type | Exchange Data
Context | 
Note | Same as `md:Display` action


**Download** | -    
----------------|------------
Data Set Type | 
Context | 
Note | 


**Print** | -    
----------------|------------
Data Set Type | 
Context | 
Note | In the ODRL Common Vocabulary: [Print](https://www.w3.org/TR/odrl-vocab/#term-print)


**Open and print** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Same as [Print](https://www.w3.org/TR/odrl-vocab/#term-print) above?


**Store** | -    
----------------|------------
Data Set Type | Exchange Data
Context | 
Note | Captured as `md:Store` action


**Copy** | -    
----------------|------------
Data Set Type | 
Context | 
Note | In the ODRL Common Vocabulary: [Reproduce](https://www.w3.org/TR/odrl-vocab/#term-reproduce)


**Reproduce** | -    
----------------|------------
Data Set Type | 
Context | 
Note | In the ODRL Common Vocabulary: [Reproduce](https://www.w3.org/TR/odrl-vocab/#term-reproduce)


**Reformat** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Same as [Transform](https://www.w3.org/TR/odrl-vocab/#term-transform) in the ODRL Common Vocabulary?


**Modify** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Same as `md:Derive` action?

**Create derivative works** | -    
----------------|------------
Data Set Type | Exchange Data
Context | 
Note | Same as `md:Derive` action


**Install** | -    
----------------|------------
Data Set Type | 
Context | 
Note | In the ODRL Common Vocabulary: [Install](https://www.w3.org/TR/odrl-vocab/#term-install)


**Transmit** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Same as `md:Distribute` action - can be qualified by a 'md:reciepient` constraint.


**Redistribute** | -    
----------------|------------
Data Set Type | Exchange Data
Context | Frequently used to indicate distribution to an external party.
Note | Could be modelled as a `md:Distribute` action with an `md:ExternalParty` value for the `md:recipient` constraint.
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
Note | We use the `md:displayType` constraint to distiguish between individual display (`md:Device`) and group display (`md:Wallboard`). But this may not capture the public.
Note | We also use the `md:controls` constraint to require some level of access control. Does the lack of it give us the public?


**Use the content through the internet** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Is this webhosting?


**Performing analytics** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Covered by the `md:Derive` action?


**Creating internal apps** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Covered by the `md:Non-Display` action?


**Transfer** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Same as the md:Distribute action?


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
Note | Is this an Action or a Constraint on the Asset?


**Merge** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Is this an Action or a Constraint on the Asset?


**Quote or paraphrase** | -    
----------------|------------
Data Set Type | 
Context | 
Note | 


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
Note | Effectively we treat marketing as a 'md:purpose' constraint on an action.


**Sell or license** | -    
----------------|------------
Data Set Type | 
Context | 
Note | We presently model the selling of data as a compensation duty on a permission. But I'm unclear how we could prohibit it without its own action.


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
Note | Same as `md:Derive` action?



**Adapt** | -    
----------------|------------
Data Set Type | 
Context | 
Note | Same as `md:Derive` action?


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


