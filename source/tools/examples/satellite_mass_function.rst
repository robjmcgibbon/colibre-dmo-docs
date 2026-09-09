:orphan:

Satellite bound mass function
=============================

Example code for selecting the satellites of a halo and plotting
their bound mass function.
The most massive halo in the box (by :math:`M_{200c}`) is identified,
and then all satellite subhalos
are selected using the ``is_central`` flag and ``host_halo_index``.

.. code-block:: python

    import matplotlib.pyplot as plt
    import numpy as np
    import swiftsimio as sw

    # ---------------------------------------------------------
    # Load the SOAP catalogue using swiftsimio
    # ---------------------------------------------------------
    # Files are read from the data service without downloading them. See the
    # swiftsimio page for how to open files you have downloaded instead.
    import hdfstream
    root_dir = hdfstream.open("cosma", "/")

    run = "COLIBRE/L100_m6/DMO"
    snap_nr = 127  # z=0
    soap = sw.load(root_dir[f"{run}/SOAP-HBT/halo_properties_{snap_nr:04}.hdf5"])

    # ---------------------------------------------------------
    # Find the most massive halo by M200c
    # ---------------------------------------------------------
    # Spherical overdensity properties are only computed for central subhalos,
    # so the maximum M200c identifies a central.
    halo_M200c = soap.spherical_overdensity_200_crit.total_mass.to_physical_value("Msun")
    central_idx = np.argmax(halo_M200c)

    track_id = soap.input_halos_hbtplus.track_id[central_idx].value
    print(f"Most massive halo: M200c = {halo_M200c[central_idx]:.2e} Msun, TrackId = {track_id}")

    # ---------------------------------------------------------
    # Select satellites of this halo
    # ---------------------------------------------------------
    # soap.soap.host_halo_index gives the SOAP catalogue index of each subhalo's
    # host central. For a central this points to itself; for a satellite it points
    # to the central of its FOF group.
    is_sat = soap.input_halos.is_central[:].value == 0
    in_host = soap.soap.host_halo_index[:].value == central_idx
    sat_mask = is_sat & in_host

    print(f"Number of satellites: {np.sum(sat_mask)}")

    # ---------------------------------------------------------
    # Get the bound mass of each satellite
    # ---------------------------------------------------------
    # bound_subhalo contains the properties of all the particles bound to a
    # subhalo, so total_mass here is the total bound mass of the satellite.
    sat_bound_mass = soap.bound_subhalo.total_mass[sat_mask].to_physical_value("Msun")

    # ---------------------------------------------------------
    # Plot the bound mass function
    # ---------------------------------------------------------
    bins = np.arange(8.0, 14.0, 0.5)

    fig, ax = plt.subplots(1)

    ax.stairs(
        np.histogram(np.log10(sat_bound_mass), bins=bins)[0],
        bins,
        fill=False,
    )

    ax.set_xlabel(r"$\log_{10}(M_{\mathrm{bound}} \, / \, \mathrm{M}_\odot)$")
    ax.set_ylabel("Number of satellites")
    ax.set_yscale("log")
    ax.set_title(f"Satellite bound mass function (TrackId = {track_id})")

    plt.savefig("satellite_bound_mass_function.png", dpi=200)
    plt.close()
