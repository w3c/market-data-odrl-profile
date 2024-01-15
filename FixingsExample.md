# The Value of DCAT: Datasets and Dataset Series

**Challenge: How to represent the variety of uses of the same data within an organisation**

Let's try a real world example:

We are consuming Bloomberg proprietary data (BFIX, so Bloomberg FX Fixings) in applications used across the front, middle, and back-office.

## Front-Office Requirements
Since the fixings frequently determines the delta of a product (to determine if an FX option as struck or not), trading requires the data in real-time.

The real-time data itself is only available via bpipe (Bloomberg's real-time streaming technology). To display data from bpipe, access to a Bloomberg terminal or a view charge is required.
 
## Middle and Back-Office Requirements
Economically it makes no sense to equip all middle and back-office users with a view charge or even a BBG terminal. The very same data is therefore retrieved again, this time via Bloomberg Data License (aka "Per Security") with a 15-minute delay.

For settlement purposes that 15-minute delay is fully sufficient. Data consumed via Bloomberg Data License encompasses a group-wide display license.

## Summary
So effectively, we have an application where a data item is consumed from bpipe with access restricted to a specific user group. If the data is later retrieved again via a different channel (BBG Data License), that restriction is removed and display to all users is possible.


**Solution: Create two permissions each pointing to a distinct dataset but link both datasets via a dataset series**

We will use the ...

## Dataset Series
First, we can define the Dataset Series which describes the information we're after before it's commercialisation as Datasets. The dataset series describes the [content type](https://github.com/w3c/market-data-odrl-profile/blob/gh-pages/Dataset-Content.md#1content-type) and the [asset classes](https://github.com/w3c/market-data-odrl-profile/blob/gh-pages/Dataset-Content.md#2asset-class) (fixings for spots, forward, and non-deliverable forward FX rates), the originator of the data (Bloomberg Index Services Limited), and the IP owner (the same).

```
dre:af85e5b1-26a8-4e9f-a1ad-de5586d5c96e
	a			dcat:DatasetSeries ;
	dc:title		"The Bloomberg FX Fixings (BFIX) family of benchmarks covers spots, forward and non-deliverable forward (NDF) rates for a comprehensive global coverage of currencies and metals" ;
	dc:description		"BFIX is an accurate representation of up-to-date FX pricing. At each fix, you get the latest representation of the market, aggregated and streamlined from bid and ask data. This data is gathered from a wide variety of pricing providers." ;
	dc:identifier		"BFIX" ;
	dprod:contentType	[
					a 			dprod:Fixings ;
					dc:description		"Benchmarks covering spots, forward, and non-deliverable forward FX rates" ;
					dprod:assetClass	iso10962:IFXXXX , iso10962:JFTXFP , iso10962:JFTXFN ;

				] ;
	schema:url		<https://www.bloomberg.com/professional/product/indices/bfix/> ;
	dc:creator		lei:254900GIJ499G51QA968 ; # Bloomberg Index Services Limited
	dprod:ipOwner		lei:254900GIJ499G51QA968 .
```

Then we can describe the Datasets created from this Dataset Series. There are two in the example above: one [real-time](https://github.com/w3c/market-data-odrl-profile/blob/gh-pages/Dataset-Time.md#11interval-realtime) and one [delayed](https://github.com/w3c/market-data-odrl-profile/blob/gh-pages/Dataset-Time.md#12interval-delayed). Both datasets share the same Dataset Series and [publication schedule](https://github.com/w3c/market-data-odrl-profile/blob/gh-pages/Dataset-Time.md#5publication-schedule) (every 30 minutes).

For the real-time dataset, we would specify the time interval in which the data is considered real-time: 15 minutes. We might also specify the [update method](https://github.com/w3c/market-data-odrl-profile/blob/gh-pages/Dataset-Time.md#2update-method) as streaming updates.

```
dre:8752a444-e3e1-4be1-b4ac-01333941b202
	a			md:Asset , dcat:Dataset ;
	dc:title		"Realtime Bloomberg FX Fixings (BFIX)" ;
	dc:identifier		"BFIX" ;
	dprod:timeliness	[
					a			dprod:Realtime ;
					dc:description		"Less than 15 minutes from time of calculation" ;
					time:hasBeginning	dprod:timeOfCalculation ;
					time:hasXSDDuration	"PT15M"^^xsd:duration ;

				] ;
	dprod:publicationSchedule [
					a 			dprod:PublicationSchedule ;
					dc:description		"Published every 30 minutes" ;
					dprod:frequency		[																		a			dprod:Frequency ;
									dc:description		"Every 30 minutes" ;
									time:hasXSDDuration	"PT30M"^^xsd:duration ;
								] ;
				] ;
	dprod:updateMethod	md:streaming ;
	dcat:distribution	dre:3b601f6d-7ad1-4220-93fc-39284a6248f3 ;
	dprod:inSeries 		dre:dre:af85e5b1-26a8-4e9f-a1ad-de5586d5c96e ; # Linking to the dataset series described above
	dprod:provider		lei:549300B56MD0ZC402L06 . # Bloomberg LP
```

For the delayed dataset, we would specify the time interval after which the data is considered delayed: 15 minutes. We might also specify the update method as a time series.

```
dre:a6be3f7a-ecb9-4d3f-acaa-01f2c07c3d3c
	a			md:Asset , dcat:Dataset ;
	dc:title		"Delayed Bloomberg FX Fixings (BFIX)" ;
	dc:identifier		"BFIX" ;
	dprod:timeliness	[
					a			dprod:Delayed ;
					dc:description		"More than 15 minutes from time of calculation" ;
					time:intervalAfter	[
									a			time:ProperInterval ;
									time:hasBeginning	dprod:originationTime ;
									time:hasXSDDuration	"PT15M"^^xsd:duration
								] ;
				] ;
	dprod:publicationSchedule [
					a 			dprod:PublicationSchedule ;
					dc:description		"Published every 30 minutes" ;
					dprod:frequency		[
									a			dprod:Frequency ;
									dc:description		"Every 30 minutes" ;
									time:hasXSDDuration	"PT30M"^^xsd:duration ;
								] ;
				] ;
	dprod:updateMethod	md:timeSeries ;
	dcat:distribution	dre:d067b56c-1f79-48e1-bd6c-0836979d533a ;
	dprod:inSeries 		dre:dre:af85e5b1-26a8-4e9f-a1ad-de5586d5c96e ; # Linking to the dataset series described above
	dprod:provider		lei:549300B56MD0ZC402L06 . # Bloomberg LP
```

Finally, we can create two Permissions. The Permission controlling the real-time data specifies the assignee as just FI "XYZ" (no affiliates) and constrain the users of the Permission to just those working in the front office. Likely, we'd also have to specify that those users be members of a Closed User Group - so only authorized and authenticated users can access the data.

```
dre:1dab2ac7-ef96-41e3-8b2f-bdd9ead1a983
	a                       md:Permission ;
	tpl:effectiveFrom       "2021-01-01T00:00:00Z"^^xsd:dateTime ;
	dc:title		"Display of Realtime Bloomberg FX Fixings" ;
	dc:description		"Front-office display of realtime Bloomberg FX Fixings in a client-managed environment" ;
	odrl:assigner		lei:549300B56MD0ZC402L06 ;
	md:assigneeList		[
					a			md:AssigneeList ;
					dc:description		"Commerzbank AG";
					md:licensee		lei:851WYGNLUQLFZBSYGB56 ;
				] ;
	rbim:cdm		rbim:enterpriseDisplayService ;
	md:users		[
					a 			md:InternalParty ;
					dc:description		"Internal consumers in the front office" ;
					md:roles		md:consumer ;
					md:function		md:frontOffice ;
				] ;
	md:controls		[
					a			md:ClosedUserGroup ;
					dc:description		"Vendor-managed Closed User Group" ;
					md:systemProvider	lei:549300B56MD0ZC402L06 ; # Bloomberg LP
				] ;
	odrl:action		[
					a			md:Display ;
					dc:title		"Vendor-managed Display" ;
					md:systemProvider	lei:549300B56MD0ZC402L06 ; # Bloomberg LP
				] ;
	odrl:target		dre:8752a444-e3e1-4be1-b4ac-01333941b202 .
```

The Permission to display the delayed data need not be so strict. We could set the assignee to FI "X" and all its majority owned subsidiaries. The users of the Permission is set to Enterprise (i.e. everyone working for FI "X" and all its majority owned subsidiaries.) We probably don't need to specify any access control requirements.

```
dre:5c2b155b-b7e2-416a-bd5d-5ed93dd2b61b
	a                       md:Permission ;
	tpl:effectiveFrom       "2021-01-01T00:00:00Z"^^xsd:dateTime ;
	dc:title		"Display of Delayed Bloomberg FX Fixings" ;
	dc:description		"Enterprise display of delayed Bloomberg FX Fixings" ;
	odrl:assigner		lei:549300B56MD0ZC402L06 ;
	md:assigneeList		[
					a			md:AssigneeList ;
					dc:description		"Commerzbank AG and majority owned subsidiaries";
					md:licensee		lei:851WYGNLUQLFZBSYGB56 ;
					md:minHolding         	"0.5"^^xsd:decimal ;
				] ;
	rbim:cdm		rbim:clientOpenDisplayService ;
	md:users		[
					a 			md:InternalParty ;
					dc:description		"Data consumers across the enterprise" ;
					md:roles		md:consumer ;
					md:lineOfBusiness	md:enterprise ;
				] ;
	odrl:action		md:display ;
	odrl:target		dre:a6be3f7a-ecb9-4d3f-acaa-01f2c07c3d3c .
```

So, to summerise: we have one Dataset Series, that is provided as a real-time Dataset and a delayed Dataset. Each Dataset is then controlled by a different Permission.
