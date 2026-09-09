Simulations
===========

The COLIBRE dark matter only (DMO) simulations were run with the same initial
phases and the same total number of particles as the corresponding
hydrodynamical runs. To create the initial conditions for a DMO simulation,
the baryonic particles of the corresponding hydrodynamical run were converted
into CDM particles.

The hydrodynamical initial conditions contain one baryonic particle for every
four CDM particles. Since :math:`\Omega_{\rm b}` is not exactly a quarter of
:math:`\Omega_{\rm CDM}`, the two species do not have the same particle mass,
and this carries over into the DMO runs: one particle in five is lighter than
the other four. The tables below therefore quote the mean particle mass,

.. math::

   \bar{m} = \frac{m_{\rm b} + 4\,m_{\rm CDM}}{5},

where :math:`m_{\rm b}` is the mass of the converted baryonic particles and
:math:`m_{\rm CDM}` that of the original CDM particles. Both masses are given
for each resolution below. The columns list the simulation identifier; the
comoving box side length, L; the number of CDM particles, N :sub:`CDM`; the
mean CDM particle mass, :math:`\bar{m}`; the Plummer-equivalent comoving
gravitational softening length, ε :sub:`com`; and the maximum proper
gravitational softening length, ε :sub:`prop`.

Available simulations
---------------------

m5 resolution
~~~~~~~~~~~~~

The converted baryonic particles have a mass of :math:`2.30 \times 10^5\ \rm{M}_\odot` and the original CDM particles :math:`3.03 \times 10^5\ \rm{M}_\odot`.

.. list-table::
   :header-rows: 1
   :widths: 20 12 22 20 13 13
   :align: center
   :class: simulation-table row-divider

   * - Identifier
     - L (cMpc)
     - N :sub:`CDM`
     - :math:`\bar{m}` (M :sub:`☉`)
     - ε :sub:`com` (ckpc)
     - ε :sub:`prop` (pkpc)
   * - **L100m5**
     - 100
     - :math:`5 \times 3008^3`
     - :math:`2.88 \times 10^5`
     - 0.9
     - 0.35
   * - **L050m5**
     - 50
     - :math:`5 \times 1504^3`
     - :math:`2.88 \times 10^5`
     - 0.9
     - 0.35
   * - **L025m5**
     - 25
     - :math:`5 \times 752^3`
     - :math:`2.88 \times 10^5`
     - 0.9
     - 0.35
   * - **L012m5**
     - 12.5
     - :math:`5 \times 376^3`
     - :math:`2.88 \times 10^5`
     - 0.9
     - 0.35

m6 resolution
~~~~~~~~~~~~~

The converted baryonic particles have a mass of :math:`1.84 \times 10^6\ \rm{M}_\odot` and the original CDM particles :math:`2.42 \times 10^6\ \rm{M}_\odot`.

.. list-table::
   :header-rows: 1
   :widths: 20 12 22 20 13 13
   :align: center
   :class: simulation-table row-divider

   * - Identifier
     - L (cMpc)
     - N :sub:`CDM`
     - :math:`\bar{m}` (M :sub:`☉`)
     - ε :sub:`com` (ckpc)
     - ε :sub:`prop` (pkpc)
   * - **L200m6**
     - 200
     - :math:`5 \times 3008^3`
     - :math:`2.30 \times 10^6`
     - 1.8
     - 0.7
   * - **L100m6**
     - 100
     - :math:`5 \times 1504^3`
     - :math:`2.30 \times 10^6`
     - 1.8
     - 0.7
   * - **L050m6**
     - 50
     - :math:`5 \times 752^3`
     - :math:`2.30 \times 10^6`
     - 1.8
     - 0.7
   * - **L025m6**
     - 25
     - :math:`5 \times 376^3`
     - :math:`2.30 \times 10^6`
     - 1.8
     - 0.7

m7 resolution
~~~~~~~~~~~~~

The converted baryonic particles have a mass of :math:`1.47 \times 10^7\ \rm{M}_\odot` and the original CDM particles :math:`1.94 \times 10^7\ \rm{M}_\odot`.

.. list-table::
   :header-rows: 1
   :widths: 20 12 22 20 13 13
   :align: center
   :class: simulation-table row-divider

   * - Identifier
     - L (cMpc)
     - N :sub:`CDM`
     - :math:`\bar{m}` (M :sub:`☉`)
     - ε :sub:`com` (ckpc)
     - ε :sub:`prop` (pkpc)
   * - **L400m7**
     - 400
     - :math:`5 \times 3008^3`
     - :math:`1.85 \times 10^7`
     - 3.6
     - 1.4
   * - **L200m7**
     - 200
     - :math:`5 \times 1504^3`
     - :math:`1.85 \times 10^7`
     - 3.6
     - 1.4
   * - **L100m7**
     - 100
     - :math:`5 \times 752^3`
     - :math:`1.85 \times 10^7`
     - 3.6
     - 1.4
   * - **L050m7**
     - 50
     - :math:`5 \times 376^3`
     - :math:`1.85 \times 10^7`
     - 3.6
     - 1.4
   * - **L025m7**
     - 25
     - :math:`5 \times 188^3`
     - :math:`1.85 \times 10^7`
     - 3.6
     - 1.4

Directory layout and naming conventions
---------------------------------------

All simulations are kept under ``COLIBRE`` on the data service. The simulations are divided into subdirectories based on their box size and mass resolution with names of the form ``LXXX_mY``. The value of ``XXX`` corresponds to the simulation box side length in comoving Mpc, and the value of ``Y`` is the mass resolution. For example, the directory ``L100_m6`` contains all simulations run in a :math:`100\rm{Mpc}^3` box at :math:`m_{dm} \approx 10^6 \rm{M_\odot}` resolution. Within each simulation directory there are subdirectories for the available data products.

.. mermaid::

   flowchart LR
     colibre["`**Project root**
     .../colibre/Runs/`"]

     colibre --> L100_m6["`**Box size and resolution**
     L100_m6/
     L200_m6/
     ...`"]

     L100_m6-->DMO["`**Run name**
     DMO/`"]

     DMO-->snapshots["**Snapshot data**
     snapshots/"]
     DMO-->soap["**Halo catalogues**
     SOAP-HBT/
     HBT-HERONS/"]
     DMO-->powerspec["**Power spectra**
     power_spectra/"]


