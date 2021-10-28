# Variant Classification Downloads

## Overview

As well as having your lab upload classifications to Shariant, we want to get Shariant's classifications in your curation system so that you can quickly see if a variant has been previously classified using your regular workflow.

The download file can be downloaded by a user manually, or streamed directly into your connector with additional coding, and can be in one of the following formats:
* CSV
* JSON
* MVL
* VCF

More detail about each format is provided below.

Within each format there are some configuration options.
Please discuss with the Shariant team if none of the formats suit your needs as we can develop additional formats or tweak existing ones.

## Configuring Your Download

If you navigate to
[https://shariant.org.au/variantclassification/export](https://shariant.org.au/variantclassification/export)
you are presented with the download builder.

This page lets you choose if your downloads are going to be done manually in a web browser or invoked via API, the genome build, which labs to include/exclude, the format and any additional format parameters.
(Via web browser or API result in the same file, but the web browser link will provide you with a login page if you're not currently logged in)

Once configured, a re-usable URL will be produced that you can either bookmark or invoke from custom connector code.
Some formats provide all the data Shariant has, while others only have summary data and a link to the relevant Shariant data.

## CSV

* The CSV format provides one row per variant classification and all evidence other labs have uploaded.
* The first few columns are header information, e.g. record ids and the normalised c.hgvs value. These columns are then followed by columns of imported data.
* The CSV can be configured to use codes, or more human readable headers and values.

## JSON

The JSON format is what Shariant internally uses when displaying data on web pages and closely matches the internal database representation of records.

* JSON downloads will download an array called "records" with one JSON object per variant classification.
* Each record classification will show evidence in the format of "key": {"value": X, "note": Y} etc.
* Each record will have an allele section that will show data about the variant lifted over to GRCh37 and GRCh38.

## MVL

The MVL format is used for Agilent's Alissa Interpret interpretation system. 

* For Alissa 5.2, the MVL will need to be sent to Agilent for processing. If using Alissa v5.3, this can be uploaded manually in the Alissa interface.
* The MVL format provides one entry per variant/transcript combination, but that entry will include summary details and links about all classifications.
* The default settings for the MVL will work with most instances of Alissa, but it's important to check which clinical significance values are accepted by your instance (e.g. LIKELY_PATHOGENIC vs Likely Pathogenic).
* One important detail is that if there are classifications for the same variant that result in different clinical contexts, we can only provide a single overall value - so you can choose if that value is the least or most pathogenic. It's recommended that labs double check Shariant when a variant in Alissa is highlighted as existing in Shariant to view the latest records.

## VCF

VCF (Variant Class Format 4.1) is a common format used for bioinfomatics.

* The VCF will have one row per variant, but using additional info fields have repeatable values. So if a single variant has three classifications, the INFO fields lab and chgvs will each have three comma separated values. The first lab and first INFO chgvs for that row relate to the same record. Likewise the second of each of those fields refer to the next record, etc.
* The VCF has the least amount of data of all the formats, but provides a link to the relevant Shariant page to see all data.
