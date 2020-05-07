# Gene / Transcript / Build issues FAQ

## Q. How do genes and symbols work?

RefSeq and Ensembl curate genes and transcripts, giving them stable identifiers (such as ENSG00000139618) and versions.

Gene symbols (eg BRCA2) are decided by committees - eg HUGO / HGNC for human. A gene version has an assigned symbol, but this changes over time

## Q. Why are some gene/transcripts only available in certain genome builds?

Transcripts releases are made frequently (RefSeq is on version 99 and Ensembl version 100 as of May 2020) but new transcripts are only aligned to the latest build. Here are build release dates:

|Build | Released | Last Update |
|------|----------|-------------|
| GRCh37 | 2009/02/27 | 2013/06/28 (p.13) |
| GRCh38 | 2013/12/17 | 2019/02/28 (p.13) |

So all gene/transcript versions released since 2013/06/28 are not available for GRCh37

Obsolete transcript versions are not mapped to new builds, so all gene/transcript versions replaced between 2009-2013 are available in GRCh37 but not GRCh38.

## Q. Why do gene names change between genome builds?

A gene version has a fixed gene symbol, independent of build, eg ENSG00000164199 version 11 has the symbol 'GPR98', while in version 18 it is “ADGRV1”
However, as per above, the versions of genes and transcripts available for a build will differ, so ENSG00000164199 is 'GPR98' in GRCh37 but ADGRV1 in GRCh38

## Q. Why does the same gene/transcript version have different exons in different genome builds?

Transcripts are worked out as mRNA then aligned back against the genome builds to find the exon coordinates. If genome builds differ at that gene, for instance inserting or deleting sequence, or base changes altering splice sites, then exon lengths or ends can change.

