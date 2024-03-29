# API Variant Classification POST

All operations against a variant classification submission from your lab can be performed against a single end point:
https://shariant.org.au/classification/api/classifications/v2/record/

Ensure that any posts there are passing the required authentication data and is sending data as ContentType "application/json"

## Example Post

```json
{
	"id":"xyz_pathology/north_street_lab/F03432",
	"data": {
		"c_hgvs": "NM_000071.2(CBS):c.1539C>T",
		"genome_build": "GRCh37",
		"clinical_significance": "VUS",
		"zygosity": "hemizygous",
		"bp4": true,
		"mode_of_inheritance": ["autosomal_dominant", "autosomal_recessive"],
		"literature": "Found a book PMID: 342244"
	},
	"publish": "institution",
	"return_data": "changes"
}
```
or
```json
{
	"id":"xyz_pathology/north_street_lab/F03432",
	"delete": true
}
```

## All Parameters

|POST|Effect|
|----|------|
|`"id":_xxx_`|See ID Part|
|`"create":{}` or `"patch":{}` or `"overwrite":{}` or `"upsert":{}` or `"data":{}`|See Evidence Operation|
|`"publish":"_level_"`|see Publish|
|`"delete":true`|See Deleting|
|`"test":true`|The effects of your POST operation will not be saved on the server. This is handy for validation.|
|`"editable": true`|Will not mark uploaded values as immutable for web form users, i.e. they'll be able to overwrite what was uploaded.|
|`"return_data": true`|Will return the complete list of evidence stored against this record|
|`"return_data": "flat"`|As above but not-nested, so a note would be returned as `"c_hgvs.note":true`
|`"return_data": "changes"`|Returns only the evidence that changed as a result of your POST|

## ID Part
To uniquely identify the record, its ID can be part of the URL, or provided as part of JSON submission.

While we will assign a Shariant ID to all records, upon creation of a record you can assign it your own internal ID that only needs to be unique within your lab. You can then continue to use your internal ID for all future references.

The ID part of a submission consists of the following parts:

|Part|Description|
|----|-----------|
|lab_id|Identifier assigned to your lab, will be composed of the lab’s parent body and lab ID, e.g. `xyz_pathology/north_street_lab`.|
|lab_record_id|This is your internally unique identifier that can be any string. If no value is provided for the creation of a new record, a UUID will be automatically assigned.|
|rid|This is Shariant’s ID for the record. It can only be referenced for existing records and can not be dictated for new records. If provided then lab and lab_record_id should be omitted.|
|version|This will be a UNIX timestamp of the version when it was created. If the version is omitted then you will be dealing with the editable version of the record on a POST (if you have access), or the latest version your account has access to otherwise.|

e.g.

```json
{"id":"xyz_pathology/north_street_lab/F03432.1557189685.485863"}
```
or
```json
{"id":{
	"lab_id":"xyz_pathology/north_street_lab",
	"lab_record_id":"F03432",
	"version":1557189685.485863
}}
```

## Versions
Any change to the evidence of a record will automatically create a new version of that record.

A version is denoted by the UNIX timestamp (with decimal places) of when the record was altered.
If a value of version is provided in the ID part, then you will be referring to the read only version of the variant classification at that point in time and won’t be able to perform any operations against it.
Versions cannot be un-published after being published, but more up to date versions can be published to become the new default.

## Evidence Operation

Evidence part can be provided under one of the following. A submission can only provide a maximum of one of these elements at a time.
### create
Provide evidence for a new record. Will error if the ID part matches an existing record.

### patch
Evidence included in this will be merged with the existing evidence of a record. Will error if the ID part doesn’t match an existing record.

### upsert or data
Will either act as create or patch depending on if the ID part matches an existing record.

It is suggested that you only submit with upsert, as it stops labs from having to keep track of if a record has already been submitted.

### overwrite
Like upsert, except all existing evidence (if any) will be overwritten.

## Evidence Format
The content of create/patch/overwrite/upsert will be using keys as seen in the evidence keys section, with keys matching a value or a dictionary with a key of value or note.
Notes allow you to associate arbitrary text with an evidence key,  especially useful for boolean or (multi)select fields.

The evidence itself should in the form of  `key : value`
or `key: { “value”: value, “note”: note}`
e.g.
```json
{
    "id": "...",
	"upsert": {
		"literature": "Found a book PMID: 342244",
		"affected_status": {
		    "value": "yes",
		    "note": "Need to double check this"
		},
		"condition": {
		    "value": null
		},
		"search_terms": null
	}
}
```

How the data is provided is important for mixing the use of API and the web form.
By default, any key with anything on the right hand side other than a straight `null` will be immutable on the web form.
This is because your own curation system is deemed to be the source of truth about a variant classification. We want to avoid a scenario where users fix data on Shariant and then your curation system is out of date. This could be followed by another sync operation where the curation system's out of date data then upsets over the top of the correct data in Shariant.
The selective immutability will allow web form users to provide values for keys that your curation system can’t provide, if necessary.
Importantly, a web user’s ability to change the text for a “note” is not affected by the immutability status.

### Formats

`key : null` This completely blanks out any value associated with the key. Value, note, explain will be blanked. Web form immutability will be set unless otherwise configured.

`key : <value>` This will set the value for a key as well as wiping any note. Web form immutability will be set unless otherwise configured.

`key : { "value": "<value>", “note”: "<note>", "explain": "<explain>" }` If only a subset of value, note or explain are provided, this will merge with existing data. e.g. only providing value will leave any existing note and explain untouched. Immutability will be set.

The preferred method is `key: {“value”: x}` (with note only if your curation system can send notes). For records that don’t have values for certain keys that you would normally sync, provide `key: null` instead of omitting the entry all together. This is so immutability is set appropriately.

### Values

The individual entries valid for values will depend on the associated key types,
e.g. "BP4" accepts "NM", "BS", "BP", <etc>, true
	
"variant_type" accepts "indel", "splice_site" etc

"mode_of_inheritance" accepts ["autosomal_dominant","other"] or "autosomal_dominant, other"

See the [Evidence Key Types](../evidence_keys/types) page for more details.

## Sharing
You can provide a publish flag in a POST. If create/patch/overwrite/upsert is provided, the publish will relate to the record as it is after applying that change.
Note that you cannot un-publish a version, just publish more up to date versions.

To publish include a value for publish in your JSON body.
e.g.
```json
{
	"id": "67",
	"publish": "institution"
}
```
### institution
Visible to any user that belongs to a lab that belongs to the same institution as the lab the record was created against.

### logged_in_users
Visible to all logged in Shariant users and will be included in Shariant exports to other labs around Australia.

### global
Allowed to be shared with Clinvar or other 3rd party systems.

Each share level is inclusive of all previous share levels. If on Monday you published a record to level 3, then on Tuesday you published the same record to level 2 - general Shariant users will have read-only access to the record as it was on Monday, but users within your institution will have access to the more up to date version as it was on Tuesday.

## Deleting / Withdrawing

Records that haven't been shared with logged in users or global can be deleted by including
`"delete": true`

Records that have been shared with logged in users or global can be withdrawn by including the same
`"delete": true`

Withdrawn records:
Can be "unwithdrawn" with a subsequent submission for the ID that doesn't have `"delete": true` or via the dashboard within the application.
Do not show up in exports.
Do not show up in classification searches (unless searching for the ID).
Do not count towards discordance calculations.
Will still be accessible using their ID, and will still appear in historical discordance reports that they were previously involved in.

## Bulk POST
To perform multiple operations in one call, simply post a JSON array instead of a dictionary, e.g.
```json
{
	"records":[
		{"id":77, "patch": {"ps1":"NM"}},
		{"id":78, "delete": true},
	]
}
``` 
Though it is best if this is batched to no more than 20 operations per POST.
