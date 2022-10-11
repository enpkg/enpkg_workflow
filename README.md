# enpkg_workflow
The **Experimental Natural Products Knowledge Graph** workflow aims at integrating experimental LC-MS/MS metabolomics data into a Wikidata-connected knowledge graph. To allow for iterative addition of samples over time, data from each sample is processed individually. For each of them, the required input data are 1) a minmal metadata file containing the sample's originating species (binomial nomenclature), 2) the feature list (.csv file) and 3) the corresponding fragmentation spectra (.mgf file). The workflow automatically resolves the species taxonomy against Open Tree of Life (ottID), generates a Molecular Network from fragmentation spectra (MN) and annotates features using two different methods (spectral matching to *in silico* DB coupled to taxonomical reweighting and Sirius/CSI:FingerID). 

Once the processing on individual samples is done, different meta-analysis to enhance the comparison among samples are available. Spectra can be compared among samples using a *meta*-MN through GNPS and samples' fingerprint can be compared using MEMO. For annotated compounds, Wikidata ID and NPClassifier ontology is automatically retrieved and it is possible to integrate compounds with activity reported against one (or more) selected biological target in ChEMBL DB. 

Finally, all of the data previously generated is integrated into a RDF knowledge graph. The graph structure allow for optimal query using the SPARQL language and is fully compatible for subsequent addition of samples.

The different steps are described below, with the link to the corresponding repository:

# Individual sample scale processing:
These steps needs to be run only once for each sample.

## 0) Organize data
Organize output from MzMine in individual folders for each sample.  
Repo: https://github.com/mandelbrot-project/data_organization

## 1) Taxonomical enhancement
Resolve taxonomy for each sample and link it to Wikidata.  
Repository: https://github.com/mandelbrot-project/taxo_enhancer

## 2) Structural annotation and MN
- ISDB and MS1 annotation coupled to taxonomical reweighting and MN generation.  
Repo: https://github.com/mandelbrot-project/indifiles_annotation
- Sirius/CSI:FingerID/Canopus.  
Repo: https://github.com/mandelbrot-project/sirius_canopus

# Meta-analysis
These steps needs to be run each time a sample is added to the sample set.

## 1) Data integration and metadata fetcher
- compound_metadata_fetcher: Retrieve NPClassifier taxonomy and WD ID for each annotated compoud
- MEMO: Generate MEMO matrix from samples' spectral data
- Meta_MN: Generate a meta-MN to link spectra among samples (GNPS)
- chembl_fetcher: download compounds with a reported activity against a given target (Optional)

Repo: https://github.com/mandelbrot-project/meta_analysis

## 2) Graph builder
Build a knowledge graph integrating the data generated above.  
Repo: https://github.com/mandelbrot-project/graph_builder

## 2') Sample explorer
Explore visually the data generated above.  
Repo: https://github.com/mandelbrot-project/sample_explorer

