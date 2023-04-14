# Testing the CMM-RT pipeline

In this repository you can find the scripts and the data I have been using to test the CMM-RT pipeline.

I used my own fork of the cmmrt repository to install CMMRT ([here](https://github.com/Coayala/cmmrt)), as there were some broken paths. The original repository is [this one](https://github.com/constantino-garcia/cmmrt).

To be able to install CMM-RT I had to use exactly the Xgboost module 1.3.3 otherwise it did not work. 

I am currently running the scripts using Jupyter notebooks. 

## Repository contents

**Input files**:

All this files will be inside the `data` directory.

- `CMM_vectorfingerprints.csv`: file with the molecular descriptors of the metabolites from the PubChem database.
- `final_pubchem_results.csv`: file with information about metabolites in the PubChem database (e.g., Name, Molecular Formula, etc).
- `RP_skin_all.csv`: Table with the experimental abundance and retention time of all the metabolites detected in the experiment (metabolites were extracted from pig skin).
- `RP_skin_id.csv`: Table containing only metabolites that were identified using the internal database of the UA Mass Spectrometry Core (this are high-confidence identifications).
- `saved_models/v0/preprocessor.pkl`: A pickled file with the preprocessed data provided by the original authors.
- `saved_models/v0/dnn.pkl`: A pickled file with the deep neural network model provided by the original authors.

**Scripts**:

- `test_dnn_predict.ipynb`: This script was used to create the predicted retention time database (`predicted_rt_db.csv`) using the provided **dnn model**.
- `train projectors.ipynb`: This script was used to recreate the projector models from the original authors.
- `prediction_loops.ipynb`: This script was used to test the projector model by randomly selecting 10, 20 or 30 *known* metabolites from the`RP_skin_id.csv` file to do the projections.
- `own_predictions.ipynb`: This script was used to annotate all the unknowns from the`RP_skin_all.csv` file.

**Results**

All the outputs are in the `results` directory.

- `projection functions/`: A directory containing outputs generated while training the projectors.
- `train_projectors/`: A directory that contains the trained projector `p2e_zero_rbf+linear_4e03_-1_10`.
- `predicted_rt_db.csv`: A table with the predicted retention times of the metabolites from PubChem
- `results_test_loop/`: Directory containing the annotated metabolites and the plot of the projections while testing different number of *known* metabolites.