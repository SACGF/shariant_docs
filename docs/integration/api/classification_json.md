# API Variant Classification JSON

An example of the result of a GET or POST below

```json
{
    "id": 31,
    "meta": {
        "lab_record_id": "77",
        "institution_name": "SA Pathology",
        "lab_id": "sa_pathology/unit_1",
        "lab_name": "SA Pathology Unit 1",
        "title": "SA Pathology Unit 1 31",
        "user": "varadmin",
        "version": 1544864360.852882,
        "can_write": true,
        "can_write_latest": true,
        "flag_collection": 13,
        "has_changes": true,
        "last_edited": 1553238219.242146
    },
    "allele": {
        "clingen_allele_id": "CA396457842",
        "genome_builds": {
            "GRCh37": {
                "variant_coordinate": "16:68842599 A>G",
                "g_hgvs": "NC_000016.9:g.68842599A>G",
                "c_hgvs": "NM_004360.4(CDH1):c.535A>G",
                "origin": "Imported as this build",
                "variant_id": 535913
            }
        }
    },
    "publish": "logged_in_users",
    "data": {
        "age": {
            "value": "76"
        },
        "g_hgvs": {
            "value": "NC_012980.1:m.1898A>G"
        },
        "sample": {
            "value": "blood"
        },
        "zygosity": {
            "value": "heteroplasmic",
            "note": "xyz"
        }
    },
	"messages": [
        {
            "key": "clinical_significance",
            "code": "mandatory",
            "message": "Missing mandatory value",
            "severity": "error"
        }
    ],
}
```

|key|meaning|
|---|-------|
|can_write|Can the current user perform modification operations on this record. Note if the record was requested with a version, can_write will always be false.|
|can_write_latest|If you are viewing a classification at a specific version, would the user be able to edit the working copy for this classification.|
|data|Is present by default on a GET but not on a POST. The complete set of evidence saved against this record. Format/Contents can be changed by using return_data in POST or data in GET|
|flag_collection|Id for as the yet unpublished flag API (used for discordance resoluton and notifications)|
|id|This is the Shariant ID, referred to as `rid` in other contexts.|
|institution_name|English friendly name of the institution/organisation which the lab belongs to.|
|lab_id|How the lab should be referred to via API. Will be in the form of instiution_id/lab_part_id|
|lab_name|English friendly name of the lab which the record belongs to.|
|lab_record_id|The id the lab associated with this record.|
|last_edited|The date (in unix time) when the working copy of the record was last edited|
|messages|Any validation messages associated with the data of the record.|
|title|English friendly title of the record. Does not refer to the variant or the classification.|
|user|The Shariant user that owns this record.|
|variant|Chromosome, Position, Ref and Alt|
|variant_id|Shariant's internal database id for this record (It wont be meaningful outside of Shariant)|
|version|The version we're looking at. It will be the unix time when the record was edited before it was submitted, NOT the time it was submitted. e.g. if you edited the record on Jan 1st and submitted it on Feb 2nd, the version will be the unix time for Jan 1st|