SOAP
====

If you need to compute properties for all subhalos in a simulation,
it can be useful to use `SOAP <https://github.com/SWIFTSIM/SOAP>`__.
The standard SOAP catalogues include a large number of precomputed properties,
but SOAP can also be configured to compute only a selected subset,
which significantly reduces runtime.
Below is a minimal parameter file required to run SOAP.

.. note:: Unlike the other examples, SOAP reads the snapshot and halo finder
          output directly rather than through the data service, so you need to
          :doc:`download </service_docs/index>` the files for the snapshots you
          want to process and set ``sim_dir`` to where you put them.


Further details on running SOAP are available
`in the repository documentation <https://github.com/SWIFTSIM/SOAP#computing-halo-properties>`__.
Note that there is no need to regenerate membership files,
the existing ones can be reused.
The repository also includes
`guidance on adding new properties <https://github.com/SWIFTSIM/SOAP?tab=readme-ov-file#modifying-the-code>`__.

.. code-block:: yaml

   # Values in this section are substituted into the other sections
   Parameters:
     sim_dir: /path/to/downloaded/colibre/data
     output_dir: /path/to/soap_example
     scratch_dir: /path/to/scratch/soap_example

   # Location of the Swift snapshots:
   Snapshots:
     # Use {snap_nr:04d} for the snapshot number and {file_nr} for the file number.
     filename: "{sim_dir}/{sim_name}/snapshots/colibre_{snap_nr:04d}/colibre_{snap_nr:04d}.{file_nr}.hdf5"

   # Which halo finder we're using, and base name for halo finder output files
   HaloFinder:
     type: HBTplus
     filename: "{sim_dir}/{sim_name}/HBT-HERONS/sorted_catalogues/OrderedSubSnap_{snap_nr:03d}.hdf5"

   GroupMembership:
     # Where to write the group membership files
     filename: "{sim_dir}/{sim_name}/SOAP/membership_{snap_nr:04d}/membership_{snap_nr:04d}.{file_nr}.hdf5"

   HaloProperties:
     # Where to write the halo properties file
     filename: "{output_dir}/{sim_name}/SOAP_uncompressed/halo_properties_{snap_nr:04d}.hdf5"
     # Where to write temporary chunk output
     chunk_dir: "{scratch_dir}/{sim_name}/SOAP-tmp/"

   SOProperties:
     properties:
       CentreOfMass: true
       CentreOfMassVelocity: true
       Concentration: true
       ConcentrationUnsoftened: true
       MassFractionSatellites: true
       MassFractionExternal: true
       MaximumCircularVelocity: true
       MaximumCircularVelocityRadius: true
       NumberOfDarkMatterParticles: true
       SORadius: true
       SpinParameter: true
       TotalMass: true
   variations:
     200_crit:
       type: crit
       value: 200.0
     500_crit:
       type: crit
       value: 500.0

   SubhaloProperties:
     properties:
       EncloseRadius: true
       NumberOfDarkMatterParticles: true
       TotalMass: true

   filters:
     general:
       limit: 100
       properties:
         - BoundSubhalo/NumberOfDarkMatterParticles
       combine_properties: sum
   calculations:
     calculate_missing_properties: false
     strict_halo_copy: false
