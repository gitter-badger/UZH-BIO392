# Genomic Variant Annotation Formats

## ISCN Report: used to report chromosomal abnormalities through cytogenetic techniques FISH, SKY and SNP arrays. 

* At least two patient identifiers: patient name and date of birth, gender (advised)
* Laboratory number
* Date of sample collection and date of receipt
* Type and origin of sample (i.e. fresh, fixed or frozen)
* Cell type if mutiple cell types were used
* Names and contacts of physician and other recipients scanning report
* Laboratory contact details
* Reason for referral
* Title
* Date of the report and (digital) signature of authorized person
* Overall result or conclusion, written description of the result
* A clear statement whether the test result is normal or abnormal
* A clear written description of the cytogenetic abnormality and the interpretation of the results of the analysis
* It should be stated whether the karyotype is male or female, unless the X and/or Y-chromosome are involved in an aberrant karyotype or no information is available about X and Y
* Clinically significant constitutional abnormalities including recommendations for genetic counseling should be provided where appropriate
* The association with prognosis in case a robust association in large published series of clinical trials (including literature reference) exists
* Any technical details relevant to interpretation must be made clear or the report should include a referral that the information is available upon request
* Where a cytogenetic abnormality of unknown significance is detected, the term “malignancy” should not be used in reports. Terms such as “clonal disease” or “neoplasm” are recommended instead
* The interpretation and reporting of loss of the Y chromosome or trisomy 15 can be problematic. Both features are seen in bone marrow cells of elderly patients with no hematological disease, but may \
also occur as markers of neoplastic clones
* When relevant the report should refer to previous genetic test results
* Normal karyotypic, FISH, and microarray results must always be regarded with suspicion, since malignant cells may be underrepresented in the tested sample (culture)
* If the proportion of malignant cells in the sample is unknown, this must be qualified to point out the possibility that the malignant clone was not represented in the analysis, i.e., the possibility \
of a false-negative result. In order to obtain information regarding the percentage of malignant cells, close collaboration with a pathologist or physician is recommended
* If commercially available kits, (FISH) probes, software packages (including version), or microarray platforms are used, then the manufacturer, kit number, and version number must be reported
* The technical sensitivity and practical resolution of the test must be provided where applicable
* The resolution of array platform as well as the practical resolution used for analysis to exclude benign constitutional variants (e.g., copy number aberrations >5 Mb) should be provided
* Limitations of the test or where the minimal quality or requirements are not achieved, should be stated. Limitations of the microarray test, including cut-off levels for the detection of mosaicism \
and  a statement that the test will not detect point mutations and balanced rearrangements and, for some platforms, polyploidy and copy neutral loss of heterozygosity should be provided
* For microarray studies, relevant genes located within the interval of aberrations that are known to be associated with the disorder stated in the referral or have possible prognostic or predictive \
implications should be reported.
* Integrated reporting of results for a patient is encouraged. This may be multiple tests within one laboratory or several test results from different laboratory disciplines for one patient event
* It is realistic to expect a result within 28 days. However, if the test is known to influence treatment decisions, the laboratory should have a policy for prioritization of samples. Reporting times \
should be adjusted with local clinicians, e.g., a urgent FISH result of childhood acute leukemia or a t(15;17) should be expected within 48 h
- Reporting of results of SKY, M-FISH, I-FISH and genomic microarray is different. See [here](https://link.springer.com/protocol/10.1007/978-1-4939-6703-2_24)
![Example of ISCN](https://www.researchgate.net/profile/Bradley_Coe/publication/5358710/figure/fig5/AS:267578379599876@1440807065243/Sample-ISCN-report-exported-from-MD-SeeGH-Tab-delimited-ISCN-report-exported-from.png)

## HGVS: reports variants on DNA, RNA and protein level. 
* General variant annotation: reference id: description. 
** Reference id are of different types:
*** Genomic: 1. NC_ reference sequence based on a chromosome 2. NG_ reference sequence based on a gene or gene region, 3. LRG_ used in diagnostic setting, reference sequence based on a gene or gene \
region; Description: 'g' (e.g. 1,NC_000023.9:g.32317682G>A; 2,NG_012232.1:g.954966C>T; 3,LRG_199:g.954966C>T)
*** Transcriptomic: 1. NM_ reference sequence based on protein-coding RNA, 2. NR_ reference sequence based on non-coding RNA; Description: 'c' (e.g. 1,NM_004006.2:c.4375C>T; 2,NR_002196.1:c.601G>T)
*** Proteomic: 1. NP_ reference sequence based on protein; Description: 'p' (e.g. NP_003997.1:p.Arg1459*)

![Example of nomenclature HGVS](https://www.researchgate.net/profile/Charles_Steward/publication/317301091/figure/tbl1/AS:668532673110016@1536402018051/Examples-of-disease-causing-variation-with-associated-HGVS-nomenclature.png)


## VCF: reports all sorts of mutations 
* General annotation format: header and body.
** Header portion includes file format, file date, genotype quality, mapping quality and other fields. 
** Body portion comprises variants such as ![here](https://biomedical-sequencing.at/VCFFilter/VCFFilter/VCF_example_50.png)

*** Fields annotating the variant are chromosome, position, id of the variant, reference allele, alternative allele (observed in samples), quality of variant, result of filtering status, information  \
of the variant such as NS: number of samples, AF: allelic frequency, DP: total depth, DB: dbSNP membership, H2: presence of variant in HapMap2, AA: ancestral allele, format of the individual sample information: GT genotype, GQ genotype \
quality, DP total depth and HQ haplotype quality. 

Note: not fitting for structural variant annotation due to one entry in POS column

## GA4GH Variation Representation Specification: provides a standard variant-calling format and result of a collaboration among contributors representing national information resource providers, major \
 international public initiatives, and diagnostic testing laboratories



# Genomic Coordinate Systems
## 0 vs 1-based 

See ![here](https://s11.postimg.cc/jmk325fvn/basic_diagram.jpg)

For example: in 0-based chr1:1-4 = ACG, in 1-based chr1:1-4 = TACG

Annotate variants: ![SNVs](https://s2.postimg.cc/40doixek9/single_nucleotide_or_variant.jpg)
![Indels](https://s16.postimg.cc/9ne4syrp1/insertion_or_deletion.jpg)


