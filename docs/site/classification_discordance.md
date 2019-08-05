# Classification Discordance

## Terminology

### Allele
Shariant refers to "alleles" as a way to join logically equivalent variants in different builds together.

e.g. `GRCh37 1:40773150 G>A` is linked to the same allele as `GRCh38 1:40307478 G>A`.

Discordance is applied across genome builds on alleles, so if your lab is using GRCh37 and another lab is using GRCh38 and if both labs have a classification that is logically referring to the same variant, then discordance calculations will consider both of those classifications together.

### Clinical Groups
Clinical groups are used to subdivide classifications within an allele. In many cases there will be only be one "default" clinical group for an allele, but in the following scenarios you might need to make new ones:
* The conditions between the classifications is significantly different (e.g. "Tietz syndrome" vs "Carpenter syndrome")
* The transcripts are significantly different

In most cases the "default" clinical group per allele will be sufficient.

### Discordance
Two (or more) classifications are considered discordant if they:
* Belong to the same allele
* Belong to the same clincal group within that allele (including the "default" clinical group)
* Transcript & condition do not directly affect the calculation unless a human determines the differences in those values designate a different clinical group
* Are shared at the Shariant Users level or 3rd Party Database level
* Have clinical signifiances that fall into 2 or more of the following buckets (benign/likely benign), (VUS A/B/C), (likely pathogenic/ pathogenic), risk factor . e.g. likely benign is discordant with VUS, but likely benign is concordant with benign.

## Discordance... Now what?

So if one of your classifications meets the discordance criteria with another classification, what happens next?

## Discordance Report

A good place to start is the Discordance Report. The Discordance flag will provide you a link to get to here.

![](images/discordance_report.png)

This shows you all:
When the discordance was first detected and why.
* The classifications that were involved at the start of this discordance.
* The state of the classifications at the beginning of the discordance.
* The state of the classifications as they are now (or after the discordance was resolved if it has been)
* A summary of actions taken against each classification.

### ![](images/work.png) Internal Review

When discordance is first detected, it is recommended practise to perform an internal review of the classification.

You can raise an internal review flag in "In Progress" and complete it later, or if you perform an internal review you can raise the flag as "Complete".
This will then show up in the report that an internal review has taken place.

For the actual performing of the internal review, the exact steps will be different for each organisation, but it should done as a double check as now somebody else came up with a different answer.

If the internal review found that some data should be changed, please change the record in your curation system and the update will be applied the next time your data in synced up.

Note that you are welcome to do (and record) Internal Reviews outside of discordance, though doing so is not required from Shariant.

### Who's in Charge / Responsible

The owner of the classficaton that triggered the discordance is seen as the primary person in charge of resolving discordance. Note that this is not enforced in Shariant, anybody is free to take the lead on this.

### Discordance Discussion

Once you've completed your internal review, you should investigate what other labs have provided for the same variant.

The diff page is a good place to do this as it shows all the details of the classifications that are involved in the discordance discussion. (The Discordance Flag will provide a link to this.)

See details [About the Diff Page here](classification_diffs)

See if there's any relevant data that other labs have included that your lab may have missed (e.g. internal laboratory assays from another lab). Likewise after reviewing details from another lab's classification, you can raise ![](images/lightbulb.png) "Suggestion" flags on their classifications.

When reviewing the other classification, keep in mind what flags they already have open and closed e.g. they may not have yet completed an Internal Review or there might be some previously recorded accepted and rejected suggestions.
Also keep if somebody has agreed to make a change, it may take some time for that change to be synced back up to Shariant.

### ![](images/exchange.png) Change of Clinical Significance

If as a result of an Internal Review, Suggestions or outside discussions you may have changed your Clinical Significance (hopefully towards concordance).
Whenever a classification is updated with a different clinical significance, a flag is automatically raised asking for the reason.
That reason will then be translated to the Discordance Report.
Note that even if the report has been closed, if you still have outstanding Clinical Significance Change flags you can still update them and it will be reflected.

### Withdrawing

If a classification that caused the discordance has been found to be in large error and shouldn't be considered in its current form, the owner of the classification may mark it as Withdrawn from the classification form.

Withdrawn classifications are not considered during discordance calculations.
(It will still appear on the report, but will be struck out to indiciate it is no longer considered.)

### Comparisons are not Relevant

If you determine you have two or more classifications that are discordant but for good reason, you can change the Clinical Grouping of the records.

For example, if a variation is Pathogenic for "Tietz syndrome" and benign for "Carpenter syndrome" you can divide classifications up into both.
To do so from the variant page, click "Change Clinical Grouping".

A column for clinical grouping will appear, any classifications that have the same text in that column will be considered in the same Clinical Grouping. Note that a Clinical Grouping is just a free text name and the classifications that belong to it.

Once you've updated it so classificaitons have the appropriate groupings, hit save. This may resolve (or cause) outstanding discordances.
It is suggested that if you do subdivide records, that you don't leave any in that variant in the "default" grouping for that Aalele.

### Concordance is Reached

If you or another lab changes
* Sub-divide classifications into more meaningful groupings. (should only be rarely required)
* Withdraw classifications that aren't in concordance. (should only be rarely required)
* Change clinical significances so all the remaining classifications are in the same clinical significance bucket.
Then you will have reached concordance and the discordance and report will automatically close. Congradulations.

### Stuck in Discordance

If after internal reviews and discussion, you have been unable to reach concordance, navigate to the Discordance Report page.

From here you can click "Unable to reach concordance".
Please only do this as a last resort. Note that if there are any changes to the Clinical Context (a new record is added or a record changes its significance) discordance will be re-opened and the report will report the starting state as it was when "Unable to reach concordane" was clicked.