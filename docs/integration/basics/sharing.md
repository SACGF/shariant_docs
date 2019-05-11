# Variant Classification Sharing

Shariant has the following concepts for handling who has access to what

|Body|Meaning|
|----|-------|
|Organisation|Aka Institution (eg SA Pathology, VCGS) |
|Lab|Lab in an organisation (eg SA Pathology’s Familial Cancer, Frome Road) |
|User|Each lab member should have their own login. The sync tool will have a separate account. |
|Variant Classification|A variant classification will be owned by a user and a lab |

A user can belong to multiple labs, though typically a user will only belong to one. Please contact us when a staff member leaves your lab and we can disable access to your lab's records.

Variant Classifications can be seen in two modes.

* The live editable copy (there is only 1 of these)
* A read-only version shared at a given point in time

There can be multiple read-only versions for each live editable classification.

If you or someone from your lab created a variant classification, you will be dealing with editable copy.
If someone from outside your lab shares a record with you, you will be dealing with the specific version that they deemed to share. If they make changes and share it again, you will then have access to the new version. The same applies when you share records with them

Users with access to the editable version can elect to share the record in its current state as long as there are no outstanding validation errors. This will give other users read only access to the data as it is when the publish action was performed.

Sharing can be done at several levels. Each level encompasses the level before it, and once it's shared at a certain level it can only be shared at that level or higher in future. The share levels are:

|Share Level|Who Can See|
|-----------|-----------|
|Lab|Will be available to the lab|
|Organisation|Every lab belonging to the institution/organisation that the owning lab belongs to can see this version|
|All Shariant Users|All Shariant users will be able to see this version|
|3rd Party Databases|This version is deemed ready to be exported to 3rd party databases such as Clinvar|

See the Sharing section in the API for information on how to utilise these share levels.

The purpose of Shariant is to share records. The lower share levels are intended for records that are awaiting review or more information - not as a permanent half sharing state, and the system will automatically share records to other labs within Shariant after 6 months to ensure progress down the Sharing lifecycle.
