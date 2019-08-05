# Integration Getting Started

## Step 1 : Defining the sync tool

Shariant accepts the upload of classifications via REST and is authenticated via OAUTH2.
Shariant will not initiate any communication to your system (e.g. you wont have to open any ports or provide us authentication) instead it waits for uploads and requests for downloads.

You will need to have a tool running with access to your curation data on your network/cloud. This will be responsible for providing classifications to Shariant and if possible, automatically providing Shariant classifications as annotations to your system.

If your curation system is one that we've seen before, we can get you started with integration code.
If it's new, we do have a Python library that will provide some structure around the calls.
If your IT team already has a series of integrations, they're welcome to use any existing framework to perform the syncing.

## Step 2 : Accessing and identifying data for the sync tool

Your curation system may have an API to access its data, it might have a database on your network that you can query or you might have to do a regular extract to a file and process that.

You probably don't want to upload all of your variants immediately, so it is useful to add some tags/fields to your system to help decide what to share and help with the integration.

* Last modified date
* Whether the variant is complete
* Share level

Last modified can be used to determine what you need to send to us since your last upload. The other fields are to determine whether to send the classification to us, and what the initial share status should be.

Some additional questions you may want to ask at this point:

* How do I uniquely identify a record from my lab (probably your internal database primary key)
* How frequently will the sync process take place?
* Will you re-upload all relevant records or only the ones that have changed?


## Step 3 : Mapping from your structure to Shariants

Given any individual field you can enter in your system, how does it map to our [pre-registered set of evidence keys](https://shariant.org.au/variantclassification/evidence_keys)?
The sync tool may just need to use a different field name, or the mapping process may be more complicated.

For example, if your system has a Yes/No field called "This gene is known to be associated with X-linked recessive disease." that would map to our field "mode_of_inheritance" with a value of "x_linked_recessive".

### Minimum mandatory set

Shariant enforces a small base level of required fields
* Fields to identify the variant, e.g. c.hgvs including gene symbol, ref and alt along with a transcript and a build (hg19 or 38)
* Lab record id: An ID you provide for the record so you can refer to it in future
* Clinical significance: How have you classified this on ACMG’s scale of Benign to Pathogenic
* Condition: What condition are you curating against
* Zygosity: Zygosity in the tested individual.

### Avoid personal identifiable information

Do not send us any information that could be used to identify the patient, specifically avoid names, detailed pedigrees, birth dates and addresses.
You must also not enter such information into summaries or other fields you are mapping from your curation system.

Your **lab record id** should be a number like "10125" which doesn't mean anything and can only be matched to a sample or patient if you have access to your own secured patient record system or a record of the mappings.

## Step 4 : Maintenance & user interaction

The Shariant API will return error messages for records that fail variant matching or are missing mandatory fields. Someone needs to periodically examine these logs and resolve any issues.

Individual classifications can be assigned to different users, if there's something on a classification that requires attention, the linked user will be notified by email.
Some issues can be fixed by updating your curation system and waiting for the next sync, others will require interaction with the Shariant website.

Assigning resposible users may cause less coordination work for your team, though any lab member can see and edit all of your lab's classifications.

## Step 5 : How best can your system integrate data from Shariant

Shariant provides an API for bulk downloading of classifications.
Currently we provide classifications in our own JSON format, CSV, MVL, VCF. It is expected that most systems will be able to use these formats but some may require a custom solution.