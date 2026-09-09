.. _snapshot_particle_properties:

Particle properties
===================

This page documents all of the properties which are stored for each
dark matter particle in a COLIBRE snapshot. The first column in the table gives the
name of the property when opened using the swiftsimio library.
Clicking on each property name will open a dropdown box,
which contains information about the dataset within the HDF5 file.
The second column gives a description of the property.

.. note:: Units are provided here for information, but it's usually
          better to use the metadata in the files for any unit
          conversions. The `swiftsimio
          <https://swiftsimio.readthedocs.io/en/latest/loading_data/index.html>`__
          python module handles units automatically in snapshots and
          SOAP halo catalogues.

Dark matter particles
---------------------

.. list-table::
   :header-rows: 1

   * - Name
     - Description
   * - .. dropdown:: ``coordinates``

          * **HDF5 name:** ``Coordinates``
          * **Shape:** 3
          * **Datatype:** float64
          * **Units:** :math:`a \cdot \rm{Mpc}`
          * **Compression:** 1 pc accurate
     - Co-moving position of the particles
   * - .. dropdown:: ``fofgroup_ids``

          * **HDF5 name:** ``FOFGroupIDs``
          * **Shape:** 1
          * **Datatype:** int64
          * **Units:** dimensionless
          * **Compression:** Store less bits
     - Friends-Of-Friends ID of the group the particles belong to
   * - .. dropdown:: ``halo_catalogue_index``

          * **HDF5 name:** ``HaloCatalogueIndex``
          * **Shape:** 1
          * **Datatype:** int64
          * **Units:** dimensionless
          * **Compression:** no compression
     - Index of halo in which this particle is a bound member, or -1 if none
   * - .. dropdown:: ``masses``

          * **HDF5 name:** ``Masses``
          * **Shape:** 1
          * **Datatype:** float32
          * **Units:** :math:`10^{10}\ \rm{M}_\odot`
          * **Compression:** no compression
     - Masses of the particles
   * - .. dropdown:: ``particle_ids``

          * **HDF5 name:** ``ParticleIDs``
          * **Shape:** 1
          * **Datatype:** uint64
          * **Units:** dimensionless
          * **Compression:** Store less bits
     - Unique ID of the particles
   * - .. dropdown:: ``potentials``

          * **HDF5 name:** ``Potentials``
          * **Shape:** 1
          * **Datatype:** float32
          * **Units:** :math:`a^{-1.0} \cdot \rm{km}^{2} / \rm{s}^{2}`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - Gravitational potentials of the particles
   * - .. dropdown:: ``rank_bound``

          * **HDF5 name:** ``Rank_bound``
          * **Shape:** 1
          * **Datatype:** int64
          * **Units:** dimensionless
          * **Compression:** no compression
     - Ranking by binding energy of the bound particles (first in halo=0), or -1 if not bound
   * - .. dropdown:: ``specific_potential_energies``

          * **HDF5 name:** ``SpecificPotentialEnergies``
          * **Shape:** 1
          * **Datatype:** float32
          * **Units:** :math:`\rm{km}^{2} / \rm{s}^{2}`
          * **Compression:** no compression
     - Specific potential energy of the bound particles
   * - .. dropdown:: ``velocities``

          * **HDF5 name:** ``Velocities``
          * **Shape:** 3
          * **Datatype:** float32
          * **Units:** :math:`\rm{km} / \rm{s}`
          * **Compression:** 0.1 km/s accurate
     - Peculiar velocities of the particles. This is :math:`a \frac{dx}{dt}` where :math:`x` is the co-moving position of the particles.
