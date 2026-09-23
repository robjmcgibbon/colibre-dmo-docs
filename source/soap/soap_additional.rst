Additional SOAP catalogues
==========================

This page lists additional halo catalogues produced with SOAP.
These products are intended to supplement analyses and have only been
generated for a limited selection of snapshots and simulations.

SubFind SOAP catalogues
-----------------------

To facilitate comparisons with previous work, we have run SubFind
(the GADGET-4 public version) for several simulations.
Note that due to fundamental differences in how halo finders operate,
any discrepancies between HBT and SubFind catalogues should not be
interpreted as an indication of "error" in the halo finding process.

SubFind has been run for :math:`z=0` for the following simulations:

* L050m5
* L100m6
* L200m7

We have also produced SOAP catalogues using these SubFind catalogues as input.
The runs listed above include a ``SOAP-Subfind`` directory containing the
:math:`z=0` catalogue.
Additionally, the ``colibre_with_SOAP_membership_0127.hdf5`` file is provided,
enabling the use of ``swiftgalaxy`` with these catalogues.
