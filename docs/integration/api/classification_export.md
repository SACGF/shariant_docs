# API Variant Classification Export

The Shariant web interface provides a page that will build the GET URL for generating a file your system can take in and interpret.

https://shariant.org.au/variantclassification/export

To build re-usable URLs for downloading data.

Please note the following properties of the export:

The URL you generate by default will be for a web browser bookmark. In the case of wanting to generate a URL for some custom software to download you can choose to download for "API".
_In both cases it will still require a logged in user to perform the download._

Ensure that your own lab(s) are excluded from the download. You don't want your own records to refer to themselves via their Shariant copies.

Some formats can only provide limited information (e.g. MVL and VCF), but MVLs provide direct links to the Shariant page for the variant, and in VCFs the id column can be used as the last part of a URL to get to that same page. (See the MVLs ##readme lines for details)

Variants will be uploaded by different users across multiple builds, e.g. GRCh37 and GRCh38. Most download formats convert all variants to a single build. Downloads may still contain specific data for the genome build used by the submitting user.

With the exception of the JSON and CSV format, all other formats will exclude classifications that couldn't correctly match a variant, have a variant matching warning, or where the variant couldn't be converted to the desired build.

Some formats have additional formatting options, use these to customise the downloads to your curation system's preferences.
