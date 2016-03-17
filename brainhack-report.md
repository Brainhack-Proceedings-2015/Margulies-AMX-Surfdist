---
event: '2015 Brainhack Americas (MX)'

title:  'A cortical surface-based geodesic distance package for Python'

author:

- initials: DS
  surname: Margulies
  firstname: Daniel S
  email: margulies@cbs.mpg.de
  affiliation: aff1
  corref: aff1

- initials: M
  surname: Falkiewicz
  firstname: Marcel
  email: falkiewicz@cbs.mpg.de
  affiliation: aff1
  corref: aff1

- initials: JM
  surname: Huntenburg
  firstname: Julia M
  email: huntenburg@cbs.mpg.de
  affiliation: aff1
  corref: aff1

affiliations:

- id: aff1
  orgname: 'Max Planck Research Group for Neuroanatomy & Connectivity,\
  Max Planck Institute for Human Cognitive and Brain Sciences'
  street: Stephanstraße 1a
  postcode: 04103
  city: Leipzig
  country: Germany

url: http://github.com/margulies/surfdist

coi: None

acknow: The authors would like to thank the organizers and attendees of Brainhack MX. The visualization functions were originally developed during the Nilearn coding sprint 2015 in Paris, for which we would also like to thank the organizers and participants of this event.

contrib: DSM, MF, and JMH wrote the software and report.

bibliography: brainhack-report

gigascience-ref: REFXXX
...

#Introduction

The human cerebral cortex, whether tracing it through phylogeny or ontogeny, emerges through expansion and progressive differentiation into larger and more diverse areas. While current methodologies address this analytically by characterizing local cortical expansion in the form of surface area~\cite{winkler2012}, several lines of research have proposed that the cortex in fact expands along trajectories from primordial anchor areas~\cite{Sanides1969-pa, Buckner2013-cs}, and furthermore, that the distance along the cortical surface is informative regarding cortical differentiation~\cite{Wagstyl2015-us}. We sought to investigate the geometric relationships that arise in the cortex based on expansion from such origin points. Towards this aim, we developed a Python package for measuring the geodesic distance along the cortical surface that restricts shortest paths from passing through nodes of non-cortical areas such as the non-cortical portions of the surface mesh described as the `medial wall'. 

#Approach

The calculation of geodesic distance along a mesh surface is based in the cumulative distance of the shortest path between two points. The first challenge that arises is the sensitivity of the calculation to the resolution of the mesh: the corser the mesh, the longer the shortest path may be, as the distance becomes progressively less direct. This problem has been previously addressed and subsequently implemented in the Python package [gdist](https://pypi.python.org/pypi/gdist/), which calculates the exact geodesic distance along a mesh by subdividing the shortest path until a straight line along the cortex is approximated~\cite{Mitchell1987-iw}.

The second challenge, for which there was no prefabricated solution, was ensuring that the shortest path only traverses territory within the cortex proper, avoiding shortcuts through non-cortical areas included in the surface mesh --- most prominently, the non-cortical portions along the medial wall. Were the shortest paths between two nodes to traverse non-cortical regions, the distance between nodes would be artificially decreased, which would have artifactual impact on the interpretation of results. This concern would be especially relevent to the `zones analysis' described below, where the boundaries between regions would be altered. It was therefore necessary to remove mesh nodes prior to calculating the exact geodesic, which requires reconstructing the mesh and assigning the respective new node indices for any seed regions-of-interest.

Finally, to facilitate applications to neuroscience research questions, we enabled the loading and visualization of data from commonly used formats such as FreeSurfer and the Human Connectome Project (HCP). A Nipype pipeline for group-level batch processing has also been made available~\cite{Gorgolewski2011}. The pipeline is wrapped in a command-line interface and allows for straightforward distance calculations of entire FreeSurfer-preprocessed datasets. Group-level data are stored as CSV files for each requested mesh resolution, source label and hemisphere, facilitating further statistical analyses.

#Results

The resultant package, SurfDist, achieves the aforementioned goals of faciliating the calculation of exact geodesic distance on the cortical surface. We present here the distance measures from the central sulcus label on the FreeSurfer native surfaces (Figure \ref{keyfig}, \emph(Top)). The distance measure provides a means to parcellate the cortex using the surface geometry. Towards that aim, we also implement a `zones analysis', which constructs a Voronoi diagram, establishing partitions based on the greater proximity to a set of label nodes (Figure \ref{keyfig}B).

\begin{figure}[h!]
  \includegraphics[width=0.47\textwidth]{figure-01}
  \caption{\label{keyfig}
  (A) FreeSurfer labels delineated from the central and calcarine sulci depicted on the individual inflated surface.
  (B) Schematic indicated the difference between the distance (C) and zones (D) analyses. 
  (C) Exact geodesic distance from the central sulcus on an individual pial surface.
  (D) Zones based on proximity to the central (red) or calcarine (blue) sulci.
  }
\end{figure}

Surface rendering of the results draws from plotting functions as implemented in Nilearn ~\cite{Abraham2014} and exclusively relies on the common library matplotlib to minimize dependencies. The visualization applies sensible defaults but can flexibly be adapted to different views, colormaps and thresholds as well as shadowing using a sulcal depth map.

#Conclusions

The SurfDist package is designed to enable investigation of intrinisic geometric properties of the cerebral cortex based on geodesic distance measures. Towards the aim of enabling applications specific to neuroimaging-based research question, we have designed the package to facilitate analysis and visualization of geodesic distance metrics using standard cortical surface meshes. 
