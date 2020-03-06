# Evidence Key Types

A key's value type will determine how it will behave:

### (F) free-text
Free text, no default validation applies, avoid new line characters if possible.

Any HTML tags will be stripped out.

### (T) free-text multi-line
Free text, no validation applies, can contain new line characters and the following basic HTML elements:
```
<br>
<b>
<i>
<ol>
<ul>
<li>
<u>
```

### (S) select
The key will also contain an array of options. To submit a value, provide a value that matches an option's key. If the entry also has `allows_custom_values` then any value will be accepted.

### (M) multi-select
As per the normal select, the key should also contain an array of options. To submit a value, provide either a json array or a comma separated string. The elements in the array or string should match the keys of options. If the entry also has `allows_custom_values` then any value will be accepted, and standard values and custom values can be intermixed.
The ordering of values from submission will not be maintained.

When viewing records, the value will be an array of option keys, unless there were no values selected in which case the value will be `null`.

### (B) boolean
Provide a json boolean value, or alternatively "true" or "false" case insensitive.
Be aware that the web form is unable to distinguish between false and no value.

### (D) date
Provide a string in the format of yyyy-MM-dd e.g. Jan 2nd 1997 would be "1997-01-02". Time parts are not supported.

### (C) criteria
An ACMG criteria e.g. PVS1, PS1, PS2. Accepts values of
* `NM` for Not Met
* `BS` for Benign Strong
* `BP` for Benign Supporting
* `BA` for Benign Standalone
* `PP` for Pathogenic Supporting
* `PM` for Pathogenic Moderate
* `PS` for Pathogenic Strong
* `PVS` for Pathogenic Very Strong
* `true` for the default strength of of the criteria

### (L) float
_sorry (F) was taken_ accepts any number, if valid will be stored as a float.

### (I) integer
Accepts any whole number, if valid will be stored as an int.

### (N) unit
Accepts a number between 0 and 1, if valid will be stored as a float.

### (P) percent
Has been deprecated in favour of always using unit.
~~Accepts a number between 0 and 100, if valid will be stored as a float~~

### (U) user
Provide the email address of a user. Typically this will be for the owner of a record, in which case it's more important for it to be the user who will login to the system to fix the issues rather than the person who created the classification.
