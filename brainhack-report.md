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

- initials: J
  surname: Huntenburg
  firstname: Julia
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

acknow: The authors would like to thank the organizers and attendees of Brainhack MX.

contrib: DSM, MF, and JH wrote the software and report.
  
bibliography: brainhack-report

gigascience-ref: REFXXX
...

#Introduction

The emergence of the human cerebral cortex, whether tracing it through phylogeny or ontogeny, tracks its expansion and progressive differentiation into larger and more diverse areas. While several previous methodologies have addressed this analytically by characterizing local cortical expansion, several lines of research have proposed that the cortex in fact expands along trajectories from primordial archor areas. We sought to investigate the geometric relationships that arise in the cortex based on expansion from such origin points. Towards this aim, we developed a python package for measuring the geodesic distance along the cortical surface that restricts shortest paths through the non-cortical medial wall. 

#Approach

The calculation of geodesic distance along a mesh surface is based in the cumulative distance of the shortest path between two points. The first challenge that arises is the sensitivity of the calculation to the resolution of the mesh: the corser the mesh, the longer the shortest path may be, as the distance becomes progressively less direct. This problem has been previously addressed and subsequently implemented in the python package [gdist](https://pypi.python.org/pypi/gdist/), which calculates the exact geodesic distance along a mesh by estimating... 

The second challenge, for which there was no prefabricated solution, is ensuring that the shortest path does not tranverse non-cortical areas--- most prominently, the medial wall. It is therefore necessary to remove mesh nodes prior to calculating the exact geodesic, which requires reconstructing the mesh and calculating the respective new node indices for any seed regions-of-interest. 

Finally, to facilitate applications to neuroscience research questions, we enabled the loading and visualization of data from commonly used formats such as FreeSurfer and the Human Connectome Project (HCP). A Nipype pipeline for group-level batch processing has also been made available.

#Results

The resultant package, SurfDist, achieves the aforementioned goals of faciliating the calculation of exact geodesic distance on the cortical surface. We present here the distance measures from the central sulcus label on the FreeSurfer fsaverage template and the HCP 32k_LR template (Figure \ref{keyfig}). 

In addition, it is possible to embed the figures in an IPython Notebook [Link].

#Conclusions

The SurfDist package enables  

\begin{figure}
  \includegraphics[width=0.45\textwidth]{figure-01}
  \caption{\label{keyfig}
  (a)
  (b)
  (c)
  }
\end{figure}

