# 3D Magnetic Inversion & Regional Detrending with SimPEG
In potential field inversions, numerical solvers will always converge to a mathematical minimum. However, without rigorous regional decoupling and interactive misfit inspection, the resulting model can easily misinterpret regional gradients or high-frequency noise as artificial deep targets.

In this recent workflow, I integrated Python with the SimPEG (v0.25.2) open-source framework to build an end-to-end, geology-driven 3D magnetic inversion pipeline.

Here is how the workflow is structured:

1. Regional-Residual Decoupling Constrained by Aeromagnetics

The standalone Python script for regional trend fitting and residual extraction is available in regional_detrending.ipynb

<img width="1395" height="1000" alt="image" src="https://github.com/user-attachments/assets/5baabbb6-5dc7-4909-8441-8fe56126f14e" />

Rather than relying on arbitrary polynomial filtering across a localized ground survey, we anchored our ground magnetic data into a 20x20 km aeromagnetic framework (500m Upward :low-pass filtered). Fitting a regional trend plane ensured that the residual magnetic anomaly entering the inversion mesh strictly reflects prospective deposit-scale lithologies and hydrothermal alteration corridors.

2. Interactive Spatial Misfit & Quality Control
<img width="1292" height="528" alt="image" src="https://github.com/user-attachments/assets/43fdc2fe-6f01-4448-822e-119fe35e2752" />

Inversion shouldn't be an opaque "black-box" run. Using custom interactive Jupyter widgets, we tracked observed vs. predicted data and spatial normalized misfit across every iteration.

Why Iteration 18? Starting from standard 𝐿2-norm regularization (which reached target misfit at Iter 15), we transitioned into Iteratively Reweighted Least Squares (IRLS). Iteration 18 represents the structural "sweet spot" — sharpening the boundaries of the magnetic source without over-sparsifying continuous geological features.

3. Regularization Diagnostics & Model Statistics

<img width="1262" height="702" alt="image" src="https://github.com/user-attachments/assets/c7a5ce74-47b8-426b-85b9-97d251fff544" />
<img width="1244" height="815" alt="image" src="https://github.com/user-attachments/assets/c8d85362-5a85-4501-8d25-428d3f96ab95" />
Tikhonov Curve (𝜙𝑑 vs 𝜙𝑚): Verifies the cooling schedule of the trade-off parameter (𝛽) and monitors the transition from smooth inversion to IRLS compact steps.

Susceptibility Distribution: A logarithmic inspection confirms physically realistic susceptibility values, effectively isolating mineralized cores from barren host rocks.

4. Dynamic 3D Structural Targeting

<img width="1390" height="863" alt="image" src="https://github.com/user-attachments/assets/b0112185-98ca-4f54-b1ba-f33a5dbabdd3" />
The payoff: Inverting over 285,000 active subsurface cells with active topography and a distance-weighting penalty yields an unaliased, dipping 3D magnetic body (filtered at >0.08 SI threshold) that correlates with the known tectonic and mineralization corridor.

Transparent, reproducible, and open-source workflows like this significantly de-risk exploration programs before drilling begins.

Big thanks to the open-source geophysics community and contributors like Lindsey Heagy , Dominique Fournier , SEOGI KANG and Joseph Capriotti for maintaining such a powerful foundation in SimPEG.

 To fellow explorationists and geophysicists: When using IRLS or compact norms, at what stage do you prefer to freeze your iterations to avoid over-sparsification? Looking forward to hearing your experiences!

#Geophysics #SimPEG #Python #MineralExploration #3DInversion #Magnetics #MiningTech #OpenGeoscience #DataScience
