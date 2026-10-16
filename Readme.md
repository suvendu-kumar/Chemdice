# FeatureDice — Legacy Repository

> **Note:** This repository contains an older version of Chemical Dice Integrator (CDI). For the latest implementation, updates, and documentation, please visit the official repository: [**Chemical Dice Integrator — The Ahuja Lab**](<https://github.com/the-ahuja-lab/ChemicalDice>)

## Introduction

FeatureDice is a Python framework for multimodal data fusion in cheminformatics and bioinformatics. It integrates heterogeneous feature representations, including molecular descriptors, chemical embeddings, graph representations, and omics data, into unified representations for downstream analysis and predictive modeling.

The framework supports a range of feature fusion techniques, including PCA, ICA, Incremental PCA, CCA, t-SNE, Kernel PCA, Random Kitchen Sinks (RKS), Partial Least Squares Discriminant Analysis (PLS-DA), autoencoders, and tensor decomposition.

Additional functionality includes data preprocessing, missing-value handling, normalization, dimensionality reduction, model evaluation, cross-validation, and visualization of predictive performance.

## Installation

This legacy version can be installed from TestPyPI with its dependencies:

```
pip install -i https://test.pypi.org/simple/ FeatureDice==1.0.1 scikit-learn torch tensorly
```

Compatibility may depend on the Python version and the versions of the dependencies installed.

## Usage

### Import

```
from FeatureDice.fusionData import fusionData
from FeatureDice.plot_data import plot_model_metrics
from FeatureDice.plot_data import plot_model_boxplot
```

### Load datasets

Provide a dictionary mapping dataset names to CSV file paths. Each dataset should contain sample identifiers, prediction labels, and feature columns.

```
data_paths = {
    "tabular1": "data/Chemberta_embeddings.csv",
    "tabular2": "data/graph_embeddings.csv",
    "tabular3": "data/mopac_descriptors.csv",
    "tabular4": "data/mordred_descriptors.csv",
    "tabular5": "data/signaturizer_descriptors.csv",
}

fusiondata = fusionData(data_paths=data_paths)
```

Access a loaded dataset using:

```
fusiondata.dataframes["tabular1"]
```

### Data preprocessing

FeatureDice provides methods for aligning samples across datasets, inspecting missing values, removing features with excessive missingness, imputing missing values, and scaling or transforming data.

```
fusiondata.keep_common_samples()

fusiondata.ShowMissingValues()
fusiondata.remove_empty_features(threshold=20)

fusiondata.ImputeData(method="knn")
fusiondata.scale_data(scaling_type="standardize")
fusiondata.normalize_data(normalization_type="constant_sum")
fusiondata.transform_df(transformation_type="log")
```

Available preprocessing options include:

- **Imputation:** KNN, mean, mode, median, and interpolation.
- **Scaling:** Standardization, min-max scaling, robust scaling, and Pareto scaling.
- **Normalization:** Constant-sum, L1, L2, and max normalization.
- **Transformation:** Logarithmic, square-root, cube-root, power, and quantile transformations.

### Feature fusion

Fuse features from multiple datasets into a unified representation.

```
fusiondata.fuseFeatures(
    n_components=10,
    method="plsda"
)

fused_dataframe = fusiondata.fusedData
```

Available fusion methods include PCA, ICA, Incremental PCA, CCA, t-SNE, Kernel PCA, RKS, SEM, autoencoders, tensor decomposition, and PLS-DA, subject to the capabilities of this legacy implementation.

### Model evaluation

Evaluate fusion methods using machine-learning models:

```
fusiondata.evaluate_fusion_models(
    n_components=10,
    methods=["pca", "cca"]
)

metrics = fusiondata.Accuracy_metrics
top_models = metrics.iloc[:10, :]
```

For cross-validation, the legacy API documents the following method:

```
fusiondata.evaluate_fusion_model_nfold(
    n_components=10,
    methods=["pca", "cca"],
    n_folds=10
)
```

Check the installed version's API for the exact method name and supported parameters.

### Visualization

Visualize model evaluation metrics:

```
plot_model_metrics(
    top_models,
    save_dir="output_plots"
)

plot_model_boxplot(
    top_models,
    save_dir="outputs"
)
```

## Project Status

This repository is retained for reference to an earlier version of the project. It may not reflect the latest features, implementation, or documentation.

For current development and the latest version of Chemical Dice Integrator, visit:

[**https://github.com/the-ahuja-lab/ChemicalDice**](<https://github.com/the-ahuja-lab/ChemicalDice>)
