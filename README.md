# Documentation for the COLIBRE dark matter only simulations

This repository contains sphinx documentation for the public release of the
COLIBRE dark matter only (DMO) simulations. The documentation for the full
simulation suite, including the hydrodynamical runs, lives in a separate
repository.

## Building

To build the html documentation:
```
pip install sphinx piccolo_theme sphinx_design sphinxcontrib_mermaid
make html
```

`./build.sh` cleans and rebuilds the site.

