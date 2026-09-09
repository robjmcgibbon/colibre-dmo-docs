Snapshots
=========

Each COLIBRE simulation models the evolution of a cubic volume of the
Universe from just after the big bang to the present day. The state of
the simulation is output at intervals as a series of "snapshots",
which record the distribution of particles in the simulated volume at
an instant in time.

In the dark matter only simulations only CDM particles are present, but the
CDM particles account for the mass in baryons, which are assumed to trace
the distribution of the CDM. Many physical properties, such as position,
mass and velocity, are stored for each particle.

.. card-carousel:: 3

    .. card:: L025m5 DM density at z=0

        .. image:: images/DM_density_L025m5_0.jpg

    .. card:: L200m6 DM density at z=0

        .. image:: images/DM_density_L200m6_0.jpg

    .. card:: L400m7 DM density at z=0

        .. image:: images/DM_density_L400m7_0.jpg

The following sections describe the layout and contents of the snapshots.

.. toctree::
   :maxdepth: 2

   Directory layout <snapshot_dirs>
   File format <snapshot_format>
   Output redshifts <snapshot_redshifts>
   snapshot_particle_properties

For more information about the SWIFT simulation snapshot format used
here, see the `SWIFT documentation
<https://swift.strw.leidenuniv.nl/docs/Snapshots/index.html>`__.
