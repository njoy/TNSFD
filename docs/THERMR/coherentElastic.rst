
.. _coherentElastic:

**********************
Coherent Elastic
**********************

In crystalline solids consisting of coherent scatterers [i.e. materials with relatively large bound coherent scattering cross sections], the so-called "zero-phonon term" leads to interference scattering from the various planes of atoms of the crystal making up the solid. There is no energy loss/gain in such events, and are described using the coherent elastic cross section formula:

.. math::
  \sigma^{coh}(E,E',\mu) = \frac{\sigma_{coh}}{E}~\sum_{E_i>E}f_i~\mathrm{e}^{-2WE_i}~\delta(\mu-\mu_0)~\delta(E-E')

where 

.. math::
  \mu_0=1-\frac{2E_i}{E}.

Here, :math:`E` is the incident neutron energy, :math:`E'` is the secondary neutron energy, :math:`\mu` is the scattering cosine in the laboratory reference system, :math:`\sigma_{coh}` is the characteristic bound coherent scattering cross section of the material, :math:`W` is the Debye-Waller Coefficient (which is a function of temperature), :math:`E_i` are the locations in energy of the Bragg-edges, and :math:`f_i` are the related to crystallographic structures. 


For select materials, LEAPR prepares the coherent elastic scattering data and writes the data into the MF=7/MT=2 ENDF-6 section. THERMR may then take those Bragg peak locations and weights, calculate the cross section, and write the output coherent elastic cross sections to the MF=3 file of the output PENDF.

.. locations :math:`E_i` and the :math:`f_i` factors (which are both material and temperature dependent).






