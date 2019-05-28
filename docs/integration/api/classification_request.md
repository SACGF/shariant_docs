# API Variant Classification GET/POST
All operations against a variant classification submission from your lab can be performed against a single end point.

That end point being
https://shariant.org.au/variantclassification/api/classifications/record/

## Example Post

```json
{
	"id":"xyz_pathology/north_street_lab/F03432",
	"upsert": {
		"c_hgvs": "NM_032119.3:c.4171G>A",
		"clinical_significance": "VUS",
		"bp4": true,
		"mode_of_inheritance": ["autosomal_dominant", "autosomal_recessive"],
		"literature": "Found a book PMID: 342244"
	},
	"publish": "institution",
	"editable": true,
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

## Example GET

`https://shariant.org.au/variantclassification/api/classifications/record/xyz_pathology/north_street_lab/F03432?data=flat&config=true`

## All Parameters

|POST|GET|Effect|
|----|---|------|
|"id":_xxx_|in URL|See Id Part|
|"create":{} _or_ "patch":{} _or_ "overwrite":{} _or_ "upsert":{} _or_ "data":{}|N/A|See Evidence Operation|
|"publish":"_level_"|N/A|see Publish|
|"delete":true|N/A|See Deleting |
|"test":true|N/A|The effects of your POST operation will not be saved on the server. This is handy for validation.|
|"config":true|?config=true|Will return your lab’s evidence key configuration that will be merged with the default configuration for the web form. For the sake of syncing data, ignore this option.|
|"editable": true|N/A|Will not mark uploaded values as for web form users, i.e. they'll be able to overwrite what was uploaded.|
|"return_data": "true"|(default)|Will return the complete list of evidence stored against this record|
|"return_data": "flat"|?data=flat|As above but not-nested, so a note would be returned as `"c_hgvs.note":true`
|"return_data": "changes"|N/A|Returns only the evidence that changed as a result of your POST|

## ID Part
To uniquely identify the record, its id can be part of the URL, or provided as part of JSON submission.

While we will assign a Sharint ID to all records, upon creation of a record you can assign it your own internal ID that only needs to be unique within your lab. You can then continue to use your internal ID for all future references.

The ID part of a submission consists of the following parts:

|part|description|
|----|-----------|
|lab_id|identifier assigned to your lab, will be composed of the lab’s parent body and lab id, e.g. `xyz_pathology/north_street_lab`.|
|lab_record_id|this is your internally unique identifier that can be any string. If no value is provided for the creation of a new record, a UUID will be automaticall assigned.|
|rid|this is Shariant’s id for the record. It can only be referenced for existing records and can not be dictated for new records. If provided then lab and lab_recordid should be omitted.|
|version|This will be a UNIX timestamp of the version when it was created. If version is omitted then you will be dealing with the editable version of the record on a POST (if you have access), or the latest version your account has access to otherwise.|

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
If referring to this information in the URL instead of JSON, it will be in the form of 
<div style="font-size:10pt">
`https://shariant.org.au/variantclassification/api/classifications/record/[lab]/[lab_record_id](.version)` where the (.version) is optional
e.g.
`https://shariant.org.au/variantclassification/api/classifications/record/xyz_pathology/north_street_lab/F03432.1557189685.485863`

OR

`https://shariant.org.au/variantclassification/api/classifications/record/[rid](.version)` where the (.version) is optional
`https://shariant.org.au/variantclassification/api/classifications/record/1453.1557189685.485863`
</div>

## Versions
Any change to the evidence of a record will automatically create a new version of that record.
(The exception being if multiple changes are done to a record by the same user in the same method within one minute, those changes will be merged into one version).

A version is the UNIX timestamp (with decimal places) of when the record was created.
If a value of version is provided in the ID part, then you will be referring to the read only version of the variant classification and won’t be able to perform any operations against it.
Versions can un-published after being published, but more up to date versions can be published to become the new default.

## Evidence Operation

Evidence part can be provided under one of the following. A submission can only provide one at most of these elements at a time.
### create
Provide evidence for a new record. Will error if the id part matches an existing record.

### patch
Evidence included in this will be merged with the existing evidence of a record. Will error if the id part doesn’t match an existing record.

### overwrite
Like patch, except all existing evidence will be overwritten.

### upsert or data
Will either act as create or patch depending on if the id part matches an existing record.

It is suggested that you only submit with upsert, as it stops labs from having to keep track of if a record has already been submitted.

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
This is because your own curation system is deemed to be the source of truth about a variant classification. We want to avoid a scenario where users fix data on Shariant and then your curation system is out of date. This could be followed by another sync operation where the curations out of data data then upsets over the top of the correct data in Shariant.
The selective immutability will allow web form users to provide values for keys that your curation system can’t provide if necessary.
Importantly web user’s ability to change the text for a “note” is not affected by the immutability status.

### Formats

`key : null` This completely blanks out any value associated with the key. Value, note, immutability will all be reset.
`key : value` This will set the value for a key as well as wiping any note. Web form immutability will be set unless otherwise configured.
`key : { “value”: "<value>", “note”: "<note>" }` If only value or note are provided, this will merge with existing data. e.g. only providing value will leave any existing note untouched. Immutability will be set.

The preferred method is `key: {“value”: x}` (with note only if your curation system can send notes). For records that don’t have values for certain keys that you would normally sync, provide `key: {“value”: null}` instead of omitting the entry all together. This is so immutability is set appropriately.

### Values

The individual entries valid for values will depend on the associated key types,
e.g. "BP4" accepts "NM", "BS", "BP", <etc>, true
"variant_type" accepts "indel", "splice_site" etc
"mode_of_inheritance" accepts ["autosomal_dominant","other"] or "autosomal_dominant, other"
See the Evidence Key Type page for more details.

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
Visible to any user that belong to a lab that belongs to the same institution as the lab the record was created against.

### logged_in_users
Visible to all logged in Shariant users and will be included in Shariant exports to other labs around Australia.

### global
Allowed to be shared with Clinvar or other 3rd party systems.

Each share level is inclusive of all previous share levels. If on Monday you published a record to level 3, then on Tuesday you published the same record to level 2 - general Shariant users will have read-only access to the record as it was on Monday, but users within your institution will have access to the more up to date version as it was on Tuesday.

## Deleting

Records that haven't been shared with logged in users or global can be deleted by including
`"delete": true`
