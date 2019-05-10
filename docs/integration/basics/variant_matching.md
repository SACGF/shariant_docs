Variant Matching
==================================================

TODO : The exact shariant field combinations we would like

Scope
Shariant Variant Normalisation Process describes the variant normalisation protocol implemented for the Australian Genomics initiative, Shariant. It should be read in conjunction with Shariant Technical Overview.
Abbreviations

Introduction
A variant is composed of the reference, position within the reference, and the base change. Examples include HGVS [1] and the chrom/pos/ref/alt fields of a VCF file [2]. Below shows the same variant represented in different ways:

|Type|Example
|----|-------|
|HGVS coding DNA (c.)|NM_003607.3(CDC42BPA):c.325A>G|
|HGVS genomic (g.)|NC_000001.10:g.227400866T>C|
|VCF|1:227400866 T>C|

It is critical to assign variants to a unique identifier, so that it is possible to link variants from different sources, such as external population databases like gnomAD, to track observations from different VCFs, or classifications from different labs.
Difficulties and solutions
HGVS protein changes

Some medical scientists work with HGVS protein expressions (e.g. CDC42BPA:p.Asn109Asp). The issue with this notation is that there are often many different transcripts for a given gene, meaning the amino acid change could be at a different loci. There is the concept of “canonical transcripts” (a default transcript used when no transcript is specified) but canonical transcripts differ between labs and are often inconsistent over time.

Even if the canonical transcript is specified, codon degeneracy (redundancy of base changes leading to same amino acid) means the nucleotide-level change cannot be distinguished. Determining the specific nucleotide change may be necessary (e.g. splicing).

Shariant Solution: HGVS protein changes are collected as Evidence Keys in Shariant, but are not used to link a classification to a variant. A laboratory will be unable to submit a variant with the protein change alone.
VCF or HGVS g. do not specify transcript

Genomic coordinates (such as VCF or HGVS g. notation) can uniquely resolve the base level changes, but may have different protein changes if there are different transcripts. The choice of transcript is significant for curation (e.g. splicing, pathogenicity prediction tools).

Intergenic variants will not have a transcript.

Shariant Solution: It is strongly recommended that classifications submitted with VCF or HGVS g. Evidence Keys, also include the versioned transcript identifier used for curation. Classifications without a transcript will be linked, but a warning will be provided if a variant is inside a gene.
Ambiguous build or transcript versions

Not all VCF files specify the genome build. Some labs have stored classifications using VCF coordinates in custom databases but have not specified a build. Additionally, it is not always possible to check the build based on the variant submitted.

Labs that use HGVS coding DNA notation often store the transcript (e.g. NM_003607:c.325A>G) but not the transcript version (NM_003607.3:c.325A>G). While unlikely, it is possible that a variant in a different version of the same transcript may refer to different base changes.

Shariant Solution: Submission of a variant without a genome build being specified will not be allowed in Shariant and the record rejected. Additionally, submission as HGVS c. without a transcript version will be strongly discouraged. If a laboratory does not have a transcript version, then the latest version of a transcript will be used to load the variant, and a warning will be provided that this may not be correct.
Multiple representations within the same build
It is possible to describe a variant involving insertion and/or deletion in different ways for the same build or transcript versions. For instance, if the reference is “GGG” and a single G is deleted, this variant may be described as deleting either the first, second or third G. 

Conventions have appeared, such as representing the change in as few bases as possible, and left aligning (Tan et al [3] - which introduces a tool vt normalise)

Regardless of the convention choses, this must remain consistent. 

Below shows a table (from ClinGen Allele Registry [4]) of left and right aligned variants:

|Example Variant|Left Aligned|Right Aligned|
|---------------|------------|-------------|
|ACTG____TCGTG ACTGTAAGTCGTG|ACT____GTCGTG AACTGTAAGTCGTG|ACTGTAAGTCGTG ACTGT____CGTG|
|ACTGTCGTG ACTG___TG|ACTGTCGTG ACT___GTG|ACTGTCGTG ACTGT___G|
|GTTCACTGCTGCTGCATC GTTCACTG___CTGCATC|GTTCACTGCTGCTGCATC GTTCA___CTGCTGCATC|GTTCACTGCTGCTGCATC GTTCACTGCTGC___ATC|

Popular variant callers (such as GATK) produce VCF files which are not normalised, though it is quite common for pipelines to use VT normalisation to left-align VCF files.

HGVS nomenclature specifies right alignment. The table below (copied from ClinGen Allele Registry [4]) shows multiple HGVS expressions for the same change.

|HGVS expressions|Unique CAid|
|----------------|-----------|
|NM_000277.1:c.1200‐1delG NM_000277.1:c.1200delG|CA229394|
|NM_017739.3:c.1895+1_1895+4delGTGA NM_017739.3:c.1895+5_1895+8delGTGA|CA263965|
|NM_005228.3:c.2284‐6delCinsCTCCAGGA AGCCT NM_005228.3:c.2284‐5_2290dupTCCAGG AAGCCT|CA135833|

Shariant Solution: HGVS coordinates are converted into VCF coordinates, then all VCF (or VCF from HGVS) coordinates are run through VT normalise before linking to a variant.
Cross mapping between different genome builds

It is not always possible to lift-over all variants to another build, with rates of ~97% being commonly reported.

Newer builds have resolved some difficult sequences and introduced additional haplotypes (different reference sequences for regions of the genome that vary between human populations). Therefore, it may be possible that two distinct variants in one build liftover to become a single variant in another build, or vice versa. A naive liftover of two separate classifications from the same build may make those classifications discordant on another build.

Shariant Solution: The ClinGen Allele Registry will be used to solve this problem by providing a globally unique ID (CAid) which can link variants across different builds. When a classification is imported which resolves to a novel variant in Shariant, an API request will be made to the ClinGen Allele Registry to retrieve or create an CAid for this variant.

This variant classification discordance process implemented in Shariant will work against these CAids (please refer to Shariant Technical Overview). 

CAids can also be used as Evidence Keys to provide unambiguous linking of classifications to variants, and simplify submission to ClinVar.
References

[1] Dunnen, J. T., Dalgleish, R. , Maglott, D. R., Hart, R. K., Greenblatt, M. S., McGowan‐Jordan, J. , Roux, A. , Smith, T. , Antonarakis, S. E. and Taschner, P. E. (2016), HGVS Recommendations for the Description of Sequence Variants: 2016 Update. Human Mutation, 37: 564-569. doi:10.1002/humu.22981

[2] The Variant Call Format (VCF) Version 4.2 Specification https://samtools.github.io/hts-specs/VCFv4.2.pdf

[3] Adrian Tan, Gonçalo R. Abecasis, Hyun Min Kang; Unified representation of genetic variants, Bioinformatics, Volume 31, Issue 13, 1 July 2015, Pages 2202–2204, https://doi.org/10.1093/bioinformatics/btv112

[4] Pawliczek P, Patel RY, Ashmore LR, et al. ClinGen Allele Registry links information about genetic variants. Human Mutation. 2018;39:1690–1701. https://doi.org/10.1002/humu.23637