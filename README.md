## **Title:** Reproducing Havlíček et al.: Photonic Implementation of Quantum-Enhanced Feature Spaces

Motivation:
This repository work investigates whether quantum-inspired feature maps can be realized in photonic systems and how their structure affects learning performance.

###### \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Overview**

This project explores the quantum kernel method introduced in Supervised Learning with Quantum-Enhanced Feature Spaces (Havlíček et al., 2019).



The goal is to:

* translate the Havlíček quantum feature map into a **photonic setting**
* implement and simulate a **photonic quantum kernel**
* compare its performance with classical kernels (RBF) and Havlíček-style quantum kernels.



Comparison to Havlíček-style kernels was explored separately (see previous repository).

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Key idea**

In kernel-based supervised learning (e.g., SVM), we only need the kernel function



K(x,x′)=∣⟨ψ(x)∣ψ(x′)⟩∣^2



In the quantum setting, classical data is encoded into quantum states using a feature map and similarity is computed via state overlap. In this work classical data encoded into photonic states and feature space arises from interference in linear optics.

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Repository structure**

**PART 01: Basic Photonic Kernel**

**01-01. Feature map**

We translate quantum circuit elements into photonic components:

* Hadamard gate --> Beam splitter
* Data encoding --> Phase shifter
* Feature space --> Interference

We define a minimal feature map:

U(x) = B Φ(x) B

here B - Beam splitter, /Phi(x) - Phase shifter.

The unitary map is chosen in its simplest possible form. We compute and visualize the kernel matrix for a toy dataset.



**01-02. Training and Classification**

In this part kernel matrix is used with an SVM classifier to complete labeling task on the toy data set. Due to symmetry in phase encoding, many data points collapse into similar representations.

As a result the simple photonic kernel fails to separate classes on the second data set.



**01-03. Increasing expressivity**

We extended the feature map:

U(x) = B Φ₂(x) Φ₁(x) B

Modifying the phase structure of the feature map breaks symmetry in the relative phase and increases expressivity. This trial improved classification accuracy significantly (from 50% up to 100%).



**01-04: Decision Boundaries and Comparison**

Here we compare photonic kernel with classical RBF kernel first on the simple dataset used in part 01.02. As expected this time quantum kernel draw a decision boundary same as classical kernel showing successful phase modulation. To examine these methods further two-moons data set has been classified and corresponding decision boundaries estimated.

Result:

* Photonic kernel: 0.55 accuracy
* Classical RBF: 0.95 accuracy

Decision boundary comparison shows:

* the simple photonic kernel is too rigid to capture nonlinear geometry
* RBF kernel adapts better to nonlinear geometry.



**PART 02: Double-layer kernel**

In order to increase expressive power in feature map we add layer on the feature-map, which is basically two phase shifters separated by beam-splitters in-between.

We define the new photonic feature map:

U(x) = B Φ₂(x) B Φ₁(x) B

where B is a beam splitter and Φ\_1(x), Φ\_2(x) encodes classical data as phases.

Same work-flow as previous feature-map performed on this version too.

On the two-moons data set classification accuracy increased and even took higher value than Havlicek style kernel.

Result:

* Photonic kernel: 0.7 accuracy
* Classical RBF: 0.95 accuracy
* Havlicek kernel(see previous repo): 0.65 accuracy

However on simple two cluster data double-layer kernel overcomplicated the classification task and poorly performed on labeling.

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Main observations**

* Photonic kernel is **valid** and physically consistent
* It is **computationally lightweight**
* On simple datasets matches classical performance and produces similar classical boundaries
* On complex data sets it suffers from limited expressivity underperforms compared to RBF and Havlíček kernels.
* By modification or deepening the kernel we can control the feature-map geometry easily and make it more compatible to the data set geometry in interest
* However expressivity vs computational cost is a key trade-off.

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Conclusion**

This work demonstrates that a photonic implementation of a quantum kernel is feasible. Even simple linear-optical feature maps can perform classification. However, shallow photonic circuits have limited power.

The shallow photonic kernel is well matched to simple clustered data but lacks the expressive power required for strongly nonlinear datasets such as two moons.

Adding an additional interference layer increases expressivity and improves performance on nonlinear data, but may overcomplicate simple classification tasks.

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Next steps**

Possible future steps would be:

* extend to deeper photonic circuits
* explore multi-mode/multi-photon systems
* Investigate experimentally realizable implementations

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**How to run**

* Clone the repository:

    git clone <your-repo-link>

    cd photonic-kernel

* Install dependencies:

    pip install numpy matplotlib scikit-learn

* Open the notebook:

    jupyter notebook

* Run all cells in:

    Photonic\_kernel\_implementation\_Havlicek.ipynb



**Requirements**

\- Python 3.8+

\- NumPy

\- Matplotlib

\- scikit-learn



**Example Results**

Photonic Kernel (2-layer):

!\[photonic kernel](/2layer\_photonic\_kernel\_matrix\_2moons.png)



Classical RBF Kernel:

!\[classical kernel](/class\_kernel\_matrix\_2moons.png)
