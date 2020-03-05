# API Philosophy

There are some fundamental principals that we're currently applying to the API:

The connector sync code that uploads the data should be repeatable and predictable. When data is missing or something else needs to be fixed, rather than manually tweaking things via the API - make the adjustments to the data in your curation system then re-run the connector sync code.

In addition the above, your curation system is to be considered the source of truth for the data. Evidence keys referenced by the sync code will become read-only to web users - so web users can't change data only then to have it overriden by the next sync. Data changes should be done directly in the curation system ready for the next sync.

As long as the API submission is a well formatted JSON, nearly everything uploaded will create a new (or alter an existing) variation classification record. The record itself may be marked with errors but they can be fixed in a subsequent sync or interaction with the web UI.

There will be a level of normalisation applied to submitted data, "true", "TruE", "T", 1 will be converted to `true` - and "false", "F" and 0 to `false` for boolean fields, drop down field values will have their case corrected.

We'll be mainly accepting free form text, so citing of publications or other resources will be achieved by parsing through the text looking for patterns, such as "PMID: XXXX" rather than requiring special structure in the submission.

Under no circumstances should identifiable patient data be uploaded.

Please note there is a test server https://test.shariant.org.au/

Due to the terms and conditions, do not upload real data to the test server, instead use mock data in the same format as the production data.
