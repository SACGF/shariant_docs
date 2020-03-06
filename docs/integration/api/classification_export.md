# API Variant Classification Export

The Shariant web interface provides a page that will build the GET URL for generating a file your system can take in and interpret.

https://shariant.org.au/variantclassification/export

To build URLs such as 

https://shariant.org.au/variantclassification/api/classifications/export?share_level=public&build=GRCh38&type=mvl&conflict_strategy=most_pathogenic&exclude_labs=testy_pathology%2Flab_zues

These URLs will still require an authenticated request to download.

Please note the following properties of the export.

Ensure that your own lab(s) are excluded from the download. You don't want your own records to refer to themselves via their Shariant copies.

Some formats can only provide limited information (e.g. MVL and VCF), but MVLs provide direct links to the Shariant page for the variant, and in VCFs the id column can be used as the last part of a URL to get to that same page. (See the MVLs ##readme lines for details)

Variants will be uploaded by different users across multiple builds, e.g. GRCh37 and GRCh38. Most download formats convert all variants to a single build. Downloads may still contain specific data for the genome build used by the submitting user.

The REDCap export does not normalise on builds currently.

With the exception of the JSON and CSV format, all other formats will exclude classifications that couldn't correctly match a variant, have a variant matching warning, or where the variant couldn't be converted to the desired build.
