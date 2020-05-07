# Shariant Frequently Asked Questions

## What is Shariant?
Shariant is a controlled access platform designed to allow Australian laboratories and clinical services to: automate sharing of detailed and structured scientific evidence about clinically curated variants; communicate in real-time to resolve variant interpretation differences; and access gene- and disease-focussed expertise.

By sharing, key variant information will be provided to laboratories, and also clinical services, to help them better interpret genomic tests and improve the outcomes of testing for Australian patients. 

To do this Shariant stores:
* Genomic coordinates of a curated variant 
* Clinical significance of the variant (e.g. Pathogenic, Benign)
* Structured evidence that was used to determine the clinical significance
* Brief details of the condition and phenotype 
* Technical details of the test used to detect the variant
* Contact details for the curating laboratory
* Updates that have occurred regarding a specific variant (e.g. from Shariant discordance resolution)

Shariant does/will not:
* Store genomic data files (e.g. BAM, VCF files)
* Replace a laboratory’s existing curation tool 

The information in Shariant is stored under controlled access, meaning it is limited to those who are experts in the field. Some of the information can subsequently be made public and shared with international databases, if approved by the submitting laboratory, to enable any patients undergoing genomic testing, worldwide, to benefit from the information.

During Phase 1, Shariant will provide many features to help laboratories manage these variants, including:
* Automated upload to Shariant and download to laboratory curation software
* Capture of detailed and structured evidence used to determine clinical significance
* An automated notification system to alert users to clinically important classification discordances
* An in-built communication platform to resolve classification discordances between laboratories
* Semi-automated submission of summary information to ClinVar to share internationally (upon laboratory approval)
* A web form for manual curation and input of a selected variant


* Checks to make sure that the variant naming and coordinates map correctly to international standards
* Audit trails to allow laboratories to monitor and trace user activity.
It is anticipated that more features will be developed and made available in Phase 2 of Shariant. Please contact the Shariant team for more information ( [communications@shariant.org.au](mailto:communications@shariant.org.au) ).

## Why is Shariant being developed?
Decoding the clinical significance of DNA variants is complex and challenging, and is impeded by operation of clinical laboratories as data silos. It is currently difficult for one Australian laboratory to know if others hold evidence to support or refute the clinical impact of a variant they have assessed. Failure to share information leads to the risk of missing a diagnosis or misclassifying a variant.

Shariant is being developed to unite these data silos, and provide key variant information to laboratories, to help them better interpret genomic tests and improve the outcomes of testing for Australian patients. Additionally, Shariant will assist laboratories in meeting the National Pathology Accreditation Advisory Council (NPAAC) and Royal College of Pathologists of Australasia (RCPA) recommendations for submission of genotypic data to clinical databases.

Shariant aims to share information about clinically curated variants to:

* Combine siloed information and expertise for increased and faster diagnoses across Australian laboratories, for targeted treatment and better health care of patients and their families
* Reduce the risk of variant misclassification by allowing laboratories to identify potential interpretation differences before they occur
* Streamline communication between laboratories via an in-built communication platform
* Standardise and improve practices, information and terminology relating to genomic information across Australia, providing greater consistency in how we diagnose and treat diseases
* Facilitate knowledge transfer between the Australian clinical genomics community and international data sources, benefiting patients in Australia and globally.

Most importantly, Shariant is designed to assist healthcare professionals deliver better genomics results. If you have suggestions for how Shariant might be helpful to you, please let the Shariant team know ( [communications@shariant.org.au](mailto:communications@shariant.org.au) ).

## Who is behind Shariant?
Shariant is an Australian Genomics initiative, run under its national project on Clinical Variant Classification and Sharing led by Amanda Spurdle at QIMR Berghofer Medical Research Institute. The project was established in response to an identified need, from Australian Genomics’ member organisations and Australian clinical genetic testing laboratories, for assistance in meeting the growing technical and administrative requirements for clinical data sharing. 

The Shariant platform is based on existing software, 'VariantGrid.com', developed by David Lawrence at the Centre for Cancer Biology, an SA Pathology and University of South Australia Alliance.

The key personnel involved in Shariant are:
* Amanda Spurdle (Project Lead, QIMRB, QLD)
* Emma Tudini (Project Coordinator, QIMRB, QLD)
* David Lawrence (Lead Developer, CCB, SA)
* James Andrews (Software Developer, CCB, SA)
* Sarah King-Smith (Reclassification, CCB, SA)

Shariant is supported by both Australian Genomics and the Centre for Cancer Biology. 

## What is the advantage of submitting to Shariant over only submitting variants to ClinVar?
Shariant offers additional features to the international database, ClinVar, including:
* Collection, storage and sharing of detailed curation evidence against ACMG criteria in a structured format 
* Sharing of this detailed curation evidence in a controlled access manner between Australian laboratories and clinicians first, bypassing potential issues of displaying data in a publicly accessible databases and sending data overseas
* A notification service alerting laboratories to potential discordances between laboratories or changes in classifications
* An in-built communication platform to assist in the resolution of discordances
* A central administrative node for submission to external databases (such as ClinVar) upon laboratory approval, reducing the technical and logistical burden associated with managing upload of data to databases and preventing laboratories from duplicating this process. 

Shariant is also streamlining the process of submitting to ClinVar, enabling laboratories to do so in a semi-automated manner, at their discretion. 

## Who can access the data?
Shariant is a controlled access platform. Therefore, access to Shariant is restricted to experts in the field and managed via Australian Genomics. Users must agree to the [terms of use](terms_and_conditions.md), which includes clauses to forbid data re-distribution, and requires approval to publish findings using data obtained from Shariant.

Upon laboratory approval, clinically curated variants and associated evidence will be submitted to external databases (such as ClinVar). These external databases may be public (no login required) and can therefore be accessed by anyone with internet access. 

## Do we have to change how we perform variant curation?
No. Shariant simplifies the sharing of curated variants for laboratories, with little disruption to their current workflow. Laboratories can continue to use their existing curation systems such as Agilent Alissa, Golden Helix or a custom curation tool. Shariant will connect to each existing curation tool via an Application Programming Interface (API) to allow for automated submission to Shariant. Information shared in Shariant will then be available for download into a laboratory’s existing curation system. 

A web form is available to enter or edit classifications manually (for instance, if a laboratory wished to enter data by hand from paper records) but for many laboratories this is unnecessary.

## How much does Shariant change my laboratory’s clinical curation workflow?
Shariant maximises the benefits of sharing and discordance resolution, while minimising changes to workflows.

Sharing variant classifications and associated evidence is performed behind the scenes for most users, so that no additional steps are needed to share variants. The main difference is that classifications from other Australian laboratories will now be visible inside their curation system, so they will be aware when a variant has been seen before, and can re-use the expertise and effort of others. Laboratories will be sent discordance notifications if any variants they have classified have been given a different clinical significance by other laboratories.

## How is data shared with my laboratory’s curation system?
We work with your laboratory to build a small tool that runs on your intranet and automatically shares classifications between your curation tool and Shariant.


We are working with Agilent, Golden Helix and the pilot laboratories to build these connector tools. All programs built will be open source and available on GitHub, allowing laboratories to audit them. All communication will be driven by the client and the laboratories will deploy the client tools themselves, following internal security practices. For more information please see the  [Shariant help guide](https://shariant.readthedocs.io/en/latest/integration/basics/getting_started.html) .

## How does sharing data between different curation systems work?
Australian Genomics surveyed Australian NATA-accredited diagnostic genetic testing laboratories, and found almost all use the  [American College of Medical Genetics and Genomics (ACMG)/ Association for Molecular Pathology (AMP)](https://www.nature.com/articles/gim201530)  or ACMG/AMP-like guidelines. Our data collection is based around these guidelines, and we collect:
* An internal laboratory identifier (to track or modify the classification)
* A way to uniquely identify a variant (HGVS nomenclature or genomic coordinates)
* Clinical significance (Pathogenic to Benign)
* Condition
* All 28 ACMG criteria (BS1, BS2, PM5, etc)
* Evidence used to support the evaluation.
Sharing detailed curation evidence in a structured way gives Shariant an edge over other sharing tools. Comparing a variant’s classification and associated evidence is as simple as looking at which ACMG criteria have been interpreted differently or whether extra hidden evidence exists.

## What kind of evidence can I store against my classification?
Laboratories can submit any evidence they want.

The goal is to balance keeping evidence structured while also accepting all the different types of evidence that exist (e.g. databases, websites, bioinformatic prediction tools) - some of which haven’t been released yet!

Thus, each piece of evidence requires a name, section, version and value (eg “gnomAD”, “Population Data”, “2.0.2” and “0.01”). For evidence names, laboratories should strive to re-use existing keys so that they match between laboratories. Sections are from the ACMG/AMP guidelines that group criteria into sections such as “Population Data”, “Computational and Predictive Data” and “Functional Data”. This helps to show the relevant data when comparing classifications between different laboratories.

For more information please see the  [Shariant help guide](https://shariant.readthedocs.io/en/latest/integration/basics/getting_started.html) .

## I work in a private laboratory, can my laboratory participate?
Yes. Shariant aims to connect to all interested Australian NATA-accredited genetic testing laboratories, regardless of whether a laboratory is public or private. Prioritisation of laboratories for connection to Shariant will be based on the following criteria:


* Interest of the laboratory
* Ease of connection to the laboratory’s curation system
* Testing output of the laboratory
* Whether a laboratory is public or private

Please contact the Shariant team, if you are interested in connecting to Shariant ( [communications@shariant.org.au](mailto:communications@shariant.org.au) ).

## What is the timeframe for the development of Shariant?
Shariant is currently under rapid development, with new features being added each week. A beta-version of Shariant will be released for pilot testing in June 2019. After three laboratories have been successfully linked to Shariant, the platform will be rolled out nationally at all other interested Australian laboratories. Full technical support will be provided to assist laboratories connect to the platform.

Please contact the Shariant team if your laboratory has expertise in variant curation and is interested in testing the beta-release of Shariant.

## How are Shariant and VariantGrid related?

[VariantGrid](https://variantgrid.com) is a variant database and web analysis platform, and is the technology licenced by Australian Genomics to build Shariant.

