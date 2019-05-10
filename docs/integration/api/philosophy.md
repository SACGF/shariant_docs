# API Philosophy

There are some fundamental principals that we're currently applying to the API

* To be able to do the majority of modifications through the one end-point with different parameters. This was decided to help support batch submissions in future.
* As long as the API submission is well formatted JSON, nearly everything uploaded will create a new (or alter an existing) variation classification record. The record itself may be marked with errors but they can be fixed with subsequent API calls or interaction with the web UI.
* There will be a level of normalisation applied to submitted data, case insensitive "true", "T", 1 will be converted to `true` - and "false", "F" and 0 to `false` for boolean fields, drop down field values will have their case corrected. The level of normalisation will be limited as to reduce unexpected behaviour.
* We'll be mainly accepting free form text, so citing of publications or other resources will be achieved by parsing through the text looking for patterns, such as "PMID: XXXX" rather than requiring special structure in the submission.
* Under no circumstances should patient identifiable data be uploaded.