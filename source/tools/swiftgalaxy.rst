SWIFTGalaxy
===========

The `swiftgalaxy <https://swiftgalaxy.readthedocs.io/en/stable/index.html>`__
python module can be used to analyse particles belonging to individual subhalos.
It is build on top of :doc:`swiftsimio <swiftsimio>` and inherits all of its features,
while adding features designed for working with individual galaxies.

Full documentation of ``SWIFTGalaxy`` can
`be found here <https://swiftgalaxy.readthedocs.io/en/stable/index.html>`__.

Installation
------------

The swiftgalaxy module can be installed as follows::

  pip install swiftgalaxy

Creating a SWIFTGalaxy
----------------------

A ``SWIFTGalaxy`` needs two things: the path to the virtual snapshot
file (the same file used with swiftsimio, which must contain the HBT-Herons
membership information) and an initialised halo finder object. For
COLIBRE outputs we use the ``SOAP`` halo catalogue class. The
``soap_index`` identifies the row in the SOAP catalogue corresponding
to the subhalo of interest.

.. code-block:: python

   from swiftgalaxy import SWIFTGalaxy, SOAP

   # Files are read from the data service without downloading them. See the
   # swiftsimio page for how to open files you have downloaded instead.
   import hdfstream
   root_dir = hdfstream.open("cosma", "/")

   run = "COLIBRE/L025_m5/DMO"
   snap_nr = 127

   virtual_snapshot_file = root_dir[f"{run}/SOAP-HBT/colibre_with_SOAP_membership_{snap_nr:04}.hdf5"]
   soap_catalogue_file   = root_dir[f"{run}/SOAP-HBT/halo_properties_{snap_nr:04}.hdf5"]

   sg = SWIFTGalaxy(
       virtual_snapshot_file,
       SOAP(
           soap_catalogue_file,
           soap_index=42,
       ),
   )

We can load a SOAP catalogue with swiftsimio to pick a target. Here for example a
halo with :math:`M_{200c} \approx 10^{11}\,\mathrm{M}_\odot`

.. code-block:: python

    import numpy as np
    import unyt as u
    from swiftsimio import load, cosmo_quantity

    soap = load(soap_catalogue_file)
    m200c = soap.spherical_overdensity_200_crit.total_mass
    candidates = np.argwhere(
        np.logical_and(
            m200c > cosmo_quantity(
                1e11,
                u.solMass,
                comoving=True,
                scale_factor=soap.metadata.scale_factor,
                scale_exponent=0,
            ),
            m200c < cosmo_quantity(
                2e11,
                u.solMass,
                comoving=True,
                scale_factor=soap.metadata.scale_factor,
                scale_exponent=0,
            ),
        )
    ).squeeze()

    sg = SWIFTGalaxy(
        virtual_snapshot_file,
        SOAP(soap_catalogue_file, soap_index=candidates[0]),
    )

Accessing particle data
-----------------------

Because ``SWIFTGalaxy`` inherits from ``SWIFTDataset``, particle data
are accessed in exactly the same way as in swiftsimio, with lazy
loading and unit-aware ``cosmo_array`` results. See
:doc:`swiftsimio <swiftsimio>` for a full description of how to work
with these arrays. The key difference is that the coordinates are
automatically recentred on the subhalo of interest at construction
time, so all coordinates are in the subhalo's rest frame. If we print
the median we can see the value is close to zero as expected::

  >>> print(np.median(sg.dark_matter.coordinates, axis=0)
  [-0.00043459 -0.00018946  0.00061128] Mpc (Comoving)

SOAP integrated properties are also available through the
``halo_catalogue`` attribute. Only the properties of the selected
subhalo are loaded::

  m200c = sg.halo_catalogue.spherical_overdensity_200_crit.total_mass.to(u.solMass)

``SWIFTGalaxy`` also provides spherical and cylindrical coordinates and 
velocities as a convenience (they are lazily calculated/re-calculated as needed),
for example the :math:`z`-component of the dark matter specific angular momentum
becomes very easy to calculate::

  jz_dm = np.sum(sg.dark_matter.spherical_coordinates.r * sg.dark_matter.spherical_velocities.phi)

Coordinate transformations
--------------------------
 
All particle types in a ``SWIFTGalaxy`` share a common coordinate
frame and always transform together. Rotations, translations and
velocity boosts are all supported. Rotations are specified using the
`scipy Rotation class
<https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.transform.Rotation.html>`__,
which accepts rotation matrices, Euler angles, and more.
 
A common use case is to align the halo using the angular
momentum vector pre-computed by SOAP:
 
.. code-block:: python
 
   import numpy as np
   from scipy.spatial.transform import Rotation
 
   Ldm = sg.halo_catalogue.bound_subhalo.angular_momentum_dark_matter.squeeze()
   rot, _ = Rotation.align_vectors([0, 0, 1], Ldm / np.linalg.norm(Ldm))
   sg.rotate(rot)
 
After the rotation every particle type is automatically in the new
frame, and subsequently loaded properties will also be in that frame.

