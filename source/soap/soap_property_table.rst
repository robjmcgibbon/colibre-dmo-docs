.. _soap_property_table:

SOAP properties table
=====================

The tables below list the (sub)halo properties available within the SOAP catalogues. The first table contains the properties within the ``input_halos`` group.
The second table contains the properties calculated for the dark matter only simulations.
The final table contains the datasets copied over from the HBT-HERONS and FoF catalogues.
Within each table the properties are sorted based on their filters.
The bottom of the page contains a number of footnotes, which give further explanation as to how different properties are computed.

The first column gives the name of the property when opened using the `swiftsimio library <https://swiftsimio.readthedocs.io/en/latest/soap/index.html>`_. Clicking on each property name will open a dropdown box, which contains information about the dataset within the HDF5 file. The second column gives the filter applied to that property, as described in :doc:`soap_filters`. The third column indicates the halo variations for which this property is available (:avail:`green` if the property is computed for a certain variation, :unavail:`red` if not computed for that variation). The variations are as follows:

* ``BS`` - :ref:`bound_subhalo_description`
* ``ES`` - :ref:`exclusive_sphere_description`
* ``IS`` - :ref:`inclusive_sphere_description`
* ``EP`` - :ref:`projected_aperture_description`
* ``SO`` - :ref:`spherical_overdensity_description`

The final column gives a description of the property. Certain properties also contain a link to a footnote at the bottom of this page which gives a full description of how they were calculated.

Input halo properties
---------------------

.. list-table::
   :widths: 25 10 15 50
   :header-rows: 1

   * - Name
     - Filter
     - Variations
     - Description
   * - .. dropdown:: ``input_halos.halo_catalogue_index``

          * **HDF5 name:** ``InputHalos/HaloCatalogueIndex``
          * **Shape:** 1
          * **Type:** int64
          * **Units:** dimensionless
          * **Compression:** no compression
     - basic
     - \-
     - Index of this halo in the original halo finder catalogue (first halo has index=0).
   * - .. dropdown:: ``input_halos.halo_centre``

          * **HDF5 name:** ``InputHalos/HaloCentre``
          * **Shape:** 3
          * **Type:** float64
          * **Units:** :math:`a \cdot \rm{Mpc}`
          * **Compression:** 1 pc accurate
     - basic
     - \-
     - The centre of the subhalo as given by the halo finder. Used as reference for all relative positions. For VR and HBTplus this is equal to the position of the most bound particle in the subhalo.
   * - .. dropdown:: ``input_halos.is_central``

          * **HDF5 name:** ``InputHalos/IsCentral``
          * **Shape:** 1
          * **Type:** int64
          * **Units:** dimensionless
          * **Compression:** no compression
     - basic
     - \-
     - Whether the halo finder flagged the halo as central (1) or satellite (0).
   * - .. dropdown:: ``input_halos.number_of_bound_particles``

          * **HDF5 name:** ``InputHalos/NumberOfBoundParticles``
          * **Shape:** 1
          * **Type:** int64
          * **Units:** dimensionless
          * **Compression:** no compression
     - basic
     - \-
     - Total number of particles bound to the subhalo.

Halo properties
---------------

.. list-table::
   :widths: 25 10 15 50
   :header-rows: 1

   * - Name
     - Filter
     - Variations
     - Description
   * - .. dropdown:: ``centre_of_mass``

          * **HDF5 name:** ``CentreOfMass``
          * **Shape:** 3
          * **Type:** float64
          * **Units:** :math:`a \cdot \rm{Mpc}`
          * **Compression:** 1 pc accurate
     - basic
     - :avail:`BS` :avail:`ES` :avail:`IS` :avail:`EP` :avail:`SO`
     - Centre of mass. `[1] <footnote-1_>`_
   * - .. dropdown:: ``centre_of_mass_velocity``

          * **HDF5 name:** ``CentreOfMassVelocity``
          * **Shape:** 3
          * **Type:** float32
          * **Units:** :math:`\rm{km} / \rm{s}`
          * **Compression:** 0.1 km/s accurate
     - basic
     - :avail:`BS` :avail:`ES` :avail:`IS` :avail:`EP` :avail:`SO`
     - Centre of mass velocity. `[1] <footnote-1_>`_
   * - .. dropdown:: ``concentration``

          * **HDF5 name:** ``Concentration``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** dimensionless
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - basic
     - :unavail:`BS` :unavail:`ES` :unavail:`IS` :unavail:`EP` :avail:`SO`
     - Halo concentration assuming an NFW profile. Minimum particle radius set to softening length `[2] <footnote-2_>`_
   * - .. dropdown:: ``concentration_unsoftened``

          * **HDF5 name:** ``ConcentrationUnsoftened``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** dimensionless
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - basic
     - :unavail:`BS` :unavail:`ES` :unavail:`IS` :unavail:`EP` :avail:`SO`
     - Halo concentration assuming an NFW profile. No particle softening. `[2] <footnote-2_>`_
   * - .. dropdown:: ``dark_matter_mass``

          * **HDF5 name:** ``DarkMatterMass``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** :math:`10^{10}\ \rm{M}_\odot`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - basic
     - :avail:`BS` :avail:`ES` :avail:`IS` :avail:`EP` :avail:`SO`
     - Total DM mass.
   * - .. dropdown:: ``enclose_radius``

          * **HDF5 name:** ``EncloseRadius``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** :math:`a \cdot \rm{Mpc}`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - basic
     - :avail:`BS` :unavail:`ES` :unavail:`IS` :unavail:`EP` :unavail:`SO`
     - Radius of the particle furthest from the halo centre
   * - .. dropdown:: ``half_mass_radius_total``

          * **HDF5 name:** ``HalfMassRadiusTotal``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** :math:`a \cdot \rm{Mpc}`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - basic
     - :avail:`BS` :unavail:`ES` :unavail:`IS` :unavail:`EP` :unavail:`SO`
     - Total half mass radius. `[3] <footnote-3_>`_
   * - .. dropdown:: ``mass_fraction_external``

          * **HDF5 name:** ``MassFractionExternal``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** dimensionless
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - basic
     - :unavail:`BS` :unavail:`ES` :unavail:`IS` :unavail:`EP` :avail:`SO`
     - Fraction of mass that is bound to a satellite outside this FoF group. `[4] <footnote-4_>`_
   * - .. dropdown:: ``mass_fraction_satellites``

          * **HDF5 name:** ``MassFractionSatellites``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** dimensionless
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - basic
     - :unavail:`BS` :unavail:`ES` :unavail:`IS` :unavail:`EP` :avail:`SO`
     - Fraction of mass that is bound to a satellite in the same FoF group. `[4] <footnote-4_>`_
   * - .. dropdown:: ``maximum_circular_velocity``

          * **HDF5 name:** ``MaximumCircularVelocity``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** :math:`\rm{km} / \rm{s}`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - basic
     - :avail:`BS` :avail:`ES` :avail:`IS` :unavail:`EP` :avail:`SO`
     - Maximum circular velocity when accounting for particle softening lengths. `[5] <footnote-5_>`_
   * - .. dropdown:: ``maximum_circular_velocity_radius``

          * **HDF5 name:** ``MaximumCircularVelocityRadius``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** :math:`a \cdot \rm{Mpc}`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - basic
     - :unavail:`BS` :avail:`ES` :avail:`IS` :unavail:`EP` :avail:`SO`
     - Radius at which MaximumCircularVelocity is reached.
   * - .. dropdown:: ``maximum_circular_velocity_radius_unsoftened``

          * **HDF5 name:** ``MaximumCircularVelocityRadiusUnsoftened``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** :math:`a \cdot \rm{Mpc}`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - basic
     - :avail:`BS` :unavail:`ES` :unavail:`IS` :unavail:`EP` :unavail:`SO`
     - Radius at which MaximumCircularVelocityUnsoftened is reached. `[5] <footnote-5_>`_
   * - .. dropdown:: ``maximum_circular_velocity_unsoftened``

          * **HDF5 name:** ``MaximumCircularVelocityUnsoftened``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** :math:`\rm{km} / \rm{s}`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - basic
     - :avail:`BS` :unavail:`ES` :unavail:`IS` :unavail:`EP` :unavail:`SO`
     - Maximum circular velocity when not accounting for particle softening lengths. `[5] <footnote-5_>`_
   * - .. dropdown:: ``number_of_dark_matter_particles``

          * **HDF5 name:** ``NumberOfDarkMatterParticles``
          * **Shape:** 1
          * **Type:** uint32
          * **Units:** dimensionless
          * **Compression:** no compression
     - basic
     - :avail:`BS` :avail:`ES` :avail:`IS` :avail:`EP` :avail:`SO`
     - Number of dark matter particles.
   * - .. dropdown:: ``soradius``

          * **HDF5 name:** ``SORadius``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** :math:`a \cdot \rm{Mpc}`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - basic
     - :unavail:`BS` :unavail:`ES` :unavail:`IS` :unavail:`EP` :avail:`SO`
     - Radius of a sphere satisfying a spherical overdensity criterion.
   * - .. dropdown:: ``total_mass``

          * **HDF5 name:** ``TotalMass``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** :math:`10^{10}\ \rm{M}_\odot`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - basic
     - :avail:`BS` :avail:`ES` :avail:`IS` :avail:`EP` :avail:`SO`
     - Total mass.
   * - .. dropdown:: ``angular_momentum_dark_matter``

          * **HDF5 name:** ``AngularMomentumDarkMatter``
          * **Shape:** 3
          * **Type:** float32
          * **Units:** :math:`10^{10}\ \rm{Mpc} \cdot \rm{M}_\odot \cdot \rm{km} / \rm{s}`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - general
     - :avail:`BS` :avail:`ES` :avail:`IS` :unavail:`EP` :avail:`SO`
     - Total angular momentum of the dark matter, relative to the HaloCentre and DM centre of mass velocity. `[6] <footnote-6_>`_
   * - .. dropdown:: ``dark_matter_inertia_tensor_noniterative``

          * **HDF5 name:** ``DarkMatterInertiaTensorNoniterative``
          * **Shape:** 6
          * **Type:** float32
          * **Units:** :math:`\rm{Mpc}^{2}`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - general
     - :avail:`BS` :unavail:`ES` :unavail:`IS` :unavail:`EP` :avail:`SO`
     - 3D inertia tensor computed in a single interation from the DM mass distribution, relative to the halo centre. Diagonal components and one off-diagonal triangle as (1,1), (2,2), (3,3), (1,2), (1,3), (2,3). Only calculated when we have more than 20 particles.
   * - .. dropdown:: ``dark_matter_inertia_tensor_reduced_noniterative``

          * **HDF5 name:** ``DarkMatterInertiaTensorReducedNoniterative``
          * **Shape:** 6
          * **Type:** float32
          * **Units:** dimensionless
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - general
     - :avail:`BS` :unavail:`ES` :unavail:`IS` :unavail:`EP` :avail:`SO`
     - Reduced 3D inertia tensor computed in a single interation from the DM mass distribution, relative to the halo centre. Diagonal components and one off-diagonal triangle as (1,1), (2,2), (3,3), (1,2), (1,3), (2,3). Only calculated when we have more than 20 particles.
   * - .. dropdown:: ``dark_matter_mass_flow_rate``

          * **HDF5 name:** ``DarkMatterMassFlowRate``
          * **Shape:** 6
          * **Type:** float32
          * **Units:** :math:`10^{10}\ \frac{\rm{M}_\odot \cdot \rm{km}}{\rm{Mpc} \cdot \rm{s}}`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - general
     - :unavail:`BS` :unavail:`ES` :unavail:`IS` :unavail:`EP` :avail:`SO`
     - Mass flow rate of dark matter particles through spherical shells. Contains 6 entries: inflow rate at 0.1R, 0.3R, R, outflow rate at 0.1R, 0.3R, R. `[7] <footnote-7_>`_
   * - .. dropdown:: ``dark_matter_projected_velocity_dispersion``

          * **HDF5 name:** ``DarkMatterProjectedVelocityDispersion``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** :math:`\rm{km} / \rm{s}`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - general
     - :unavail:`BS` :unavail:`ES` :unavail:`IS` :avail:`EP` :unavail:`SO`
     - Mass-weighted velocity dispersion of the DM along the projection axis, relative to the DM centre of mass velocity. `[8] <footnote-8_>`_
   * - .. dropdown:: ``dark_matter_velocity_dispersion_matrix``

          * **HDF5 name:** ``DarkMatterVelocityDispersionMatrix``
          * **Shape:** 6
          * **Type:** float32
          * **Units:** :math:`\rm{km}^{2} / \rm{s}^{2}`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - general
     - :avail:`BS` :avail:`ES` :avail:`IS` :unavail:`EP` :unavail:`SO`
     - Mass-weighted velocity dispersion of the dark matter. Measured relative to the DM centre of mass velocity. The order of the components of the dispersion tensor is XX YY ZZ XY XZ YZ. `[9] <footnote-9_>`_
   * - .. dropdown:: ``half_mass_radius_dark_matter``

          * **HDF5 name:** ``HalfMassRadiusDarkMatter``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** :math:`a \cdot \rm{Mpc}`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - general
     - :avail:`BS` :avail:`ES` :avail:`IS` :avail:`EP` :unavail:`SO`
     - Dark matter half mass radius. `[3] <footnote-3_>`_
   * - .. dropdown:: ``spin_parameter``

          * **HDF5 name:** ``SpinParameter``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** dimensionless
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - general
     - :avail:`BS` :unavail:`ES` :unavail:`IS` :unavail:`EP` :avail:`SO`
     - Bullock et al. (2001) spin parameter. `[10] <footnote-10_>`_
   * - .. dropdown:: ``total_inertia_tensor_noniterative``

          * **HDF5 name:** ``TotalInertiaTensorNoniterative``
          * **Shape:** 6
          * **Type:** float32
          * **Units:** :math:`\rm{Mpc}^{2}`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - general
     - :avail:`BS` :unavail:`ES` :unavail:`IS` :unavail:`EP` :avail:`SO`
     - 3D inertia tensor computed in a single iteration from the total mass distribution, relative to the halo centre. Diagonal components and one off-diagonal triangle as (1,1), (2,2), (3,3), (1,2), (1,3), (2,3). Only calculated when we have more than 20 particles. `[11] <footnote-11_>`_
   * - .. dropdown:: ``total_inertia_tensor_reduced_noniterative``

          * **HDF5 name:** ``TotalInertiaTensorReducedNoniterative``
          * **Shape:** 6
          * **Type:** float32
          * **Units:** dimensionless
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - general
     - :avail:`BS` :unavail:`ES` :unavail:`IS` :unavail:`EP` :avail:`SO`
     - Reduced 3D inertia tensor computed in a single iteration from the total mass distribution, relative to the halo centre. Diagonal components and one off-diagonal triangle as (1,1), (2,2), (3,3), (1,2), (1,3), (2,3). Only calculated when we have more than 20 particles. `[11] <footnote-11_>`_

Copied properties
-----------------

.. list-table::
   :widths: 25 10 15 50
   :header-rows: 1

   * - Name
     - Filter
     - Variations
     - Description
   * - .. dropdown:: ``input_halos_hbtplus.depth``

          * **HDF5 name:** ``InputHalos/HBTplus/Depth``
          * **Shape:** 1
          * **Type:** uint64
          * **Units:** dimensionless
          * **Compression:** no compression
     - basic
     - \-
     - Level of the subhalo in the merging hierarchy.
   * - .. dropdown:: ``input_halos_hbtplus.host_fofid``

          * **HDF5 name:** ``InputHalos/HBTplus/HostFOFId``
          * **Shape:** 1
          * **Type:** int64
          * **Units:** dimensionless
          * **Compression:** no compression
     - basic
     - \-
     - ID of the host FoF halo of this subhalo. Hostless halos have HostFOFId == -1
   * - .. dropdown:: ``input_halos_hbtplus.last_max_mass``

          * **HDF5 name:** ``InputHalos/HBTplus/LastMaxMass``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** :math:`10^{10}\ \rm{M}_\odot`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - basic
     - \-
     - Maximum mass of this subhalo across its evolutionary history
   * - .. dropdown:: ``input_halos_hbtplus.last_max_vmax_physical``

          * **HDF5 name:** ``InputHalos/HBTplus/LastMaxVmaxPhysical``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** :math:`\rm{km} / \rm{s}`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - basic
     - \-
     - Largest value of maximum circular velocity of this subhalo across its evolutionary history
   * - .. dropdown:: ``input_halos_hbtplus.nested_parent_track_id``

          * **HDF5 name:** ``InputHalos/HBTplus/NestedParentTrackId``
          * **Shape:** 1
          * **Type:** int64
          * **Units:** dimensionless
          * **Compression:** no compression
     - basic
     - \-
     - TrackId of the parent of this subhalo.
   * - .. dropdown:: ``input_halos_hbtplus.snapshot_of_birth``

          * **HDF5 name:** ``InputHalos/HBTplus/SnapshotOfBirth``
          * **Shape:** 1
          * **Type:** int64
          * **Units:** dimensionless
          * **Compression:** no compression
     - basic
     - \-
     - Snapshot when this subhalo was formed.
   * - .. dropdown:: ``input_halos_hbtplus.snapshot_of_last_isolation``

          * **HDF5 name:** ``InputHalos/HBTplus/SnapshotOfLastIsolation``
          * **Shape:** 1
          * **Type:** int64
          * **Units:** dimensionless
          * **Compression:** no compression
     - basic
     - \-
     - Latest snapshot when this subhalo was a central. -1 if the subhalo has always been a central. For a subhalo which is currently a central but was a satellite in the past it will be equal to the current snapshot. See :ref:`issues_overflow_snapshotindexoflastisolation`
   * - .. dropdown:: ``input_halos_hbtplus.snapshot_of_last_max_mass``

          * **HDF5 name:** ``InputHalos/HBTplus/SnapshotOfLastMaxMass``
          * **Shape:** 1
          * **Type:** int64
          * **Units:** dimensionless
          * **Compression:** no compression
     - basic
     - \-
     - Latest snapshot when this subhalo had its maximum mass.
   * - .. dropdown:: ``input_halos_hbtplus.snapshot_of_last_max_vmax``

          * **HDF5 name:** ``InputHalos/HBTplus/SnapshotOfLastMaxVmax``
          * **Shape:** 1
          * **Type:** int64
          * **Units:** dimensionless
          * **Compression:** no compression
     - basic
     - \-
     - Latest snapshot when this subhalo had its largest maximum circular velocity.
   * - .. dropdown:: ``input_halos_hbtplus.track_id``

          * **HDF5 name:** ``InputHalos/HBTplus/TrackId``
          * **Shape:** 1
          * **Type:** uint64
          * **Units:** dimensionless
          * **Compression:** no compression
     - basic
     - \-
     - Unique ID for this subhalo which is consistent across snapshots.
   * - .. dropdown:: ``input_halos_fof.centres``

          * **HDF5 name:** ``InputHalos/FOF/Centres``
          * **Shape:** 3
          * **Type:** float64
          * **Units:** :math:`a \cdot \rm{Mpc}`
          * **Compression:** 1 pc accurate
     - basic
     - \-
     - Centre of mass of the host FoF halo of this subhalo. Zero for satellite and hostless subhalos.
   * - .. dropdown:: ``input_halos_fof.masses``

          * **HDF5 name:** ``InputHalos/FOF/Masses``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** :math:`10^{10}\ \rm{M}_\odot`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - basic
     - \-
     - Mass of the host FoF halo of this subhalo. Zero for satellite and hostless subhalos.
   * - .. dropdown:: ``input_halos_fof.radii``

          * **HDF5 name:** ``InputHalos/FOF/Radii``
          * **Shape:** 1
          * **Type:** float32
          * **Units:** :math:`a \cdot \rm{Mpc}`
          * **Compression:** :math:`1.36693{\rm{}e}10 \rightarrow{} 1.367{\rm{}e}10`
     - basic
     - \-
     - Radius of the particle furthest from the FoF centre of mass. Zero for satellite and hostless subhalos. Missing for older runs.
   * - .. dropdown:: ``input_halos_fof.sizes``

          * **HDF5 name:** ``InputHalos/FOF/Sizes``
          * **Shape:** 1
          * **Type:** uint64
          * **Units:** dimensionless
          * **Compression:** no compression
     - basic
     - \-
     - Number of particles in the host FoF halo of this subhalo. Zero for satellite and hostless subhalos.
   * - .. dropdown:: ``soap.descendant_index``

          * **HDF5 name:** ``SOAP/DescendantIndex``
          * **Shape:** 1
          * **Type:** int32
          * **Units:** dimensionless
          * **Compression:** no compression
     - basic
     - \-
     - Index (within the next snapshot SOAP arrays) of the main descendant of this subhalo. `[12] <footnote-12_>`_
   * - .. dropdown:: ``soap.host_halo_index``

          * **HDF5 name:** ``SOAP/HostHaloIndex``
          * **Shape:** 1
          * **Type:** int64
          * **Units:** dimensionless
          * **Compression:** no compression
     - basic
     - \-
     - Index (within the SOAP arrays) of the top level parent of this subhalo. -1 for hostless halos.
   * - .. dropdown:: ``soap.included_in_reduced_snapshot``

          * **HDF5 name:** ``SOAP/IncludedInReducedSnapshot``
          * **Shape:** 1
          * **Type:** int32
          * **Units:** dimensionless
          * **Compression:** no compression
     - basic
     - \-
     - Whether this halo is included in the reduced snapshot.
   * - .. dropdown:: ``soap.progenitor_index``

          * **HDF5 name:** ``SOAP/ProgenitorIndex``
          * **Shape:** 1
          * **Type:** int32
          * **Units:** dimensionless
          * **Compression:** no compression
     - basic
     - \-
     - Index (within the previous snapshot SOAP arrays) of the main progenitor of this subhalo. `[12] <footnote-12_>`_
   * - .. dropdown:: ``soap.subhalo_rank_by_bound_mass``

          * **HDF5 name:** ``SOAP/SubhaloRankByBoundMass``
          * **Shape:** 1
          * **Type:** int32
          * **Units:** dimensionless
          * **Compression:** no compression
     - basic
     - \-
     - Ranking by mass of the halo within its parent field halo. Zero for the most massive halo in the field halo.

Footnotes
---------

.. _footnote-1:

**[1]** **The centre of mass and centre of mass velocity** are computed using all
particle types except neutrinos.

.. _footnote-2:

**[2]** **The concentration** is computed using the
method described in `Wang et al. (2024) <https://ui.adsabs.harvard.edu/abs/2024MNRAS.52710760W>`_, but using a fifth order polynomial fit to
the R1-concentration relation for :math:`1<c<1000`. Therefore, we set a floor of 1 and
a ceiling of 1000 for the values calculated by SOAP. This method assumes halos have
an NFW profile, and is only calculated for the
following SO variations: 200 crit, 200 mean, and BN98.
Neutrinos are included in the calculation of total concentration.
The first moment of the density distribution, :math:`R1`, can be estimated from
the concentration. From :math:`R1` the Einasto concentration can be calculated. It
also possible to estimate other properties, such as :math:`v_{max}`, by using the :math:`R1`
value and assuming an NFW profile.

.. _footnote-3:

**[3]** **The half mass radius** is determined by linear interpolation of the
cumulative mass profile obtained after sorting all particles by radius. For the projected apertures, SOAP 
uses the 2D radius (distance to the projection axis) instead of the 3D radius.

.. _footnote-4:

**[4]** **The satellite mass fractions** is obtained by summing the masses of all
particles within the inclusive sphere that are bound to a subhalo that is not the central subhalo, and 
dividing this by :math:`M_{SO}`. This uses the same membership information as is used to decide what 
particles need to be included in the exclusive sphere and projected aperture properties. For MassFractionSatellites
we only consider particles with the same FoF ID as the most bound particle in the central subhalo. For
MassFractionExternal we include all particles with a FoF ID not equal to the most bound particle in the central subhalo.

.. _footnote-5:

**[5]** **The maximum circular velocity and the radius where it is reached** are
computed using

.. math::

   v_{\rm{}max} = \sqrt{\frac{G M(\leq{}r)}{r}},

where the cumulative mass :math:`M(r)` includes all particles within the radius :math:`r`, and includes the
contribution of the particle(s) at :math:`r=0`. The radius is computed relative to the halo centre.
The softened :math:`v_{max}` value is calculated using the same method, except that the particle
radius has a floor equal to the softening length. An alternative way to calculate :math:`v_{max}`
is to estimate it from the halo concentration by assuming an NFW profile. We store the radius of the
unsoftened maximum circular velocity. If the softened and unsoftened maximum circular velocities are
equal, then their radii will also be equal. If the values are not equal, then the radius of the
softened maximum circular velocity will be the simulation softening length.
Note that the softened vmax is :math:`*not*` the :math:`v_{max}` computed using a softened potential.

.. _footnote-6:

**[6]** **The angular momentum** of gas, dark matter, or stars is computed relative to
the halo centre and the centre of mass velocity of that particular component, and not to the 
total centre of mass velocity. The full expression is

.. math::

   \vec{L}_{\rm{}comp} = \sum_{i={\rm{}comp}} m_i \left(\vec{x}_{r,i} \times{} \vec{v}_{{\rm{}comp},r,i} \right),

with the sum :math:`i` over all particles of that particular component (bound to the halo), and

.. math::

   \vec{x}_{r,i} = \vec{x}_i - \vec{x}_{\rm{}cop},

.. math::

   \vec{v}_{{\rm{}comp},r,i} = \vec{v}_i - \vec{v}_{\rm{}com,comp},

where

.. math::

   \vec{v}_{\rm{}com,comp} = \frac{\sum_{i={\rm{}comp}} m_i \vec{v}_i}{\sum_{i={\rm{}comp}} m_i}.

We also compute the angular momentum for baryons, where the sum is then over both gas and star 
particles.

.. _footnote-7:

**[7]** **The flow rates** are computed for three spherical
shells: :math:`R` = :math:`f R_{SO}` with :math:`f = 0.1, 0.3, 1`. In all cases the width of the
spherical shell is given by :math:`dR = 0.1 R`.

For each particle :math:`i` within the shell we calculate their radial velocity as

.. math::

   v_{r,i} = (\underline{v_i} - \underline{v_{COM}}) \cdot \underline{\hat{r}} - \dot{R}

where :math:`v_i` is the velocity of the particle, :math:`v_{COM}` is the centre of mass velocity of all particles within :math:`R` (therefore we use a different value for each spherical shell). The final term accounts for the "pseudo-evolution" of the halo radius and is given by

.. math::

   \dot{R} = f \frac{2}{3} \left(\frac{GHM_{SO}}{100}\right)^\frac{1}{3} \left( 2 \Omega_\gamma + \frac{3}{2} \Omega_m \right)

This is required since accretion rates are often measured by subtracting the halo mass between consecutive snapshots and dividing by the time interval.
To be consistent with this method we must consider that the virial radius is defined w.r.t background density (which decreases in time). Hence, the virial radius actually moves
outward with a velocity that we can compute analytically. This means that static
particles at the virial radius actually become inflowing. The expression is derived by taking the partial differential of the analytic expression for :math:`R_{200}` w.r.t. time.
Note that :math:`v_{r,i}` does not include the Hubble flow relative to the halo centre.

To calculate the mass inflow (outflow) rate
we compute the following sum over particles within the spherical shell which satisfy
:math:`v_{r,i} < 0` (:math:`v_{r,i} > 0`),

.. math::

   \frac{1}{dR} \sum_{i} m_i v_{r, i},

where :math:`m_i` is the mass of particle :math:`i`. For energy flow rates the sum is

.. math::

   \frac{1}{dR} \sum_{i} m_i v_{r, i} \left(\frac{v_i^2}{2} + u_i\right),

where :math:`u_i` is the internal energy per unit mass and :math:`v_i` is the total 3D velocity·
relative to the center of mass velocity. For momentum flow rates the sum is

.. math::

   \frac{1}{dR} \sum_{i} m_i \left(v_{r,i}^2 + \frac{c_s^2}{\gamma}\right),

where :math:`c_s` is the sound speed and :math:`` = 5/3 (the second term accounts for pressure). For the gas phases we also calculate "fast outflow" rates. These are calculated by using the equations above, but only for particles that satisfy :math:`v_{r,i} > V_{max} / 4`, where :math:`V_{max}` is the maximum circular velocity of the halo. The flow rates are always positive, so to compute the net rate you must subtract the inflow rate from the outflow rate. Flow rates are only calculated for the
following SO definitions: :math:`200_{c}`, :math:`200_{m}`, :math:`BN98`. To calculate the total gas flow rate the individual phases should be summed together.

.. _footnote-8:

**[8]** **The projected velocity dispersion** is computed along the projection axis.
Along this axis the velocity is a 1D quantity, so the velocity dispersion is simply a scalar.

.. _footnote-9:

**[9]** **The velocity dispersion matrix** is defined as

.. math::

   V_{\rm{}disp,comp} = \frac{1}{\sum_{i={\rm{}comp}} m_i} \sum_{i={\rm{}comp}} m_i \vec{v}_{{\rm{}comp},r,i}\vec{v}_{{\rm{}comp},r,i},

where we compute the relative velocity as before, i.e. w.r.t. the centre of mass velocity of the particular 
component of interest. While it is strictly speaking a :math:`3 \times 3` matrix, there are only 6 independent 
components. We use the following convention to output those 6 components as a 6-element array:

.. math::

   V'_{\rm{}disp} = \begin{pmatrix}
       V_{xx} & V_{yy} & V_{zz} & V_{xy} & V_{xz} & V_{yz}
       \end{pmatrix}.

Other velocity dispersion definitions can be derived from this general form. The one-dimensional velocity dispersion can be calculated as

.. math::

   \sigma = \sqrt{\frac{V_{xx} + V_{yy} + V_{zz}}{3}}

.. _footnote-10:

**[10]** **The spin parameter** is computed following `Bullock et al. (2001) <https://ui.adsabs.harvard.edu/abs/2001ApJ...555..240B>`_:

.. math::

   \lambda{} = \frac{|\vec{L}_{\rm{}tot}|}{\sqrt{2}M v_{\rm{}max} R},

where :math:`L_{tot}` is the total angular momentum of all particles within radius :math:`R`, and :math:`M` their 
total mass. The angular momentum is computed relative to the halo centre and the total centre of mass 
velocity. Since subhalos do not have a natural radius associated with them, we use the radius where the softened
:math:`v_{max}` is reached.

.. _footnote-11:

**[11]** **The inertia tensor** for a set of particles is computed as

.. math::

   I_{ij} = \frac{1}{\sum_k m_k} \sum_k m_k \; r_{k,i} \; r_{k, j}

where the index :math:`k` loops over all particles, :math:`m_k` is the mass of particle :math:`k`, and :math:`r_{k, i}` is the :math:`i`-component of the position vector of particle :math:`k` relative to the halo centre. We first compute the inertia tensor using all particles within a sphere (with radius equal to the aperture size, except for subhalos where we use the half mass radius of the particles). This is the tensor we output in the non-iterative case. In the iterative case we construct an ellipsoid with a volume equal to the initial sphere, but whose shape is given by the inertia tensor. We then recalculate the inertia tensor using only the particles within the ellipsoid. This process is repeated until the value of the :math:`q` parameter converges, or we reach 20 iterations. If at any point during the iterations there is only a single particle within the ellipsoid, we return zero. For projected apertures the process is similar, except we use circles and ellipses in the projected plane to determine which particles to include.

The reduced inertia tensor is calculated as

.. math::

   I_{ij} = \frac{1}{\sum_k m_k} \sum_k m_k \; r_{k,i} \; r_{k, j} \; r_{k}^{-2}

where :math:`r_k` is the radial distance of the particle.

We do not calculate the inertia tensor if there are fewer than 20 particles within the initial sphere.

When calculating the inertia tensor for a bound subhalo we use a sphere with a radius equal to 10 times the half mass radius of the particles being considered.

.. _footnote-12:
.. _footnote-30:

**[12]** **The progenitor/descendant index** of a subhalo points to the subhalo in the previous/next snapshot that has the same HBT TrackId. This index can therefore only be used to move up/down the main progenitor branch for a subhalo, it provides no information about subhalo mergers.
