# Evidence Keys Overview

A variant classification in Shariant is mostly comprised of evidence key values.

[Evidence keys can be viewed here](https://shariant.org.au/classification/evidence_keys)

Extra details

* Evidence keys are flat, e.g. a key will not be nested within another key.
* Each key is of a certain type, see [Evidence Key Types](types.md).
* Each evidence key allows for a free text "note". Use notes to include extra details, especially when the evidence key itself has to conform to a certain format, e.g. `{"bp2":{"value": true, "note": "Was 50/50 on this one"}`
* Each evidence key allows for a free text "explain". Use explains to include details about how your lab uses that field if it differs (or is more explicit) than the ACMG guidelines, e.g. `{"pm2":{"value": false, "note": "absent from gnomAD, other pop databases are not used"}`
