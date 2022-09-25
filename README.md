<p align="center">
  <img alt="📊SDP__HCGM_vs_Vu-Condat" src="https://user-images.githubusercontent.com/62103572/183293118-4471f748-6b26-46c3-80cc-1a37633483f1.png">
  <img alt="GitHub commit activity" src="https://img.shields.io/github/commit-activity/y/EliaFantini/HCGM-and-VuCondat-for-Semidefinite-Programming">
  <img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/EliaFantini/HCGM-and-VuCondat-for-Semidefinite-Programming">
  <img alt="GitHub code size" src="https://img.shields.io/github/languages/code-size/EliaFantini/HCGM-and-VuCondat-for-Semidefinite-Programming">
  <img alt="GitHub repo size" src="https://img.shields.io/github/repo-size/EliaFantini/HCGM-and-VuCondat-for-Semidefinite-Programming">
  <img alt="GitHub follow" src="https://img.shields.io/github/followers/EliaFantini?label=Follow">
  <img alt="GitHub fork" src="https://img.shields.io/github/forks/EliaFantini/HCGM-and-VuCondat-for-Semidefinite-Programming?label=Fork">
  <img alt="GitHub watchers" src="https://img.shields.io/github/watchers/EliaFantini/HCGM-and-VuCondat-for-Semidefinite-Programming?label=Watch">
  <img alt="GitHub star" src="https://img.shields.io/github/stars/EliaFantini/HCGM-and-VuCondat-for-Semidefinite-Programming?style=social">
</p>

Semidefinite programming (SDP) is a subfield of convex optimization concerned with the optimization of a linear objective function (a user-specified function that the user wants to minimize or maximize) over the intersection of the cone of positive semidefinite matrices with an affine space, i.e., a spectrahedron. This project aims at using SDP to solve two problems.

The first problem is image classification on the famous dataset Fashion-MNIST, using k-means clustering. Jiming Peng and Yu Wei's paper [Approximating K-means-type clustering via semidefinite programming](https://optimization-online.org/2005/04/1114/) proposes an SDP-relaxation to approximately solve the aforementioned model-free
k−means clustering problem. To solve it, I implemented two optimization methods: Homotopy Conditional Gradient Method(HCGM) and the Vu-Condat method.

The second problem is computing a geometric embedding the Uniform Sparsest Cut problem (USC), which aims to find a bipartition (S, S¯) of the nodes of a graph G = (V, E), |V| = p, which minimizes the quantity E(S, S¯)/(|S |*|S¯|), where E(S, S¯) is the number of edges connecting S and S¯, and |S | is the number of nodes in S . This problem is of broad interest, with applications in areas such as VLSI layout design, topological design of communication networks and image segmentation. Computing such a bipartition is NP-hard and intense research has gone into designing efficient approximation algorithms for this problem. The paper [Expander flows, geometric embeddings and graph partitioning](https://dl.acm.org/doi/10.1145/1502793.1502794) proposes an O(p*log p) approximation algorithm for solving USC, which relies on finding a well-spread geometric representation of G where each node i ∈ V is mapped to a vector v_i in R^p. I used the HCGM method to compute this geometric embedding.


For a more detailed explanation of the concepts mentioned above, please read *Exercise instructions.pdf*, it contains also some theoretical questions answered in *Answers.pdf* (handwritten). 

The project was part of an assignment for the EPFL course [EE-556 Mathematics of data: from theory to computation](https://edu.epfl.ch/coursebook/en/mathematics-of-data-from-theory-to-computation-EE-556). The backbone of the code structure to run the experiments was already given by the professor and his assistants, what I had to do was to implement the core theoretical concepts to actually make the experiments work. Hence, every code file is a combination of my personal code and the code that was given us by the professor.

## Author
-  [Elia Fantini](https://github.com/EliaFantini)

## Fashion-MNIST classification results

The following images show some examples of images from the Fashion-MNIST dataset and the related prediction after training with either HCGM or Vu-Condat method.
<p align="center">
<img height="500" alt="Immagine 2022-08-07 155808" src="https://user-images.githubusercontent.com/62103572/183294389-0f1b79b6-2b9a-47fd-abdb-a41f0a08818d.png">
</br>
<img height="500" alt="Immagine 2022-08-07 155838" src="https://user-images.githubusercontent.com/62103572/183294390-63e4b401-c3d2-48e7-b296-fa7366fb8e09.png">
</p>

This plot shows a clearer comparison of the performance of the two methods, where PDHG (Primal-dual hybrid gradient) is Vu-Condat method:
<p align="center">
<img width="600" alt="Immagine 2022-08-07 160347" src="https://user-images.githubusercontent.com/62103572/183294627-35655034-517b-4630-a8fc-71fe97fa6e24.png">
</p>

## Results of geometric embedding for the Sparsest Cut Problem 

Running the algorithm for the 25 nodes graph I obtained the plots shown in the figure below and a running time of 106 seconds, while running the 55 nodes took 1189 seconds. Finally, the 102 nodes dataset took 7645 seconds. From such  results we can see that the number of constraints to be computed is a big bottleneck of this solution on big graphs, since doubling the number of nodes makes the algorithm almost 10 times slower. 
<p align="center">
<img width="500" alt="Immagine 2022-08-07 160953" src="https://user-images.githubusercontent.com/62103572/183294839-7d5adffa-c57c-4181-8a4f-c9e2c9e5a4d9.png">
</p>

## How to install and reproduce results
Download this repository as a zip file and extract it into a folder
The easiest way to run the code is to install Anaconda 3 distribution (available for Windows, macOS and Linux). To do so, follow the guidelines from the official
website (select python of version 3): https://www.anaconda.com/download/

Additional package required are: 
- matplotlib
- scipy
- jupyter notebooks

To install them write the following command on Anaconda Prompt (anaconda3):
```shell
cd *THE_FOLDER_PATH_WHERE_YOU_DOWNLOADED_AND_EXTRACTED_THIS_REPOSITORY*
```
Then write for each of the mentioned packages:
```shell
conda install *PACKAGE_NAME*
```
Some packages might require more complex installation procedures. If the above command doesn't work for a package, just google "How to install *PACKAGE_NAME* on *YOUR_MACHINE'S_OS*" and follow those guides.

Finally, run the two jupyter notebooks **Test_clustering.ipynb** and **Test_sparsest_cut.ipynb**. 

## Files description

- **code/geometric_embedding/**: folder containing all the code and dataset to perform the SDP k-means clustering, the jupyter notebook **Test_clustering.ipynb** is the one to run to obtain all the results.

-  **code/image_classification/**: folder containing all the code and dataset to perform the SDP geometric embedding for USC, the jupyter notebook **Test_sparsest_cut.ipynb** is the one to run to obtain all the results.

- **Answers.pdf**: pdf with the answers and plots to the assignment of the course

- **Exercise instructions.pdf**: pdf with the questions of the assignment of the course

## 🛠 Skills
Python, Matplotlib, Jupyter notebooks, Scipy. Machine learning, Semidefinite programming, k-means clustering, Homotopy Conditional Gradient and Primal-dual hybrid gradient (Vu_Condat) methods, geometric embedding  for Sparsest Cut problem.

## 🔗 Links
[![portfolio](https://img.shields.io/badge/my_portfolio-000?style=for-the-badge&logo=ko-fi&logoColor=white)](https://eliafantini.github.io/Portfolio/)
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/-elia-fantini/)
