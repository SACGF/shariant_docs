# Variant Classification Downloads

## Overview

As we as having your lab upload classifications to Shariant, we want to get Shariant's classifications in your curation system so you can quickly see if a variant has been previously classified using your regular workflow.

The download file can be downloaded by a user manually, or streamed directly into your connector with additional coding, and can be in one of the following formats:
* CSV
* JSON
* MVL
* REDCap
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

Once all that is configured a re-usable URL will be produced that you can either bookmark or invoke from custom connector code.
Some formats provide all the data Shariant has, while others only have summary data and a link to the relevant Shariant data.

## CSV

* The CSV format provides one row per variant classification and all the evidence other labs have uploaded.
* The first few columns are header information, e.g. record ids and the normalised c.hgvs value, they are then is then followed by columns of imported data.
* The CSV can be configured to use codes, or more human readable headers and values.

## JSON

The JSON format is what Shariant internally uses when displaying data on web pages and closely matches the internal database representation of records.

* JSON downloads will download an array called "records" with a JSON object per variant classification.
* Each record classification will show evidence in the format of "key": {"value": X, "note": Y} etc.
* Each record will have an allele section that will show data about the variant lifted over to GRCh37 and GRCh38.

## MVL

The MVL format is used for Agilent's Alissa. If you are using Alissa you'll want this file format, if you're not, another format would be more appropriate.

* For Alissa 5.2 the MVL will need to be sent to Agilent for processing (for 5.3 we are looking to see if htis can be automated)
* The MVL format provides one entry per variant/transcript combination, but that entry will include summary details and links about all the classifications.
* The default settings for the MVL will work with vanilla settings of Alissa
* One important detail is that if there's classifications for the same variant that come to different clinical contexts, we can only provide a single overall value - so you can choose if that value is the least or most pathogenic. It's good practise to double check Shariant when a variant in Alissa is highlighted as existing in a Shariant MVL to see the latest records.

## REDCap

The REDCap export isn't currently useable in the Shariant environment.

## VCF

VCF (Variant Class Format 4.1) is a common format used for bioinfomatics.

* The VCF will have one row per variant, but using additional info fields have repeatable values. So if a single variant has 3 classifications, the INFO fields lab and chgvs with each have 3 comma separated values. The first  lab and first INFO chgvs for that row all relate to the same record. Likewise the second of each of those fields refer to the next record, etc.
* The VCF has the least amount of data of all the formats, but provides a link to the relevant Shariant page to see all the data.