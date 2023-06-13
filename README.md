# enpkg_workflow

![release_badge](https://img.shields.io/github/v/release/enpkg/enpkg_workflow)
![license](https://img.shields.io/github/license/enpkg/enpkg_workflow)

<p align="center">
 <img src="https://github.com/enpkg/enpkg_workflow/blob/main/logo/enpkg_logo_full.png" width="300">
</p>

The **Experimental Natural Products Knowledge Graph** workflow aims at integrating experimental LC-MS/MS DDA metabolomics data into a Wikidata-connected knowledge graph. To allow for iterative addition of samples over time, **data from each sample is processed individually.**

For each sample, the required input data are 
1) A minimal metadata file containing the sample's originating taxon.
2) The LC-MS/MS DDA data (positive and/or negative ionization modes). 
 
After [MZmine](http://mzmine.github.io/) processing, the workflow automatically resolves the species taxonomy against [Open Tree of Life](https://tree.opentreeoflife.org/about/taxonomy-version/ott3.5) (ottID), generates a Molecular Network from fragmentation spectra (MN) and annotates features using two different methods (spectral matching to *in silico* DB coupled to taxonomical reweighting and [Sirius/CSI:FingerID](https://bio.informatik.uni-jena.de/software/sirius/)). 

Once the processing on individual samples is done, for annotated compounds, [Wikidata](https://www.wikidata.org/wiki/Wikidata:Main_Page) ID and [NPClassifier](https://npclassifier.ucsd.edu/) ontology is automatically retrieved and it is possible to integrate compounds with activity reported against one (or more) selected biological target in [ChEMBL](https://www.ebi.ac.uk/chembl/) DB. 
To compare the spectral fingerprint of the samples, the generated data structure is compatible with a [MEMO](https://github.com/mandelbrot-project/memo) analysis.  

Finally, all of the data previously generated is integrated into a sample-specific [RDF knowledge graph](https://en.wikipedia.org/wiki/Knowledge_graph). These sample-specific KG from multiple specific can be combined to effectively compare samples based on their metadata and their spectral and structural data. The graph structure allow for optimal query using the SPARQL language and is fully compatible for subsequent addition of samples.

The different steps are described below, with the link to the corresponding repository to perform the analysis:

# Prerequisites:
You will need to have [Git](https://github.com/git-guides/install-git) and [Anaconda](https://docs.anaconda.com/free/anaconda/install/index.html) (or [Miniconda](https://docs.conda.io/en/latest/miniconda.html)) installed.

# Individual sample scale processing:
These steps needs to be run **only once for each sample.** 🚀

## 1) Organize data
**Aim**: Organize output from MzMine in individual folders for each sample.  
Repository: https://github.com/enpkg/enpkg_data_organization

## 2) Taxonomical enhancement
**Aim**: Resolve taxonomy for each sample and link it to Wikidata.  
Repository: https://github.com/enpkg/enpkg_taxo_enhancer

## 3) MN, ISDB annotation and taxonomical/chemical consistency reweighting
**Aim**: MN generation, ISDB and MS1 annotation coupled to taxonomical and chemical consistency reweighting on each sample.  
Repository: https://github.com/enpkg/enpkg_mn_isdb_taxo

## 4) SIRIUS/CSI:FingerID/CANOPUS annotation
**Aim**: Perform SIRIUS/CSI:FingerID/CANOPUS on each sample.  
Repository: https://github.com/enpkg/enpkg_sirius_canopus

## 4) Compounds metadata enhancement
**Aim**: Retrieve NPClassifier taxonomy and WD ID for each annotated compoud.  
Repository: https://github.com/enpkg/enpkg_meta_analysis

## 5) Graph building
**Aim**: Build a knowledge graph for each sample integrating the data generated above.   
Repository: https://github.com/enpkg/enpkg_graph_builder

# Additional analyses compatible with the ENPKG workflow
## MEMO analysis and ChEMBL integration
- **MEMO**: Generate MEMO matrix from samples' spectral data (optional)
- **chembl_fetcher**: download compounds with a reported activity against a given target (optional)  

Repository: https://github.com/enpkg/enpkg_meta_analysis
