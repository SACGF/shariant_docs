# Variant Classification Lifecycle

Here's a general view of what will happen to a classification.
There are more details about each step.

## Assign an internal id

Before a record is uploaded to Shariant, it should be given an alpha-numeric id that is unique to your lab.
This "lab_record_id" can then be referenced in the future to refer to the classification.

## Uploaded to Shariant

Along with your "lab_record_id" the sync tool will upload your evidence data to Shariant. If a record already exists with that id it will update the fields you provide, otherwise a new record will be created.

## Variant matching

Using the fields you've provided, Shariant will start a process of variant matching for that classification. The record will be given a "Matching Variant" flag. Shortly after that flag will be automatically closed, if a variant couldn't be matched the record will now be flagged as "Matching Variant Failed" and the record will need to be deleted and attempted to be imported again.

## Submitting/Sharing

As the sync tool uploads the records, it can also request that they be submitted to a specific share level. Share levels (covered elsewhere) determine who can see your record, including exporting to 3rd parties.
Note that records must be free of errors to be submitted and shared.

## Discordance

Once you've shared a record wider than your organisation, it will be included in discordance calculations. If another classification for the same variant (even from your lab) has come to a different clinical significance the records will be marked with a "Discordance" flag.

## Updates

The same record can be uploaded an indefinate number of times. Shariant will store a version for each change, presenting the latest record to other users but previously submitted versions will still be accessible.
As your curation system is considered the "source of truth", the cycle that includes re-uploading classifications is vital.

## Clinvar Submission

TODO