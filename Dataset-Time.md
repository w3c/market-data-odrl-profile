# DATASET TIME DIMENSIONS
## 1.	Timeliness
```dprod:timeliness```

**Cardinality**

0 – 1

**Label**

Timeliness of delivery

**Definition**

Specifies the timing of the permitted use or onwards delivery of a Dataset.

**Note**

These intervals are frequently identified as Realtime, Delayed, or Embargoed.

**Note**

Unless explicitly prohibited, Permissions over shorter intervals carry across to longer intervals (e.g. Realtime data also covers Delayed, and Embargoed data)

**Domain**

```dcat:Dataset```

**Range**

```time:ProperInterval```

### 1.1.	Interval: Realtime
```dprod:Realtime```

**Label**

Realtime

**Definition**

Data received, used, or delivered with minimum latency after its time of origination, publication, or issue. 

**Note**

The latency can be quantified by specifying the beginning of the interval (```time:hasBeginning```) and its duration (```time:hasXSDDuration```).

**Subclass Of**

```time:ProperInterval```

**Code Example**

*A dataset in which data is received, used, or delivered with minimum latency.*
```
[]
	a			dcat:Dataset ;	
	dprod:timeliness	dprod:realtime .
```

**Code Example**

*A dataset in which data is received, used, or delivered with a latency of less than 15 minutes from time of issue.*
```
[]
	a			dcat:Dataset ;	
	drod:timeliness		[
					a			dprod:Realtime ;
					dc:title		"Realtime" ;
					dc:description		"Less than 15 minutes from time of issue" ;
					time:hasBeginning	dprod:timeOfIssue ;
					time:hasXSDDuration	"PT15M"^^xsd:duration ;
				] .
```

### 1.2.	Interval: Delayed
```dprod:Delayed```

**Label**

Delayed

**Definition**
Data received, used, or delivered at or after a specified time interval following its time of origination, publication, or issue. 

**Note**
The delay can be quantified applying the ```time:intervalAfter``` property to the Realtime interval specification.

**Subclass Of**

```time:ProperInterval```

**Code Example**

*A dataset in which data is delayed before receipt, use, or delivery.*
```
[]
	a			dcat:Dataset ;	
	drop:timeliness		dprod:delayed .
```

**Code Example**

*A dataset in which data is delayed by 15 minutes before receipt, use, or delivery.*
```
[]
	a			dcat:Dataset ;	
	dprod:timeliness	[
					a			dprod:Delayed ; 
					dc:title		"Delayed" ;
					dc:description		"More than 15 minutes from time of issue" ;
					time:intervalAfter	[
									a			time:ProperInterval ;
									time:hasBeginning	dprod:timeOfIssue ;
									time:hasXSDDuration	"PT15M"^^xsd:duration
								] ;
				] .
```

### 1.3.	Interval: Historical
```dprod:Historical```

**Label**

Historical

**Definition**

Stored data that relates to events in the past. 

**Note**

Usually held in the form of a time series

**Subclass Of**

```time:ProperInterval```

### 1.4.	Interval: Embargoed
```dprod:Embargoed```

**Label**

Embargoed

**Definition**

Data received, used, or delivered on or after a specified instant or future event. Can be quantified using the ```time:intervalAfter``` property with the embargo time specified using the time:hasBeginning property.

**Editorial Note**

Used to describe end-of-day or after-midnight data.

**Subclass Of**

```time:ProperInterval```

**Code Example**

*An embargoed dataset in which the data is made available at midnight.*
```
[]
	a			dcat:Dataset ;	
	dprod:timeliness	[
					a			dprod:Embargoed ;
					dc:title		"After midnight data" ;
					time:hasBeginning	dprod:midnight ;
				] .
```

**Code Example**

*An embargoed dataset in which the data is made available two hours after market close.*
```
[]
	a			dcat:Dataset ;	
	dprod:timeliness	[
					a			dprod:Embargoed ; 
					dc:title		"Embargoed until two hours after market close" ;
					time:intervalAfter	[
									a			time:ProperInterval ;
									time:hasBeginning	dprod:marketCose ;
									time:hasXSDDuration	"PT2H"^^xsd:duration
								] ;
				] .
```

### 1.5.	Instant: Origination Time
```dprod:originationTime```

**Label**

Origination time

**Definition**

The moment information condenses into data.

**Example**

The instant a price is struck and recorded.

**Type**
```time:Instant```

### 1.6.	Instant: Publication Time
```dprod:publicationTime```

**Label**

Publication time

**Definition**

The instant data is released by the Originator for distribution

**Type**

```time:Instant```

### 1.7.	Instant: Issue Time
```dprod:issueTime```

**Label**

Issue time

**Definition**

The instant data is distributed from the Originator

**Type**

```time:Instant```

### 1.8.	Instant: Market Close
```dprod:marketClose```

**Label**

Market close

**Definition**

The time published by the venue specifying when a market closes.

**Type**
```time:Instant ```

## 2.	Update Method
```dprod:updateMethod```

**Cardinality**

0 – 1

**Label**

Method of update

**Definition**

Specifies the method by which a Dataset is updated. 

**Note**

Must have a value of either Snapshot, Streaming, or Time Series

**Domain**

```dcat:Dataset```

**Range**

```dprod:UpdateMethod```

### 2.1.	Snapshot
```dprod:Snapshot```

**Label**

Snapshot

**Definition**

An update is provided only in response to a request (like an API call). 

**Editorial Note**

Also known as “one-shot”.

**Note**

The number of requests (or snaps) permitted can be specified using the ```dprod:Frequncy``` class (the count property (```odrl:count```) combined with a duration (```time:hasXSDDuration```).)

**Subclass Of**
```dprod:UpdateMethod```

**Code Example**
*A dataset for which updates can only be requested twice a day.*
```
[]
	a			dcat:Dataset ;
	dprod:updateMethod	[
					a 			dprod:Snapshot ;
					dprod:frequency		[
									a			dprod:Frequency ;
									dc:description		"Twice daily" ;
									odrl:count		2 ;
									time:hasXSDDuration	"PT1D"^^xsd:duration ;
								] ;
				] .
```

### 2.2.	Streaming
```dprod:streaming```

**Label**

Streaming

**Definition**

Changes are captured and continuously transmitted either individually or in batches.

**Subclass Of**

```dprod:UpdateMethod```

**Code Example**
*A 15-minute delayed dataset with streaming updates.*
```
[]
	a			dcat:Dataset ;	
	drop:timeliness		[
					a			dprod:Delayed ;
					dc:title		"Delayed" ;
					dc:description		"More than 15 minutes from time of issue" ;
					time:intervalAfter	[
									a			time:ProperInterval ;
									time:hasBeginning	dprod:timeOfIssue ;
									time:hasXSDDuration	"PT15M"^^xsd:duration
								] ;
				] ;
	dprod:updateMethod	dprod:streaming .
```

### 2.3.	Time Series
```dprod:timeSeries```

**Label**

Time Series

**Definition**

Multiple updates are delivered together in bulk, often as a file.

**Type**

```dprod:UpdateMethod```
 
**Code Example**
*A tick-history dataset updated with 8-hour delayed data delivered as a time series.*
```
[]
	a			dcat:Dataset ;	
	drop:timeliness		[
					a			dprod:Delayed ;
					dc:title		"Delayed" ;
					dc:description		"More than 8 hours from time of issue" ;
					time:intervalAfter	[
									a			time:ProperInterval ;
									time:hasBeginning	dprod:timeOfIssue ;
									time:hasXSDDuration	"PT8H"^^xsd:duration
								] ;
				] ;
	dprod:updateMethod	dprod:timeSeries .
```

## 3.	Update Period
```dprod:updatePeriod```

**Cardinality**

0 – 1

**Label**

Period of update

**Definition**

The period during which the Dataset has been, or continues to be, updated.

**Note**

If the Dataset is updated while a subscription holds, use the Service Period interval.

**Domain**

```dcat:Dataset```

**Range**

```time:ProperInterval```

### 3.1.	Service Period
```dprod:servicePeriod```

**Label**
Service period

**Definition**
The period across which a subscription holds.

Type
```time:ProperInterval```

**Code Example**

*A dataset for which the vendor will continue to provide updates while the subscription holds.*
```
[]
	a			dcat:Dataset ;	
	dprod:updatePeriod	dprod:servicePeriod .
```

**Code Example**

*A dataset for which the vendor will continue to provide updates for a year.*
```
[]
	a			dcat:Dataset ;	
	dprod:updatePeriod	[
					a			dprod:ServicePeriod ;
					time:hasXSDDuration	"PT1Y"^^xsd:duration ;
					# Start the clock ticking with the time:hasBeginning property
				] .
```

## 4.	Sample Frequency
```dprod:sampleFrequency```

**Cardinality**

0 – 1

**Label**

Sample Frequency

**Definition**

Specifies if and how often a data stream is sampled to provide updates to the Dataset 

**Note**

Must have a value of either Tick-By-Tick or Sampled

**Domain**

```dcat:Dataset```

**Range**

```dprod:SampleFrequency```

### 4.1.	Tick by Tick
```dprod:tickByTick```

**Label**
Tick-by-tick

**Definition**
Each and every change in value is provided in an update.

**Type**
```dprod:SampleFrequency```

**Code Example**

*A complete tick-history dataset capturing every price updated with 8-hour delayed data delivered as a time series.*
```
[]
	a			dcat:Dataset ;	
	drop:timeliness		[
					a			dprod:Delayed ;
					dc:title		"Delayed" ;
					dc:description		"More than 8 hours from time of issue" ;
					time:intervalAfter	[
									a			time:ProperInterval ;
									time:hasBeginning	dprod:timeOfIssue ;
									time:hasXSDDuration	"PT8H"^^xsd:duration ;
								] ;
				] ;
	dprod:updateMethod	dprod:timeSeries ;
	dprod:sampleFrequency dprod:tick-By-Tick .
```

### 4.2.	Sampled
```dprod:sampled```

**Definition**
Updates are sampled and/or conflated.

**Note**
Only selected updates are delivered at specified intervals or on specific events (e.g. market close or quarterly results).

**Note**
A continuous sampling frequency of can be specified using the ```dprod:frequency``` property.

**Label**
```Sampled```

**Subclass Of**
```dprod:SampleFrequency```

**Code Example**

*A 15-minute tick-history dataset updated with 8-hour delayed data delivered as a time series.*
```
[]
	a			dcat:Dataset ;	
	drop:timeliness		[
					a			dprod:Delayed ;
					dc:title		"Delayed" ;
					dc:description		"More than 8 hours from time of issue" ;
					time:intervalAfter	[
									a			time:ProperInterval ;
									time:hasBeginning	dprod:timeOfIssue ;
									time:hasXSDDuration	"PT8H"^^xsd:duration
								] ;
				] ;
	dprod:updateMethod	dprod:timeSeries ;
	dprod:sampleFrequency [
					a 			dprod:Sampled
					dprod:frequency		[
									a			dprod:Frequency ;
									dc:description		"Every 15 minutes" ;
									time:hasXSDDuration	"PT15M"^^xsd:duration ;
								] ;
				] .
```

## 5.	Publication Schedule
```dprod:publicationSchedule```

**Cardinality**

0 – 1

**Label**

Publication Schedule

**Definition**

Specifies the ```dprod:frequency``` with which updates to a Dataset are published

**Note**
The time at which updates are published can be specified using the ```schema:availabilityStarts``` property

**Domain**

```dcat:Dataset```

**Range**

```dprod:PublicationSchedule```

**Code Example**

*A 15-minute tick-history dataset updated with 8-hour delayed data and delivered as a time series twice per day at 9:30 and 14:30.*
```
[]
	a			dcat:Dataset ;	
	drop:timeliness		[
					a			dprod:Delayed ;
					dc:title		"Delayed" ;
					dc:description		"More than 8 hours from time of issue" ;
					time:intervalAfter	[
									a			time:ProperInterval ;
									time:hasBeginning	dprod:timeOfIssue ;
									time:hasXSDDuration	"PT8H"^^xsd:duration
								] ;
				] ;
	dprod:updateMethod	dprod:timeSeries ;
	dprod:sampleFrequency	[
					a 			dprod:Sampled
					time:hasXSDDuration	"PT15M"^^xsd:duration
				] ;	
	dprod:publicationSchedule [
					a 			dprod:PublicationSchedule
					dprod:frequency		[
									a			dprod:Frequency ;
									dc:description		"Twice daily" ;
									odrl:count		2 ;
									time:hasXSDDuration	"PT1D"^^xsd:duration ;
								] ;
					schema:availabilityStarts "09:30:10Z"^^xsd:time , "14:30:10Z"^^xsd:time
				] .
```

### 6.	Temporal
```dprod:temporal```

**Cardinality**

0 – 1

**Definition**

The temporal coverage offered by a dataset.

**Scope Note**

Usually used to specify the date range of historical data.

**Note**

If no end-date is specified for the interval, then it is assumed to be “now”.

**Label**

Temporal coverage

**Domain**

```dcat:Dataset```

**Range**

```time:ProperInterval```

**Sub-property Of** 

```dc:temporal```

**Code Example**

*A 15-minute tick-history dataset offering 7 years of history, updated with 8-hour delayed data and delivered as a time series twice per day at 9:30 and 14:30.*
```
[]
	a			dcat:Dataset ;	
	drop:timeliness		[
					a			dprod:Delayed ;
					dc:title		"Delayed" ;
					dc:description		"More than 8 hours from time of issue" ;
					time:intervalAfter	[
									a			time:ProperInterval ;
									time:hasBeginning	dprod:timeOfIssue ;
									time:hasXSDDuration	"PT8H"^^xsd:duration
								] ;
				] ;
	dprod:updateMethod	dprod:timeSeries ;
	dprod:sampleFrequency	[
					a 			dprod:Sampled
					time:hasXSDDuration	"PT15M"^^xsd:duration
				] ;	
	dprod:publicationSchedule [
					a 			dprod:PublicationSchedule
					odrl:count		2 ;
					time:hasXSDDuration	"PT1D"^^xsd:duration ;
					schema:availabilityStarts "09:30:10Z"^^xsd:time, "14:30:10Z"^^xsd:time ;
				] ;
	dprod:temporal		[
					a			time:ProperInterval ;
					time:hasXSDDuration	"P7Y"^^xsd:duration ;
				] .

```

