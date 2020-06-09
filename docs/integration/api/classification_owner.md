# API Variant Classification Owner

A classification is always assigned to a single user, as well as a lab.

In addition to the internal user of a classification, there's an evidence key called "owner".
If the value provided for "owner" is valid per the criteria below, the user of the record will be changed to it.
If no value is provided for "owner", the "owner" key and the internal user will both be set to the user who created the new classification (be it done over the web interface or using the API).

Criteria for owner:

* The value must be an email address.
* The email address must match an existing Shariant user.
* The user must have logged into Shariant at least once.
* The user must belong to the lab that the record is assigned to.

If a value for owner is provided that doesn't match the above criteria, a warning will be raised but there will be no other adverse effects.
