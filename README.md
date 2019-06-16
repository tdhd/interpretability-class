# interpretability-class

This repo contains exercises regarding interpretability of ML models. There are some older ones in `exercises`, the newer more tooling focused notebook and setup guide can be found in `tooling-exercises` folder.

## setup

To get started, create a new conda environment and install all of the dependencies, run

```bash
conda create --name interpret python=3.7
conda activate interpret
conda install tensorflow matplotlib scikit-learn seaborn numpy pandas scipy statsmodels ipython jupyter
pip install eli5 lime keras-applications
```

For some functionality you might need to install graphviz.
