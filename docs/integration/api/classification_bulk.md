# API Variant Classification BULK GET, POST

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

## Bulk GET
To perform a bulk export request a GET to `https://shariant.org.au/variantclassification/api/classifications/record/`

URL parameters include

Parameters

|parameter|value|description|
|---------|-----|-----------|
|level|editable|Will return records the current user has write access to and will be the latest version of those records including unshared changes.|
|level|public|Will only return records that have been published to be shared with 3rd party labs|
|level|loggd_in_users|Will only return records that have been published to be shared within Shariant|
|output|json|(Default) Output will be an JSON object with a key "records' containing all the relevant records.|
|output|csv|Output will be a CSV file.|
|output|redcap|Output will be a CSV file structured for REDCap. Note that only records with a value in redcap_record_id will be included.|
|group_by|_any_|If group_by has a value set then a zip file will be produced. Each group will be a json array of CSV file based on the output. e.g. `?group_by=variant` If omitted then the output will be a single CSV or JSON array file.|
|group_by|all|Places all the variant classifications in a single zip entry|
|group_by|none|Places each of the variant classification in a separate zip entry the entries named by lab identifier / lab record id|
|group_by|variant|Creates one zip entry per variant, the entry will have Shariant's internal ID|
|limit|_number_|Limits the number of rows returned. Warning, if grouping will limit the number of records randomly across different groups, so should be avoided in such a case|
|after|_unix timestamp_|If after has a value, only records that were last shared after will be returned. Be careful that this refers to the time the record was published, NOT the date of the last modification|