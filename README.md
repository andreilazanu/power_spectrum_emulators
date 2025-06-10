# Power spectrum emulators from the Quijote simulations

This project aims to build emulators for the matter power spectrum on non-linear scales in two extensions of the ΛCDM model:
- massive neutrinos and dark energy, via the total neutrino mass and the dark energy equation of state;
- primordial equilateral non-Gaussianity.

Emulators are models trained on N-body simulations of the Universe, that can predict cosmological observables without the user having to run the simulations. In this project, I am focussing on predicting the two-point correlation function in Fourier space (power spectrum), a key cosmological observable widely used to constrain models in the field.

The simulations used are the Quijote suite, a publicly available set of 88000 simulations, available at https://quijote-simulations.readthedocs.io/en/latest/.

In this work, the emulators are built using machine learning tools. The inputs (features) are the cosmological parameters (7 and 5 respectively), while the outputs (targets) are represented by the power spectra, all evaluated at the same k-values. As the number of targets is around 300, I am considering 2 options:
- using the full power spectra as targets
- using data compression techniques, in particular Principal Component Analysis (PCA) to reduce the number of targets. 11 principal components account for more than 99.5% of the variance of the data.

The machine learning models consist of
- a *neural network*, with 2 2048-neuron hidden layers, with ReLU activation functions, followed by Dropout layers.
- a *CatBoost* regression model.

The simulations are split into a training and test set and the model performance is validated using 5-fold cross-validation (k = 5).
The best prediction is given by the PCA version of the neural network, achieving better than 5% root-mean-square-relative-error on the test set.

Other tree-based methods (Random Forest regressors, LightGBM, XGBoost) are investigated but shown to perform worse.

The 2 Jupyter notebooks show the results at redshift z=0. For other redshifts, the corresponding files can be easily modified in the notebook. Please also refer to the accompanying paper for details (https://arxiv.org/abs/2506.07514).
