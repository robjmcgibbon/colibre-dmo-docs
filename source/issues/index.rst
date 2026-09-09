Known issues
============

This page tracks known technical issues related to the data products.
It will be updated as new issues are discovered.

Simulation
----------

Run restarted from snapshot
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The L200m6 DMO run experienced a disc failure at (:math:`z \approx 0.22`) and was
restarted from the most recent snapshot. This restart introduced minor
discontinuities in the time integration of some particle trajectories.
To quantify the effect of the restart, the L100m6 DMO run was restarted from the same
snapshot and compared with the uninterrupted run, with negligible differences
found between the two.

SOAP
----

Missing descendant track id
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The SOAP catalogues contain the property ``soap.descendant_index`` which gives
the index for the descendant of each subhalo. For some SOAP catalogues these
values are missing. These will be added in the future.

Incorrect Hubble parameter for flow rate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The :math:`z=0` value of the Hubble parameter was used when computing
:ref:`the flow rates <footnote-7>` for all redshifts.

.. _issues_overflow_snapshotindexoflastisolation:

Overflow in SnapshotIndexOfLastIsolation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The field ``soap.input_halos_hbtplus.snapshot_of_last_isolation`` gives the
latest snapshot when this subhalo was a central. It should be -1 if the subhalo
has always been a central. However, the array was set to have an unsigned integer
datatype, meaning that it could only contain positive values. When the value
should have been -1 it wrapped around and was set as 18446744073709551615 instead
(:math:`2^{64} - 1`, the maximum possible value for unsigned int64).
