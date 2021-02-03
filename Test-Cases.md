# Test Cases
One of the key objectives of the Rights Automation for Market Data Community Group is to provide a standard, machine readable description of market data licenses so that applications can decide, on the basis of those descriptions, whether a usage is allowed or not.

The test cases listed here are the kinds of questions asked day-in, day-out of market data professionals. They are also our way of measuring progress towards that objective. Can we turn these questions into queries? Do we get the right answers?

## Internal Access to Data

**IAtD-1** - Am I entitled to access a particular date range of historical content?

- *Covered by timeliness of delivery*

---

**IAtD-2** - Can I entitle my internal developers for free?

**IAtD-4** - Can I entitle my IT Support / Market Data staff for free?

**IAtD-7** - Do I need to declare and/or pay for data utilisation within my development or UAT environement?

- *Covered under the purposes of Training, Product Development, Technical Support, and Quality Assurance - but do we need additional terms?*

---

**IAtD-9** - Can I publish a particular raw real-time/delayed/intraday/end of day data set to an application which does not provide the ability to control and report those downstream users and/or applications?

- *Covered by the Controls constraint*

---

**IAtD-10** - Am I allowed to distribute to majority owned affiliates?

**IAtD-11** - Am I allowed to distribute to minority owned affiliates?

- *Can we simply rely on the enumerated list of affiliates?*

---

**IAtD-17** - Can I use the service for price validation?

- *Covered by the Non-Display action*

---

**IAtD-18** - Is there a cost to view delayed data?

- *Covered by timeliness constraints - but we need to make explicit what today is implicit*

**IAtD-19** - What duration of time is required for data to be considered delayed?

- *Covered by timeliness constraints*

**IAtD-20** - How many times am I allowed to snap real-time data for a display application, before I must declare those with access for real-time? 

- *Covered by the Count constraint on Snapshot*

---

**IAtD-3** - I’m setting up a new user location - can I send this data to a new, internal geographic location?

**IAtD-16** - Can I share my access to the service with colleagues?

- **Need to add a location constraint - and others like line-of-business, department, etc**

---

**IAtD-5** - Can I get a free trial access for any user?

**IAtD-6** - Can I get a free trial access for applications within development?

- **Need to add support for free trials under payment duties**

---

**IAtD-8** - Do I need to declare and/or pay for data utilisation within my business continuity / disaster recovery environements?

- **Need to add support**

---

**IAtD-12** - If I cancel a service, am I required to purge the data I am storing in my systems from that service?

- **Need to add support**

---

**IAtD-13** - Can I subscribe to real-time/delayed/snapshot data and persist my own historical repository of data from this service?

**IAtD-14** - Can I download data from a terminal and store on a network drive for personal access?

- **Do we need a Store action?**

**IAtD-15** - Can I download data from a terminal and store on a network drive for my team to access?

- **Need to combine the solutions to IAtD-3 and IAtD-13**

---

## Redistribution of Data
Sending data externally (attributes vary across all vendors and/or may require additional licenses which incur costs)

**RoD-14** - When sending raw/source data externally, what accreditation and disclaimers am I required to use (if any)?

- *Covered by Attribution and Disclaimer dutes*

**RoD-5** - I’m downloading a tearsheet from a rating agency – am I allowed to share this with colleagues and/or with clients?

- *Covered by the Distribute action*

---

**RoD-1** - Can I send a small amount of data to a client, in support of a transaction, on a one-off basis?

**RoD-2** - Can I send appx 10 years data for a couple of data points, in an Excel spreadsheet, to a potential client?

**RoD-3** - Can I send some data, in a chart format, in a research report to 400 clients, on a monthly basis?

**RoD-4** - I’m creating a spreadsheet containing a terminal vendor’s data – am I allowed to share this with clients

**RoD-10** - Can I send some data, in charts and/or tables, in a non-editable electronic or hardcopy format, in a client portfolio performance or valuation report to 2000 clients, on a monthly basis?

**RoD-11** - Can I send some data, in charts and/or tables, in a non-editable electronic or hardcopy format, in marketing materials to 5000 prospective clients, on an ad-hoc basis?

**RoD-12** - Can I send some data, in charts and/or tables, in an email or tweet/other social media post, as marketing to an unlimited number of current and prospective clients, on a weekly basis?

**RoD-13** - How many slides containing your data can I put into a client presentation?

- **Need an amount property which can be qualified by frequency, format, and purpose**

---

**RoD-6** - Can I publish a particular real-time data set to a public (unauthenticated) website or widget?

**RoD-7** - Can I publish a particular real-time data set to an authenticated website or widget?

**RoD-8** - Can I publish a particular delayed data set to a public (unauthenticated) website or widget?

**RoD-9** - Can I publish a particular delayed data set to an authenticated website or widget?

- *Authenticated/Unauthenticated handled by Controls; Realtime/Delayed by Timeliness*

- **Need to add support for distibution to websites/whitelabel

---

## Non-display Use
For example, use of real-time data in a new application

**NDU-1** - Can I use real-time data in a new internal application, which will not display the data to any end users?

**NDU-2** - Can I distribute the results from the new application to other users internally?

**NDU-3** - Can I distribute the results from the new application to other users at a different internal geographic location?

**NDU-4** - Can I distribute the results from the new application to external users at the end of each day?

**NDU-5** - If I want to use real-time data in an internal application that performs a simple calculation but also displays the data to end users, is that considered a non-display use?

**NDU-6** - If I want to use real-time data for portfolio valuation for internal use only, is that a non-display use?

**NDU-7** - Are separate non-display fees imposed for each internal application?


## Derived Data
Data being derived from varying sources, including for creation of Indices

**DD-1** - Can I create derived data from one vendor/exchange, using end of day data, for internal use?

**DD-2** - Can I create derived data, using delayed data, from 5 different vendors/exchanges, for internal use?

**DD-3** - Can I create derived data, in the form of an index, using EOD data, from 5 different vendors/exchanges, and send the result to a client?

**DD-4** - Can I create a spreadsheet combining two vendors data to create derived data

**DD-5** - I’m creating a spreadsheet combining two vendors data to create derived data – am I allowed to share this with clients?

**DD-6** - Am I the intellectual property owner of the derived data that I have created?

**DD-7** - Can I create a tradeable CFD instrument using one or more particular data sets?

**DD-8** - Can I create a non-tradable product containing one or more particular data sets for use as input to pricing evaluation of physical products?

**DD-9** - Can I distribute my tradable derived instrument as a white-labeled product?

**DD-10** - Can I create a structured product using data as underlying?

**DD-11** - Can I create manipulated / reverse-calculable data and redistribute that internally?

**DD-12** - Can I create manipulated / reverse-calculable data and redistribute that externally?

**DD-13** - Can I create derived data and then display it on a public website?

**DD-14** - Is data commingled from a single source classed as derived data by that source provider?


## Reporting & Audits

**R-1** - What is the unit of count I need to report?

**R-2** - How often do I need to report?

**R-3** - How long do I have to maintain records of usage/entitlement for including after termination?

**R-4** - Does the vendor have the right to audit me?

**R-5** - How far back can the vendor audit me?

**R-6** - What interest and fees can an audit attract?

**R-7** - Do DACS compliant applications need to be considered for the unit of count? 


## Termination

**T-1** - How much notice do I need to give to cancel the service?

**T-2** - In what situations would I be allowed to cancel the service early?

**T-3** - In what situations would you be allowed to terminate our access to your service?
