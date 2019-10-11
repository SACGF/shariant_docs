# API External References

Shariant parses all submitted values and note fields looking for external reference patterns (such as PMID).
e.g.

"See the paper PMID:123456 about this"

Would parse out a reference to PubMed
```
{
"value": "See the paper PMID:123456 about this",
"db_refs": [{
    "db": "PubMed",
    "id": "PubMed: 123456",
    "idx": "123456",
    "url": "https://www.ncbi.nlm.nih.gov/pubmed/?term=123456",
    "internal_id": 50165
}]
}
```

These values will be formatted into a specific structure on download, but for upload they just need to be in the format of REF_TYPE:REF_NUMBER.

There is some leeway on the formatting, e.g. for PMID the following are allowed
PMID:123456
PMID123456
PMID 123456
PMID#123456
PMID 123456,6543321
pmid 123456
Typically it's the case insensitive key term followed by any number of spaces, hashes or colons and then the refereced id.
Some terms do allow a comma separated list of values, but this is not preferred.

As of October 2019 the following are supported:

|ref type|term|example reference|resulting URL|
|--------|----|-------|------------|
|ClinGen|CA|CA123456|http://reg.clinicalgenome.org/redmine/projects/registry/genboree_registry/by_caid?caid=CA123456|
|Clinvar|VariationID|VariationID:12345|https://www.ncbi.nlm.nih.gov/clinvar/variation/12345/|
|COSMIC|COSM|COSM112085121|https://cancer.sanger.ac.uk/cosmic/mutation/overview?id=112085121|
|GTR|GTR|GTR:516181|https://www.ncbi.nlm.nih.gov/gtr/tests/516181/|
|HPO|HP or HPO|HPO:0001631|https://hpo.jax.org/app/browse/term/HP:0001631|
|MedGen|MedGen|MEDGEN:12345|https://www.ncbi.nlm.nih.gov/medgen/?term=12345|
|NCBIBookShelf|NCBIBookShelf|NCBIBookShelf:NBK11530|https://www.ncbi.nlm.nih.gov/books/NBK11530/|
|NIHMS|NIHMS|NIHMS:123456|https://www.ncbi.nlm.nih.gov/pubmed/?term=NIHMS123456|
|OMIM|OMIM|OMIM:115500|https://www.omim.org/entry/115500|
|PMC|PMCID|PMCID:1234567|https://www.ncbi.nlm.nih.gov/pubmed/?term=PMC1234567|
|PUBMED|PUBMED or PMID or PubMedCentral|PMID:123456|https://www.ncbi.nlm.nih.gov/pubmed/?term=123456|
|SNP|rs|rs123456|https://www.ncbi.nlm.nih.gov/snp/rs123456|
|UNIPROTKB|UNIPROTKB|UNIPROTKB:P30440|https://www.uniprot.org/uniprot/P30440|