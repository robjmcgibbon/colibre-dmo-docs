Welcome to the COLIBRE documentation
====================================

This service provides documentation for the dark matter only (DMO) runs of the
`COLIBRE simulations <https://colibre.strw.leidenuniv.nl/>`__.

Publications making use of the public COLIBRE data are kindly requested to:

  * Cite the two papers presenting the COLIBRE project:
    `Schaye et al (2026) <https://ui.adsabs.harvard.edu/abs/2026MNRAS.548ag375S>`__
    and `Chaikin et al (2026) <https://ui.adsabs.harvard.edu/abs/2026MNRAS.548ag300C>`__.

  * Add the following statement to the acknowledgements:

      *We acknowledge the Virgo Consortium for making their simulation data
      available. The COLIBRE simulations were performed using the Durham
      Memory Intensive system managed by the Institute for Computational
      Cosmology on behalf of the STFC DiRAC facility (www.dirac.ac.uk).*

The data from the COLIBRE hydrodynamical simulations will be made publicly available
at a later date. In the meantime, people interested in using the hydrodynamical
simulations are encouraged to contact one of the
`team members <https://colibre.strw.leidenuniv.nl/team.html>`__.

Questions about the DMO data can be sent to
`colibre-questions@strw.leidenuniv.nl <mailto:colibre-questions@strw.leidenuniv.nl>`__.


COLIBRE simulation data products
--------------------------------

The following data products are available:

* :doc:`snapshots/index` of the full distribution of dark matter particles
  at a :doc:`series of output times <snapshots/snapshot_redshifts>` between
  redshift z=30 and the present day.

* :doc:`Halo catalogues and merger trees <soap/index>` generated using the `HBT-HERONS
  <https://hbt-herons.strw.leidenuniv.nl/>`__ halo finder (`Forouhar
  Moreno et al. 2025
  <https://ui.adsabs.harvard.edu/abs/2025arXiv250206932F/abstract>`__)
  with a wide range of halo properties computed using the `SOAP
  <https://github.com/SWIFTSIM/SOAP>`__
  post-processing tool (`McGibbon et al. 2025
  <https://ui.adsabs.harvard.edu/abs/2025JOSS...10.8252M/abstract>`__).

* :doc:`power_spectra/index` of the matter distribution.

See the links in the side bar on the left for full descriptions
of the available data products, and example scripts.

Analysis of data products
-------------------------

The data is served over the web, see :doc:`How to use this service </service_docs/index>`.

A collection of helpful tools and examples can be found :doc:`on this page </tools/index>`.

.. toctree::
   :maxdepth: 2
   :hidden:

   How to use this service <service_docs/index>
   simulations/index
   snapshots/index
   Halo catalogues <soap/index>
   power_spectra/index
   tools/index
   issues/index
   questions/index
