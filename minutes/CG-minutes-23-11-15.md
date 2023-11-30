# Main Topics Discussed:

## The Relationships between Licensing, Discovery, Catalogues, and Enforcement
To unlock the full value of machine-readable rights statements we have to situate our ODRL policies in a wider world of datasets, catalogues, data services, and data products. How might we do this?

We took a look at the [DCAT](https://www.w3.org/TR/vocab-dcat-3/) model that defines the first three of these concepts and an extension (DPROD) that integrates the concept of data product. We then asked which of these should our policies control?

We discussed the importance of keeping our policies independent of the delivery technology, so targeting datasets rather than data services or data products.

To test this intuition, we revisited our ongoing efforts to define datasets at a level of specificity that allows ODRL rights to be directly associated datasets while remaining technology agnostic.

## License-sensitive dataset properties examined

[Temporal Attributes](https://github.com/w3c/market-data-odrl-profile/blob/gh-pages/Dataset-Time.md): Timeliness of Delivery, Update Method, Update Period, Sample Frequency, and Temporal Range.

[Content Attributes](https://github.com/w3c/market-data-odrl-profile/blob/gh-pages/Dataset-Content.md): Content Type, Market Depth, Spatial Coverage, and Quantity.

## Market Data Licensing Patterns
We discussed whether the great majority of market data licenses can be described using 20 or so [content delivery models](https://github.com/w3c/market-data-odrl-profile/blob/gh-pages/CDMs.md). We can test the idea by collecting exceptions. Will these be the exceptions to make or break the rule?


# Outstanding Questions:
1. Does DCAT have value in the market data world?
2. If so, is the link between ODRL and DCAT at the dataset level?
3. Should we hand over the dataset properties we have developed to the DPROD standardisation effort and focus our efforts solely on describing rights and obligations?
4. Do market data licenses really only implement a small number of patterns?


# Next Steps:
Our next meeting in January could focus on:
* The value of DCAT
* The value of content delivery models
* Lineage - mapping the relationships between master agreements and amendments

