<img align="right" src="https://github.com/klebgenomics/Kaptive/blob/master/docs/assets/logo.png?raw=true" alt="Kaptive" width="200">

# _Acinetobacter baumannii_ surface polysaccharide locus databases
*[Kaptive](https://github.com/klebgenomics/Kaptive/) databases for Acinetobacter baumannii*

[![Streamlit App](https://img.shields.io/badge/Streamlit-%23FE4B4B.svg?logo=streamlit&logoColor=white)](https://kaptive-database-validator.streamlit.app/)
[![Release Database](https://github.com/tomdstanton/A_baumannii_Surface_Antigen_Loci/actions/workflows/release.yml/badge.svg)](https://github.com/tomdstanton/A_baumannii_Surface_Antigen_Loci/actions/workflows/release.yml)

This repository houses databases for _in silico_ typing of _Acinetobacter baumannii_ K and OC surface polysaccharides using [Kaptive](https://github.com/klebgenomics/Kaptive). The capsule polysaccharide (K) and outer-core (OC) component of the lipooligosaccharide (LOS) are major cell surface structures, and key epidemiological markers. Accurate prediction of K and OC types from whole-genome sequence data therefore supports genomic surveillance, as well as the development, evaluation, and application of a range of non-antibiotic interventions that have specificity for these surface structures.

> [!WARNING]
> These databases have been developed and tested specifically for _A. baumannii_. Using the databases to type other organisms, including other _Acinetobacter_ species, may result in errors and low typing rates. You can check that your assembly is a true _A. baumannii_ by screening for the presence of the _oxaAB_ gene (also known as the _blaoxa51-like_ gene) e.g. using blastn.

## Contents
- [Database formats and versions](#database-formats-and-versions)
  - [How are loci defined?](#how-are-loci-defined)
  - [K locus database](#k-locus-database)
  - [OC locus database](#oc-locus-database)   
- [Citations](#citations)
- [Curators](#curators)
- [Contribute](#contribute)
- [License](#license)

## Database formats and versions

The K and OC locus databases each comprise two files that are required to run Kaptive:
1. A multi-genbank file containing each unique locus sequence and its gene annotations.
2. A metadata file in TOML format, which provides essential information about the database (e.g. version, target organism(s), curator details), plus any special [phenotype logic](https://klebgenomics.github.io/Kaptive/Databases.html#phenotype-logic) that applies to the database.

Please see the [Kaptive docs](https://klebgenomics.github.io/Kaptive/Databases.html#format) for more details on the database file formats.

### How are loci defined?

Unique locus sequences are characterised based on the nomenclature system described in [Kenyon JJ and Hall RM. PLoS One. 2013](https://doi.org/10.1371/journal.pone.0062160). 

For capsular polysaccharides, distinct K locus (KL) sequences represent a unique combination of genes located between _fkpA_ and _lldP_ genes on the chromosome, and KL numbers are assigned consecutively in order of discovery. Allelic differences in the seven core capsule genes (_wza_, _wzb_, _wzc_, _galU_, _ugd_, _gpi_, and _pgm_) do not warrant the designation of a new KL number.

For outer-core oligosaccharide components of the LOS, distinct OC locus (OCL) sequences represent a unique combination of genes located between _ilvE_ and _aspS_ on the chromosome, and OCL numbers are also assigned consecutively in order of discovery.

For genes to be considered 'unique', the gene translations (protein sequences) from each locus **must fall under a defined percent identity threshold of 85%.** 

In some cases, specific nucleotide variations within loci and/or additional genes located elsewhere in the genome are known to result in modifications to the resulting polysaccharide structure. Where the impact of these variations or additional genes is well understood, they are captured within the databases using the phenotype logic section of the metadata file and the 'extra genes' entries within the multi-genbank file.

### K locus database

The *A. baumannii* K locus reference database(`Acinetobacter_baumannii_K.gbk`) comprises 409 fully annotated KL sequences and 10 'extra-locus' genes.

> [!Note]
> Insertion sequences (IS) are excluded from this database since it is assumed that the ancestral sequence was likely IS-free and IS transposase genes are not specific to the K locus.
> Synthetic IS-free K locus sequences were generated for K loci for which no naturally occurring IS-free variants have been identified to date.

As a capsule serotyping scheme is no longer maintained for _A. baumannii_, Kaptive will assign 'K type' numbers based on the detected KL or combination of KL and extra-locus genes, only in cases where structural data or empirical evidence is available. In general, the numbering follows the KL numbering system i.e. KL1 produces the K1 type. However, the following rules apply for special cases:
- where two or more loci produce the same capsule structure, the type is named after the KL with the lowest number 
  i.e. KL3 and KL22 produce the K3 type.
- where gene interruptions change the structure produced, the type is assigned a numbered 'v' suffix to indicate a defined 'variant'
- where extra-locus acetyltransferase genes are found to acetylate sugar(s) in the structure, the type is assigned an 'Ac' suffix
- where extra-locus genes are found to change a sugar in the structure, the type is assigned a suffix to indicate the sugar change
- where extra-locus _wzy_ polymerase genes modify the linkage between oligosaccharide units in the structure, the type is assigned a suffix to indicate the Wzy polymerase involved.

#### Database versions:

- v0.7.0 and above (previously distributed with Kaptive) include the original _A. baumannii_ K
  locus database with 92 KL, as described in [Wyres, KL. et al. Microbial Genomics
  2020](https://doi.org/10.1099/mgen.0.000339).
- v2.0.1 and above (previously distributed with Kaptive) includes an additional 149 novel _A. baumannii_ K
  locus references (241 KL total) as described in [Cahill, S.M. et al. Microbial Genomics 2022](https://doi.org/10.1099/mgen.0.000878).
- v2.0.2 and above (previously distributed with Kaptive) includes special logic parameters that enable prediction of K type based on KL or the detected combination of a specific KL with extra-locus genes as described in [Cahill, S.M. et al. 
  Microbial Genomics 2022](https://doi.org/10.1099/mgen.0.000878).
- v 3.3.0 includes an additional 168 novel _A. baumannii_ K locus references (409 KL total).

### OC locus database

The _A. baumannii_ OC locus reference database(`Acinetobacter_baumannii_OC.gbk`) comprises 22 fully annotated OCL sequences.

#### Database versions:
- v0.7.0 and above (previously distributed with Kaptive) include the original _A. baumannii_ OC
  locus database with 12 OCL (OCL1-OCL12), as described in [Wyres, KL. et al. Microbial Genomics
  2020](https://doi.org/10.1099/mgen.0.000339).
- v2.0.5 and above (previously distributed with Kaptive) includes an additional 10 novel _A. baumannii_ OC locus
  references (OCL13-OCL22) as described in [Sorbello, B. et al. Microbial Genomics 
  2023](https://doi.org/10.1099/mgen.0.001042).

## Citations

If you use the K locus database please cite:

Kenyon JJ. 2026. Diversity at the _Acinetobacter baumannii_ K locus: towards a comprehensive in silico database for prediction of capsular polysaccharide types. _In prep._

If you use the OC locus database please cite:

Sorbello BM, Cahill SM, Kenyon JJ. 2023. Identification of further variation at the lipooligosaccharide outer core locus in _Acinetobacter baumannii_ genomes and extension of the OCL reference sequence database for Kaptive. Microbial Genomics. 9(6):001042. DOI: [https://doi.org/10.1099/mgen.0.001042](https://doi.org/10.1099/mgen.0.001042)

If you use [Kaptive](https://github.com/klebgenomics/Kaptive/) please cite:

Stanton TD, Hetland MAK, Löhr IH, Holt KE, Wyres KL. 2025. Fast and Accurate _in silico_ Antigen Typing with Kaptive 3. Microbial Genomics. 11(6):001428. DOI: [https://doi.org/10.1099/mgen.0.001428](https://doi.org/10.1099/mgen.0.001428)

## Curators

These databases are maintained by [Johanna Kenyon](https://experts.griffith.edu.au/45350-johanna-kenyon) (Griffith University, Australia)

## Contribute

If you think you've found a novel K or OC locus please [get in touch](mailto:j.kenyon@griffith.edu.au) so we can add it to the database (with attribution).
