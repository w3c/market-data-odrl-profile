# DATASET CONTENT DIMENSIONS
## 1.	Content Type
```dprod:contentType```

**Cardinality:** 0 – n

**Label:** Content type

**Definition:** Specifies the type of content provided in a Dataset or Dataset Series

**Examples:** Indices, trading data, post trade data, fixings, news, economics, people

**Domain**

```dcat:Dataset, dcat:DatasetSeries```

**Range**

```dprod:ContentType```

**Code Example**

*A dataset providing trading data from a venue.*
```
[]
	a			dcat:Dataset ;	
	dprod:contentType	[
					a			dprod:TradingData ;
				] .
```

## 2.	Asset Class
```dprod:assetClass```

**Cardinality:** 0 – n

**Label:** Asset class

**Definition:** Qualifies the content type of a Dataset or series by the financial asset class it describes.

**Domain**

```dprod:ContentType```

**Range**

```dprod:AssetClass``` – preferably using CFI codes as instance data

**Code Example**

*A dataset providing trading data for equities from a venue*
```
[]
	a			dcat:Dataset ;	
	dprod:contentType	[
					a			dprod:TradingData ;
					dprod:assetClass	iso10962:EXXXXX ;
				] .
```

## 3.	Market Depth
```dprod:marketDepth```

**Cardinality:** 0 – 1

**Label:** Depth of market

**Definition:** Measures the book depth offered by a Dataset

**Domain**

```dcat:Dataset```

**Range**

```dprod:MarketDepth```

**Code Example**

*A dataset providing full-order book trading data for equities from a venue*
```
[]
	a			dcat:Dataset ;	
	dprod:contentType	[
					a			dprod:TradingData ;
					dprod:assetClass	iso10962:EXXXXX ;
				] ;
	dprod:marketDepth	dprod:fullOrderBook .
```

### 3.1.	Last Trade Price
```dprod:lastTradePrice```

**Label:** Last trade price

**Definition:** The price at which the most recent trade was executed

**Type**

```dprod:MarketDepth```

### 3.2.	Market Price
```dprod:marketPrice```

**Label:** Market price

**Definition:** Market Price includes the content relating to at least the best bid and best ask/offer in the market.

**Editorial Note:** Also known as “Level 1” data.

**Note:** If more prices beyond the best bid are offered, the book depth can be specified by using the dprod:positionTo and dprod:positionFrom properties.

**Type**

```dprod:marketDepth```

### 3.3.	Full Order Book
```dprod:fullOrderBook```

**Label:** Full order book

**Definition:** The Full Order Book includes content relating to the bids and asks/offers at all price points and from all participants in the market.

**Editorial Note:** Also known as "market by order", the "detailed order book", or "Level 2"/"Level 3" data.

**Note:** If more prices beyond the best bid are offered, the book depth can be specified by using the dprod:positionTo and dprod:positionFrom properties.

**Type**

```dprod:MarketDepth```

## 4.	Spatial
```dprod:spatial```

**Cardinality:** 0 – n

**Label:** Geographic coverage

**Definition:** The geographic subject matter and focus of a dataset or series.

**Scope Note:** A characteristic of the dataset or series rather than its source/origin or any limitations on its distribution.

**Domain**

```dcat:Dataset, dcat:DatasetSeries```

**Range**

```schema:AdministrativeArea``` - UN M49 Codes for regions and subregions, ISO for countries and country subdivisions

**SubProperty Of**

```dc:spatial```

**Code Example**

*A dataset providing full-order book trading data for German equities*
```
[]
	a			dcat:Dataset ;	
	dprod:contentType	[
					a			dprod:TradingData ;
					dprod:assetClass	iso10962:EXXXXX ;
				] ;
	dprod:marketDepth	md:fullOrderBook ;
	dprod:spatial		iso3166:DE .
```

## 5.	Quantity (better word?)
```dprod:quantity```

**Cardinality:** 0 – 1

**Label:** Amount

**Definition:** The amount of a Dataset Series made available in a Dataset

**Note:** If a qualitative measure is all that is needed use the values ```dprod:Insubstantial``` or ```dprod:Substantial```. Else additionally specify a numeric value (```odrl:count```) and a unit of count (```odrl:unitOfCount```).

**Domain**

```dcat:Dataset```

**Range**

```dprod:Quantity```

**Code Example**

*A dataset providing full-order book trading data for three (German) instruments*
```
[]
	a			dcat:Dataset ;	
	dprod:contentType	[
					a			dprod:TradingData ;
					dprod:assetClass	iso10962:EXXXXX ;
				] ;
	dprod:marketDepth	md:fullOrderBook ;
	dprod:spatial		iso3166:DE ;
	dprod:quantity		[
					a			dprod:Insubstantial ;
					odrl:count		3 ;
					odrl:unitOfCount	md:instrument ;
				] .
```
 
