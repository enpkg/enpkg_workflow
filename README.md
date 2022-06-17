# enpkg_workflow
Summary of the different steps to independantly process metabolomics samples and integrate knowledge to finally build an Experimental Natural Products Knowledge Graph (ENPKG).

# Individual sample scale processing:
These steps needs to be run only once for each sample.

## 0) Organize data
Organize output from MzMine in individual folders for each sample.  
Repo: https://github.com/mandelbrot-project/data_organization

## 1) Taxonomical enhancement
Resolve taxonomy for each sample and link it to Wikidata.  
Repository: https://github.com/mandelbrot-project/taxo_enhancer

## 2) Structural annotation and MN
- ISDB coupled to taxonomical reweighting and MN generation.  
⚠️ Positive ionization mode only for the moment.  
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
Repo: https://github.com/mandelbrot-project/graph_sandbox

## 2') Sample explorer
Explore visually the data generated above.  
Repo: https://github.com/mandelbrot-project/sample_explorer

