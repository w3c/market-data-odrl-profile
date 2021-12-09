# New Activity Terms
A list of action terms found in market data licenses


**Access** | - 
----------------|------------
Data Type | 
Context | 
Note | 


**View** | -    
----------------|------------
Data Type | Exchange Data
Context | 
Note | Same as `md:Display` action


**Download** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Print** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Store** | -    
----------------|------------
Data Type | Exchange Data
Context | 
Note | Captured as `md:Store` action


**Copy** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Reformat** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Modify** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Create derivative works** | -    
----------------|------------
Data Type | Exchange Data
Context | 
Note | Same as `md:Derive` action


**Install** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Transmit** | -    
----------------|------------
Data Type | 
Context | 
Note | Same as `md:Distribute` action - can be qualified by a 'md:reciepient` constraint.


**Redistribute** | -    
----------------|------------
Data Type | Exchange Data
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
Data Type | Exchange Data
Context | 
Note | We use the `md:displayType` constraint to distiguish between individual display (`md:Device`) and group display (`md:Wallboard`). But this may not capture the public.
Note | We also use the `md:controls` constraint to require some level of access control. Does the lack of it give us the public?


**Use the content through the internet** | -    
----------------|------------
Data Type | 
Context | 
Note | Is this webhosting?


**Performing analytics** | -    
----------------|------------
Data Type | 
Context | 
Note | Covered by the `md:Derive` action?


**Creating internal apps** | -    
----------------|------------
Data Type | 
Context | 
Note | Covered by the `md:Non-Display` action?


**Transfer** | -    
----------------|------------
Data Type | 
Context | 
Note | Same as the md:Distribute action?


**Reproduce** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Decrypt** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Decompile** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Disaggregate** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Quote or paraphrase** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Open and print** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Merge** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Publish** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Marketing or promotion** | -    
----------------|------------
Data Type | 
Context | 
Note | We treat this not as an action itself, but as the purpose for which an action (e.g. `md:Display` or `md:Distribute`) is taken. 
Note | Effectively we treat marketing as a 'md:purpose' constraint on an action.


**Sell or license** | -    
----------------|------------
Data Type | 
Context | 
Note | We presently model the selling of data as a compensation duty on a permission. But I'm unclear how we could prohibit it without its own action.


**Disassembled** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Hyperlink** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Verify** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Validate** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Alter** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Adapt** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Translate** | -    
----------------|------------
Data Type | 
Context | 
Note | 


**Administer** | -    
----------------|------------
Data Type | 
Context | 
Note | 


