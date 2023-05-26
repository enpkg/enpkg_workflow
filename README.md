# enpkg_workflow
The **Experimental Natural Products Knowledge Graph** workflow aims at integrating experimental LC-MS/MS DDA metabolomics data into a Wikidata-connected knowledge graph. To allow for iterative addition of samples over time, data from each sample is processed individually.

For each of them, the required input data are 
1) a minimal metadata file containing the sample's originating taxon, 
2) The LC-MS/MS DDA data
 
After [MZmine](http://mzmine.github.io/) processing, the workflow automatically resolves the species taxonomy against Open Tree of Life (ottID), generates a Molecular Network from fragmentation spectra (MN) and annotates features using two different methods (spectral matching to *in silico* DB coupled to taxonomical reweighting and Sirius/CSI:FingerID). 

Once the processing on individual samples is done, for annotated compounds, Wikidata ID and NPClassifier ontology is automatically retrieved and it is possible to integrate compounds with activity reported against one (or more) selected biological target in ChEMBL DB. 
To compare the spectral fingerprint of the samples, the generated data structure is compatible with a MEMO analysis.  

Finally, all of the data previously generated is integrated into a sample-sepcfic RDF knowledge graph. These sample-specific KG from multiple specific can be combined to effectively compare samples based on their metadata and their spectral and structural data. The graph structure allow for optimal query using the SPARQL language and is fully compatible for subsequent addition of samples.

The different steps are described below, with the link to the corresponding repository:

# Prerequisites:
You will need to have [Git](https://github.com/git-guides/install-git) and [Anaconda](https://docs.anaconda.com/free/anaconda/install/index.html) (or [Miniconda](https://docs.conda.io/en/latest/miniconda.html)) installed.

# Individual sample scale processing:
These steps needs to be run only once for each sample.

## 0) Organize data
Aim: Organize output from MzMine in individual folders for each sample.  
Repository: https://github.com/enpkg/enpkg_data_organization

## 1) Taxonomical enhancement
Aim: Resolve taxonomy for each sample and link it to Wikidata.  
Repository: https://github.com/enpkg/enpkg_taxo_enhancer

## 2 and 3) MN, ISDB annotation and taxonomical/chemical consistency reweighting
Aim: MN generation, ISDB and MS1 annotation coupled to taxonomical and chemical consistency reweighting on each sample  
Repository: https://github.com/enpkg/enpkg_mn_isdb_taxo

## 4) SIRIUS/CSI:FingerID/CANOPUS annotation
Aim: Perform SIRIUS/CSI:FingerID/CANOPUS on each sample
Repository: https://github.com/enpkg/enpkg_sirius_canopus

# Meta-analysis
These steps needs to be run each time a sample is added to the sample set.

## 1) Data integration and metadata fetcher
- compound_metadata_fetcher: Retrieve NPClassifier taxonomy and WD ID for each annotated compoud
- MEMO: Generate MEMO matrix from samples' spectral data (optional)
- chembl_fetcher: download compounds with a reported activity against a given target (optional)

Repository: https://github.com/enpkg/enpkg_meta_analysis

# Final step: RDF formating for data integration

## 2) Graph builder
Aim: Build a knowledge graph integrating the data generated above.  
Repository: https://github.com/enpkg/enpkg_graph_builder
