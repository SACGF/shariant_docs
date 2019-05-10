# Integration Getting Started

Steps

## Step 1 : Defining the sync tool

Shariant accepts the upload of classifications via REST and is authenticated via OAUTH2.
Shariant will not initiate any communication to your system (e.g. you wont have to open any ports or provide us authentication) instead it waits for uploads and requests for downloads.

You will need to have a tool running with access to your curation data on your network/cloud. This will be responsible for providing classifications to Shariant and if possible, automatically providing Shariant classifications as annotations to your system.

If your curation system is one that we've seen before, we can get you started with integration code.
If it's new, we do have a python library that will provide some structure around the calls.
If your IT team already has a series of integrations, they're welcome to use any existing framework to perform the syncing.

## Step 2 : Accessing and identifying data for the sync tool

Your curation system may have an API to access its data, it might have a database on your network that you can query or you might have to do a regular extract to a file and process that.
In addition it is unlikely you'll want to upload all records from your system immediately. Some systems may let you add arbitrary tags to your system or you may already have a column to indicate that the classification is in a complete state.

Some additional questions you may want to ask at this point:
How frequently will the sync process take place?
Will you re-upload all relevant records or only the ones that have changed?


## Step 3 : Mapping from your structure to Shariants

Given any individual field you can enter in your system, how does it map to our pre-registered set of evidence keys?
The tool might just be able to rename the field, it might be more complicated and need to parse through the value to extract segments, or the field might indicate a value for one of our drop downs.

For example, if your system has a Yes/No field called "This gene is known to be associated with X-linked recessive disease." that would map to our field "mode_of_inheritance" with a value of "x_linked_recessive".

### Minimum mandatory set

Shariant enforces a small base level of required fields
* Fields to identify the variant, e.g. c.hgvs including gene symbol, ref and alt along with a transcript and a build (hg19 or 38)
* Lab record id: An ID you provide for the record so you can refer to it in future
* Clinical significance: How have you classified this on ACMG’s scale of Benign to Pathogenic
* Condition: What condition are you curating against
* Zygosity: Zygosity in the tested individual.

### Avoid personal identifiable information

You will also need to ensure you don't send us any information that could be used to identify the patient, specifically avoid names and addresses.
You will also need to ensure users don't enter such information into summaries or other fields you are mapping from your curation system.

## Step 4 : Maintenance & user interaction

It's possible that a small number of your records fail our variant mapping process, or miss out on mandatory information.
In addition, there will be valid records that run into discordance with classifications from other labs.

Individual classifications can be assigned to different users, if there's something on a classification that requires attention, the linked user will be notified by email.
Some issues can be fixed by updating your curation system and waiting for the next sync, others will require interaction with the Shariant website.

Work out which users will be repsonsible for which records, though any member of your lab has access to fix any issue with any of your lab's classifications.

## Step 5 : How best can your system integrate data from Shariant

Shariant provides an API for bulk downloading of classifications.
Currently we only provide classifications in our own JSON format, but on the roadmap is support for more export options such as VCF. It is expected that some systems will need custom solutions here, so some work may get done as the requirements come in.