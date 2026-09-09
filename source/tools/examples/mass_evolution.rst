:orphan:

Mass evolution of a subhalo
===========================

Example code for tracking the mass evolution of a halo across snapshots.
The most massive halo at :math:`z=0` (by :math:`M_{200c}`) is identified via its
``TrackId``, which remains consistent across all snapshots, allowing the halo
to be located in each earlier catalogue.
Note that if you need to do this for many objects, reading the raw
`HBT-HERONS <../../soap/hbt_merger_trees.html>`__ output files directly may
be more efficient, as those files are sorted by ``TrackId``.

.. code-block:: python

    import matplotlib.pyplot as plt
    import numpy as np
    import swiftsimio as sw

    # ---------------------------------------------------------
    # Find the most massive halo at z=0 and get its TrackId
    # ---------------------------------------------------------
    # Files are read from the data service without downloading them. See the
    # swiftsimio page for how to open files you have downloaded instead.
    import hdfstream
    root_dir = hdfstream.open("cosma", "/")

    run = "COLIBRE/L100_m6/DMO"
    snap_nr = 127  # z=0
    soap = sw.load(root_dir[f"{run}/SOAP-HBT/halo_properties_{snap_nr:04}.hdf5"])

    halo_M200c = soap.spherical_overdensity_200_crit.total_mass.to_physical_value("Msun")
    central_idx = np.argmax(halo_M200c)
    track_id = soap.input_halos_hbtplus.track_id[central_idx].value

    print(f"Tracking halo with TrackId={track_id}, M200c={halo_M200c[central_idx]:.2e} Msun")

    # ---------------------------------------------------------
    # Loop over snapshots and record masses
    # ---------------------------------------------------------
    # The dark matter mass is taken within R200c, and compared with the total
    # mass bound to the subhalo.
    # TrackIds may be absent from early snapshots if the halo had
    # fewer than 20 bound particles, so we skip any missing entries.
    snap_nrs = np.arange(22, 128, 5)
    scale_factors = []
    dm_masses = []
    bound_masses = []

    for i, snap_nr in enumerate(snap_nrs):
        print(f"Loading snapshot {snap_nr} ({i + 1}/{len(snap_nrs)})")
        soap = sw.load(root_dir[f"{run}/SOAP-HBT/halo_properties_{snap_nr:04}.hdf5"])

        matches = np.where(soap.input_halos_hbtplus.track_id[:].value == track_id)[0]
        if len(matches) == 0:
            print(f"  TrackId={track_id} not found, skipping")
            continue
        idx = matches[0]

        scale_factors.append(soap.metadata.a)
        dm_masses.append(soap.spherical_overdensity_200_crit.dark_matter_mass[idx].to_physical_value("Msun"))
        bound_masses.append(soap.bound_subhalo.total_mass[idx].to_physical_value("Msun"))

    scale_factors = np.array(scale_factors)
    dm_masses = np.array(dm_masses)
    bound_masses = np.array(bound_masses)

    # ---------------------------------------------------------
    # Plot
    # ---------------------------------------------------------
    fig, ax = plt.subplots(1)

    ax.plot(scale_factors, dm_masses, label="Dark matter ($R_{200c}$)", color="k")
    ax.plot(scale_factors, bound_masses, label="Bound mass", color="tab:blue")

    ax.set_xscale("log")
    ax.set_yscale("log")
    ax.set_xlabel("Scale factor")
    ax.set_ylabel(r"Mass [$M_\odot$]")
    ax.set_title(f"Mass evolution (TrackId = {track_id})")
    ax.legend()

    plt.savefig("mass_evolution.png", dpi=200)
    plt.close()
