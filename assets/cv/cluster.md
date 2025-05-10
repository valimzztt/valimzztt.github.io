---
layout: post
title:  "Split Operator Method"
date:   2025-05-01 20:44:51 +0100
categories: [projects]
author: Valentina Mazzotti, Cecilia Soroco
---
# Introduction

Understanding the properties of materials at the atomic level is crucial
for scientific discovery and technological innovation
[@national1999condensed]. Calculating these properties for all possible
atomic arrangements using first-principle methods like density
functional theory (DFT) [@DFT1] is computationally demanding. Cluster
expansion (CE) offers a solution, by allowing to predict the energies of
different configurations and concentrations of a several elements
arranged on a fixed lattice [@morgan2017using]. The essence of the
cluster expansion method is to represent the target
configuration-dependent property (in our case the energy $E(\sigma)$),
as an expansion of averaged cluster functions with the effective cluster
interactions (ECIs) as the coefficients.
$$E(\sigma) = \sum_{a} J_a \Phi_\alpha(\sigma)
\label{eq:cluster-expansion1}$$ In Equation
[\[eq:cluster-expansion1\]](#eq:cluster-expansion1){reference-type="ref"
reference="eq:cluster-expansion1"}, $J_{\alpha}$ are termed the
effective cluster interactions (ECIs), and $\Phi_{\alpha}$ are the
cluster correlation functions, which, in the case of a pseudo-binary
system like , are defined as the product of discrete pseudo-spin
variables $\sigma_i$ at the lattice sites forming cluster $\alpha$
(namely $\Phi_{\alpha} = \prod_{i \in \alpha} \sigma_i$). The cluster
correlation function $\Phi_{\alpha}$ for a given cluster $\alpha$
depends solely on the atomic configuration $\sigma$ and the number of
atomic sites within the cluster. The full expansion of the energy in
Equation
[\[eq:cluster-expansion1\]](#eq:cluster-expansion1){reference-type="ref"
reference="eq:cluster-expansion1"} is theoretically exact but
practically infeasible; hence, it is necessary to truncate the series
while retaining the dominant $N$-body cluster terms. Modern advancements
in machine learning provide systematic approaches to the challenge of
determining the optimal point of truncation and the relevant clusters to
include in the model [@natarajan2018machine]. In this project, we focus
on how machine learning (ML) algorithms can be utilized to identify key
interactions in the energy expansion described by Equation
[\[eq:cluster-expansion1\]](#eq:cluster-expansion1){reference-type="ref"
reference="eq:cluster-expansion1"}, aiming to enhance the accuracy of
predictions concerning its thermodynamic behavior.

By leveraging a limited dataset from density functional theory (DFT)
calculations, we assess the performance of various models. Our approach
includes experimenting with different neural network architectures,
applying regularization techniques in linear regression to select an
appropriate cluster basis set, and implementing schemes to reduce
overfitting, such as cross-validation and regularizers. Additionally, we
evaluate the impact of model complexity on the predictive ability for
unseen data. Our findings highlight the advantages of combining machine
learning with established scientific methods, offering a powerful new
approach for predicting material properties and guiding the design of
new materials. The integration of machine learning and Cluster Expansion
represents a significant advancement in the field, potentially leading
to faster, more accurate predictions that could facilitate the design
and discovery of new materials with tailored properties.\

# Description of the training set

Our dataset consists of 200 distinct structures, each one representing
an intermetallic compound targeting the specific stoichiometry of
$\ch{Mn}=0.6$, $\ch{Ni}=0.4$, $\ch{As}=1$ reflective of the
$\ch{Mn_{0.6}Ni_{0.4}As}$ intermetallic's composition under study. These
training structures are generated using a `CECrystal` framework offered
by the Python package CLEASE [@CLEASE]. Within the formalism of Cluster
Expansion, the training structures had to be defined by certain
properties, such as a fixed lattice constant of $a = b = 3.64580405\ Å$,
$c = 5.04506600\ Å$, and interaxial angles all fixed at $90^\circ$, with
the exception of the $\gamma$ angle set at $120^\circ$, capturing the
hexagonal nature of the lattice. Each structure is expanded into a
supercell ten times larger than the primitive unit, representative of
the material's extended periodicity.

# Experiment 1: Controlling the Model's Complexity {#sec:Experiment1}

#### Background:

In constructing an energy model via cluster expansion (CE), it is good
practice to integrate physical intuition and incorporate physics-based
priors on the magnitude of the effective cluster interaction (ECI), as
well as on the clusters of atoms that are relevant to describe the
energetic landscape of the system. In intermetallic materials, phenomena
such as ordering---exemplified by the magnetic nanolayering in ---are
typically governed by short-range (SR) interactions [@ShortRange]. This
suggests that the energy landscape of simpler systems may be
predominantly influenced by smaller-sized clusters of atoms or atomic
arrangements. Therefore, an initial task involves constraining model
complexity by setting cutoffs to the spatial extent of effective atomic
interactions for the diameters of 2, 3, and 4-body clusters included in
the expansion of Equation
[\[eq:cluster-expansion1\]](#eq:cluster-expansion1){reference-type="ref"
reference="eq:cluster-expansion1"}. A higher diameter size for a cluster
includes a greater number of atomic arrangements, thereby increasing
model complexity, and potentially leading to overfitting. Conversely, a
smaller diameter size restricts the model to fewer, but potentially more
relevant, atomic arrangements. For instance, specifying a cutoff
diameter of $7 \, \text{\AA}$ for a 4-body cluster implies that the
model only considers interactions from four atomic arrangements within
this maximum distance in the lattice.

#### Objective:

This first experiment aims to determine the optimal balance between
model complexity and generalization capability to unseen data. By
methodically adjusting cluster size constraints using Elastic Net
regression [@ElasticNet] with predefined lambda ($\lambda$) and L1 ratio
values, we document both the root mean square error (RMSE) and the
validation (LOCV) score, using 5-fold cross validation. This allows us
to assess how these parameters influence the model's predictive accuracy
and its ability to effectively portray the ground-state energy of
crystalline solids.

<figure id="fig:rmse_cutoff_5CV">
<div class="minipage">
<img src="figs/RMSE_DiameterCutoff.png" style="width:120.0%" />
</div>
<div class="minipage">
<img src="figs/CVScore_DiameterCutoff.png" style="width:120.0%" />
</div>
<figcaption>Root Mean Square Error and CV score as a function of cluster
diameter cutoff (in Angstrom) using Elastic Net with predefined lambda
(<span class="math inline"><em>λ</em> = 0.01</span>) and L1 ratio value
equal to <span class="math inline">0.1</span>. Darker colors correspond
to lower RMSE and CV scores. Each axis of the three-dimensional plot
represents the diameter of 2-body, 3-body or 4-body clusters
respectively. </figcaption>
</figure>

#### Results 

The analysis of the 3D plots, as shown in Figure
[1](#fig:rmse_cutoff_5CV){reference-type="ref"
reference="fig:rmse_cutoff_5CV"}, allows us to conclude that the optimal
cluster diameter cutoffs for minimizing the Root Mean Square Error
(RMSE) and enhancing model generalizability are $7$ for the 2-body
cluster, $6$ for the 3-body cluster and $6$ for the 4-body cluster. For
example in the plot on the left, we see that these dimensions correspond
to an RMSE near $0.052$ represented in purple. These configurations
provide a balance between accuracy and generalization capabilities in
the cluster expansion model, effectively capturing the essential
interactions for predicting energy of crystalline solids such as . The
reasoning behind these specific choice of values is likely due to
properties of the physical arrangement of atoms, and is beyond the scope
of our analysis.

# Experiment 2: Testing Different Regularization Techniques {#sec:Experiment2}

#### Objective:

Once the relevant clusters diameters have been selected, we let $N_c$ be
the number of clusters such that the energy can be concisely represented
as the truncated series:
$$E(\sigma) = \sum_{\alpha=0}^{N_c-1} V_{\alpha} \phi_{\alpha}(\sigma) = \boldsymbol{\phi}(\sigma) \cdot \mathbf{V},$$
where $\mathbf{V} = [V_0, V_1, \dots, V_{N_c-1}]^T$ is the column vector
of ECIs and
$\boldsymbol{\phi}(\sigma) = [\phi_0, \phi_1, \dots, \phi_{N_c-1}]$ is
the row vector of cluster functions for configuration $\sigma$. When
formulated as a linear regression problem, the construction of the CE
model suffers the limitations of the least-squares (LS) fit, among which
the most well-known one is the underfitting/overfitting dilemma, also
known as bias/variance trade-off [@Variance-Bias].\
In this experiemnt, we compare the $R^2$ value and the average
validation error for different regularization techniques to see which
would yield the best results. We set the diameters cutoffs to be $7$ for
the two-body cluster, $6$ for the three-body cluster, and $6$ for the
four-body cluster, as determined in the previous experiment. The results
of the root-mean-squared error (RMSE) and leave-one-out cross-validation
(LOCV), as well as the number of features selected, is summarized in
Table
[1](#tab:Experiment2-regularization-comparison){reference-type="ref"
reference="tab:Experiment2-regularization-comparison"}. Figures
[\[fig:Experiment2-lassoReg\]](#fig:Experiment2-lassoReg){reference-type="ref"
reference="fig:Experiment2-lassoReg"},
[\[fig:Experiment2-ridgeReg\]](#fig:Experiment2-ridgeReg){reference-type="ref"
reference="fig:Experiment2-ridgeReg"}, and
[2](#fig:Experiment2-ElasticNetHyperparam){reference-type="ref"
reference="fig:Experiment2-ElasticNetHyperparam"} below demonstrate
plots of RMSE corresponding to different hyperparameters for Lasso
regression, Ridge regression and ElasticNet. The fit of CE-predicted
energy versus DFT energy for different regularization techniques can be
seen in Panel [5](#fig:Experiment2-Fit-Comparison){reference-type="ref"
reference="fig:Experiment2-Fit-Comparison"} in the Appendix.

<figure id="fig:Experiment2-ElasticNetHyperparam">
<div class="minipage">
<img src="figs/lasso_avgrmse1.png" width="220" />
<img src="figs/ridge_avgrmse1.png" width="220" />
</div>
<div class="minipage">
<img src="figs/ElasticNet_Heatmap_HyperparameterChoice.png"
width="230" />
</div>
<figcaption>Elastic Net Hyperparameter Heatmap showing with <span
class="math inline">log (<em>α</em>) = −4.778</span> and L1 ratio =
<span class="math inline">0.8</span> yielding the best RMSE of <span
class="math inline">0.065</span>.</figcaption>
</figure>

::: {#tab:Experiment2-regularization-comparison}
  **Model**                                  **RMSE (eV/prim)**   **LOCV (eV/prim)**   **Number of features (out of 22)**
  ----------------------------------------- -------------------- -------------------- ------------------------------------
  Ridge Regression                                 0.0611               0.0754                         21
  Ordinary Least Squares                           0.0642               0.0637                         22
  Automatic Relevance Determination (ARD)          0.0668                 --                           20
  Bayesian Linear Regression (BLR)                 0.0676                 --                           21
  Elastic Net                                      0.0686               0.0859                         10
  Lasso Regression                                 0.0708               0.0772                         8
  SGD Regressor                                    0.0872               0.0877                         21

  : Comparison of the RMSE, LOCV, and number of features selected for
  different regression models ordered from best to worst RMSE. The units
  for RMSE are electron-volt (eV) per primitive cell (prim).
:::

[]{#tab:Experiment2-regularization-comparison
label="tab:Experiment2-regularization-comparison"}

#### Results

From Table
[1](#tab:Experiment2-regularization-comparison){reference-type="ref"
reference="tab:Experiment2-regularization-comparison"}, we see that
Ridge Regression succeeded in yielding the lowest RMSE out of the 7
models tested. With the exception of SGD Regressor, we notice a trend in
that the best performing models also retained the highest number of
features. In general, every model yielded quite a low RMSE, indicating
that our energy prediction of the material will be reasonable.

#### Hyperparameter Optimization Discussion

In order to assess different regularization techniques, we first needed
to optimize each one by choosing the best hyperparameters. For Lasso and
Ridge regression, we identified the best hyperparameters using
cross-validation by evaluating and monitoring the average Root Mean
Square Error (RMSE) across 50 trials, and choosing the hyperparameter
$\lambda$, accordingly. Elastic Net required tuning of both the
regularization strength ($\lambda$) and the balance between $l_1$ and
$l_2$ regularization, which was achieved by analyzing a heatmap of RMSE
values across hyperparameter combinations. From Figure
[2](#fig:Experiment2-ElasticNetHyperparam){reference-type="ref"
reference="fig:Experiment2-ElasticNetHyperparam"}, we observe that the
choice of hyperparameters that yields the lowest RMSE for ElasticNet is
$\lambda=10^{-4.778}=1.67$ x $10^{-5}$ and $l_1 =0.8$. For the SGD
Regressor with early stopping, we used validation set performance as a
proxy for the generalization error in determining when overfitting has
begun [@EarlyStopping], adjusting for improvements with a tolerance
threshold of 0.001 and integrating cross-validation to ascertain the
effectiveness of the chosen settings. The process of cross-validation
for each model starts with a standardization procedure that normalizes
the feature space, ensuring that optimization algorithms are not biased
by the scale of the features. This approach allowed us to optimize the
hyperparameters effectively for each model. In addition to
cross-validation, we briefly explored a Bayesian Learning approach to
learn the hyperparameters from the data. In Bayesian Linear Regression
(BLR), this involves modelling the posterior predictive distribution of
the data based on the assumption that samples come from a Gaussian
distribution. Given that this model failed to outperform a majority of
the other models, we are not confident that this Gaussian assumption is
true. The Automatic Relevance Determination (ARD) model makes this same
Gaussian assumption while additionally encouraging sparse weights.
Since, this model only performed slightly better, we still cannot be
confident whether the Gaussian assumption is reasonable.\
Overall, we see that only Ridge Regression outperformed Ordinary Least
Squares. However, this model retained a large amount of features. In
general, we can see that the best performing models also retained the
most amount of features, demonstrating once again the trade-off between
selecting only the most expressive clusters for the cluster expansion,
and retaining a precise energy model.\
Although every model yielded low RMSE and/or LOCV scores, commenting on
the quality of our results is beyond the scope of this experiment.
Whether an error on the order of $10^{-2}$ eV/prim is acceptable will
depend on the intended experimental applications of the model.\

# Experiment 3: Neural Network

#### Methodology

Neural networks (NNs) have been employed for modelling energetic
properties of structures, to be used in screening inorganic solid
electrolytes and predicting molecular properties with high accuracy
[@NeuralNetworkClusterExpansion]. We therefore have trained a neural
network, using the Keras Tuner hyperparameter optimization framework
[@omalley2019kerastuner] that finetunes our neural network architecture.
During hyperparameter tuning, we are adjusting the number of neurons per
layer (ranging from 32 to 512), and selecting the number of layers
(either 10, 20 or 30). Additionally, each layer's activation function
can be either `relu` or `tanh`, determined stochastically by the tuner.
The inclusion of a dropout layer is also decided by a boolean
hyperparameter. Furthermore, the learning rate for the Adam optimizer is
fine-tuned, sampling logarithmically within the interval
$[10^{-4}, 10^{-2}]$.

#### Results

The best performing model was found to be a sequential model created
using TensorFlow's Keras API [@tensorflow2015-whitepaper], which is a
fully-connected NN composed of several hidden layers, each with 64
units. These layers use ReLU activation functions and include L2
regularization. Additionally, batch normalization is applied after each
dense layer, which stabilizes learning by normalizing the activations.
For training, an Adam optimizer is employed with a learning rate that
decays exponentially, starting from 0.001 and decreasing every 10,000
steps with a rate of 0.9. Training proceeds over 300 epochs with a batch
size of 32, using one fifth of the training set for validation.

<figure id="fig:Experiment13D_5CV">
<div class="minipage">
<p><img src="figs/NN10.png" style="width:120.0%" alt="image" /> <span
id="fig:Experiment3-nn10" data-label="fig:Experiment3-nn10"></span></p>
</div>
<div class="minipage">
<p><img src="figs/NN20.png" style="width:120.0%" alt="image" /> <span
id="fig:Experiment3-nn20" data-label="fig:Experiment3-nn20"></span></p>
</div>
<div class="minipage">
<p><img src="figs/NN30.png" style="width:120.0%" alt="image" /> <span
id="fig:Experiment3-nn30" data-label="fig:Experiment3-nn30"></span></p>
</div>
<figcaption>Comparison of Cluster Expansion (CE) predicted energy versus
Density Functional Theory (DFT) energy for neural network models with
different complexities. Each plot corresponds to a model with a specific
number of layers (10, 20, and 30). The red dashed line represents
perfect prediction alignment between the CE and DFT
energies.</figcaption>
</figure>

# Experiment 4: Genetic Algorithm enhanced CE

In the quest to find the best cluster diameter cutoff, we devise a
computational pipeline leveraging the TPOT Regressor, which is a Python
Automated Machine Learning tool that uses genetic programming principles
to systematically determine the most effective model [@TPOT].

#### Methodology 1:

First, we use the TPOT Regressor to evaluate a multitude of cluster
diameter, model and hyperparameter combinations, judging their
performance based on the root mean squared error (RMSE). The genetic
algorithm begins with a population of 50 potential solutions and
iteratively applies genetic operators such as selection, crossover, and
mutation to evolve the solutions with the aim of minimizing the mean
squared error loss. This evolutionary process is set to proceed for a
number of generations, with each refining the solutions based on their
performance in cross-validation with an $80/20$ train-test ratio.

#### Methodology 2:

We repeat the same procedure, but we now fix the diameter cutoffs to be
$7$ for the two-body cluster, $6$ for the three-body cluster, and $6$
for the four-body cluster, to find the best-performing model with the
same complexity as the one used in Section
[4](#sec:Experiment2){reference-type="ref" reference="sec:Experiment2"}.
The results for both optimization tests using the genetic algorithm are
reported in the captions of Figures
[\[fig:Experiment4-randomforest\]](#fig:Experiment4-randomforest){reference-type="ref"
reference="fig:Experiment4-randomforest"} and
[\[fig:Experiment4-GeneticAlgorithm\]](#fig:Experiment4-GeneticAlgorithm){reference-type="ref"
reference="fig:Experiment4-GeneticAlgorithm"}.

<figure id="fig:Experiment13D_5CV">
<div class="minipage">
<img src="figs/RandomForest750.png" style="width:120.0%" />
</div>
<div class="minipage">
<img src="figs/GeneticAlgorithmElasticNet766.png"
style="width:120.0%" />
</div>
<figcaption>Performance of the Elastic Net model optimized using the
genetic algorithm.</figcaption>
</figure>

#### Result 1:

The TPOT Regressor found the diameters $7$ for the two-body cluster, $6$
for the three-body cluster, and $6$ for the four-body cluster, as
optimal. With these diameters, the \"fittest\" model was found to be a
Random Forest Regressor with the following configuration: bootstrapping
was disabled; a maximum of $35\%$ of the features were considered when
splitting a node; the minimum number of samples required to be at a leaf
node was set to the default of one; at least 15 samples were required to
split an internal node; and the forest was composed of 100 individual
trees. The obtained pipeline allowed us to derive an outstanding RMSE
score of approximately 0.061, which is lower than all the RMS errors
listed in Table
[1](#tab:Experiment2-regularization-comparison){reference-type="ref"
reference="tab:Experiment2-regularization-comparison"}.

#### Result 2:

The optimal pipeline we derived via TPOT was as follows: first, we apply
the L2 norm to the feature vectors, preventing any single feature from
dominating the objective function. Subsequently, an `ElasticNetCV` model
is used for regression. The L1 ratio and tolerance are set to 0.2 and
0.1, respectively. As can be seen from Figure
[\[fig:Experiment4-randomforest\]](#fig:Experiment4-randomforest){reference-type="ref"
reference="fig:Experiment4-randomforest"} and Figure
[\[fig:Experiment4-GeneticAlgorithm\]](#fig:Experiment4-GeneticAlgorithm){reference-type="ref"
reference="fig:Experiment4-GeneticAlgorithm"}, leveraging the genetic
algorithm's ability to navigate complex search spaces efficiently
allowed us to find an ML model with the best $R^2$ values overall,
saving up precious computational/ hyperparameter tuning time.

# Discussion

In this study, we have employed various machine learning algorithms to
construct various accurate energy models using the Cluster Expansion
(CE) formalism. We have demonstrated which models could be used for
applications requiring precise energy representation, and which models
could be used for applications interested in learning the most relevant
clusters in the cluster expansion. A key limitation of our approach,
however, lies in the dependence of the cluster expansion model's quality
on the training set used to develop our energy model. This aspect was
not extensively tested in the current study. Adequate sampling of the
configuration space is critical for training robust energy models , and
historically, significant efforts have been dedicated to efficiently
searching for the most stable crystalline structures given the
compositions of the system's [@pyGACE]. Enhancing the sampling of the
phase space typically involves narrowing down potential candidate
structures for density functional theory (DFT) calculations through the
use of genetic algorithms, evolutionary algorithms, and deep learning
techniques.

A logical extension of this study would involve a detailed assessment of
the impact of training set quality on the overall performance of the
energy model. Furthermore, while our current focus was on improving the
predictive capability of the model---monitored through the leave-one-out
cross-validation (LOCV) score---a more comprehensive and thorough
analysis would include running Monte Carlo simulations using the
constructed energy model to verify its predictive accuracy.
Specifically, we are interested in its ability to simulate the exotic
nanolayering phenomenon in . Although these simulations were run, the
complete results from our Monte Carlo simulations were not included in
this report due to the study's limited scope, which was primarily aimed
at evaluating different machine learning algorithms on a constrained
dataset of DFT-derived data and configurations, and comparing each
model's predictive ability.

# Supplementary material {#app:info}

#### GitHub repository:

Here is the link to the [GitHub
repository](https://github.com/valimzztt/CPSC440-Project.git).

<figure id="fig:Experiment2-Fit-Comparison">
<div class="minipage">
<img src="figs/OLS766.png" style="width:140.0%" />
<img src="figs/Lasso766.png" style="width:140.0%" />
</div>
<div class="minipage">
<img src="figs/Ridge766.png" style="width:140.0%" />
<img src="figs/ElasticNet766.png" style="width:140.0%" />
</div>
<figcaption>Elastic Net</figcaption>
</figure>

![SGD Regressor](figs/SGDRegressor766.png){#fig:figsgdregresson
width="60%"}
