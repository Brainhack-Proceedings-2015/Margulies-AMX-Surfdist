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
  street: Stephanstr 1a
  postcode: 04103
  city: Leipzig
  country: Germany

url: http://github.com/margulies/surfdist

coi: None

acknow: The authors would like to thank the organizers and attendees of Brainhack MX. The visualization functions were originally developed as part of Nilearn. We would like to thank the Nilearn developers, especially the organizers and participants of the Nilearn coding sprint 2015 in Paris.

contrib: DSM, MF, and JMH wrote the software and report.

bibliography: brainhack-report

gigascience-ref: REFXXX
...

#Introduction

<<<<<<< HEAD
The emergence of the human cerebral cortex, whether tracing it through phylogeny or ontogeny, tracks its expansion and progressive differentiation into larger and more diverse areas. While several previous methodologies have addressed this analytically by characterizing local cortical expansion, several lines of research have proposed that the cortex in fact expands along trajectories from primordial archor areas~\cite{Sanides1969-pa, Buckner2013-cs}, and furthermore, that the distance along the cortical surface is informative regarding cortical differentiation~\cite{Wagstyl2015-us}. We sought to investigate the geometric relationships that arise in the cortex based on expansion from such origin points. Towards this aim, we developed a python package for measuring the geodesic distance along the cortical surface that restricts shortest paths from passing through nodes of non-cortical areas such as the medial wall. 
=======
The emergence of the human cerebral cortex, whether tracing it through phylogeny or ontogeny, tracks its expansion and progressive differentiation into larger and more diverse areas. While previous methodologies have addressed this analytically by characterizing local cortical expansion, several lines of research have proposed that the cortex in fact expands along trajectories from primordial anchor areas~\cite{Sanides1969-pa, Buckner2013-cs}, and furthermore, that the distance along the cortical surface is informative regarding cortical differentiation~\cite{Wagstyl2015-us}. We sought to investigate the geometric relationships that arise in the cortex based on expansion from such origin points. Towards this aim, we developed a python package for measuring the geodesic distance along the cortical surface that restricts shortest paths through the non-cortical medial wall.
>>>>>>> 13e69143a82cf742d24da7d9051bf98a514198ab

#Approach

The calculation of geodesic distance along a mesh surface is based in the cumulative distance of the shortest path between two points. The first challenge that arises is the sensitivity of the calculation to the resolution of the mesh: the corser the mesh, the longer the shortest path may be, as the distance becomes progressively less direct. This problem has been previously addressed and subsequently implemented in the python package [gdist](https://pypi.python.org/pypi/gdist/), which calculates the exact geodesic distance along a mesh by subdividing the shortest path until a straight line along the cortex is approximated~\cite{Mitchell1987-iw}.

The second challenge, for which there was no prefabricated solution, is ensuring that the shortest path does not traverse non-cortical areas--- most prominently, the medial wall. It is therefore necessary to remove mesh nodes prior to calculating the exact geodesic, which requires reconstructing the mesh and assigning the respective new node indices for any seed regions-of-interest.

<<<<<<< HEAD
Finally, to facilitate applications to neuroscience research questions, we enabled the loading and visualization of data from commonly used formats such as FreeSurfer and the Human Connectome Project (HCP). A Nipype pipeline for group-level batch processing has also been made available. The pipeline is wrapped in a command-line interface and allows for straightforward distance calculations of entire FreeSurfer-preprocessed datasets. Group-level data are stored as CSV files for each requested mesh resolution, source label and hemisphere, facilitating further statistical analyses.
=======
Finally, to facilitate applications to neuroscience research questions, we enabled the loading and visualization of data from commonly used formats such as FreeSurfer and the Human Connectome Project (HCP). A Nipype ~\cite{Gorgolewski2011} pipeline for group-level batch processing has also been made available.
>>>>>>> 13e69143a82cf742d24da7d9051bf98a514198ab

#Results

The resultant package, SurfDist, achieves the aforementioned goals of faciliating the calculation of exact geodesic distance on the cortical surface. We present here the distance measures from the central sulcus label on the FreeSurfer fsaverage template and the HCP 32k_LR template (Figure \ref{keyfig}).

\begin{figure}[h!]
  \includegraphics[width=0.47\textwidth]{figure-01}
  \caption{\label{keyfig}
  (Top) Exact geodesic distance from the central sulcus on an individual pial surface.
  (Bottom) Zones based on proximity to the central or calcarine sulcus.
  }
\end{figure}

The zone analysis provides a means to construct a Voronoi diagram based on a set of individual nodes or sets of nodes.

Surface rendering of the results is based on plotting functions as implemented in Nilearn ~\cite{Abraham2014} and exclusively relies on the common library matplotlib to minimize dependencies. The visualization applies sensible defaults but can flexibly be adapted to different views, colormaps and thresholds as well as shadowing using a sulcal depth map. Figures can be embedded directly in an IPython Notebook [Link].

#Conclusions

The SurfDist package is designed to enable investigation of intrinisic geometric properties of the cerebral cortex.
