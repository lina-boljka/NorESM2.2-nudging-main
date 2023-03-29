AMIP configuration
=============================================

.. warning::
  * Again, care must be taken when using the results of this model version (pre-release). 
  * Only a limited number of compsets is presently working. Here, we show how to run a historical AMIP experiment on Betzy/Sigma2.

---------------------

To create an experiment ``case`` follow instructions on `NorESM webpage <https://noresm-docs.readthedocs.io/en/latest/configurations/amips.html>`_ or, more specifically, for AMIP experiments follow instructions `here <https://noresm-docs.readthedocs.io/en/latest/configurations/amips.html>`_. Below we show an example for only one specific compset, which has historical prescribed sea-surface-temperatures (SSTs) and historical forcing, typically 1979-2014 (or longer).

1) First enter the NorESM2.2 directory with scripts: 
  ``~/<noresm-base>/cime/scripts/`` 

2) Then run command to create a new case, e.g., <case-name>:
  ``./create_newcase --case ~/<noresm-base>/cases/<case-name> --mach betzy --res f09_f09_mg17 --compset NFHISTfsstfrc2 --project <project-name>``

Here, we specify machine as "betzy", a historical AMIP compset with frc2 forcing (generally recommended for NorESM), and the model will run with project resources <project-name>, typically of form "nn1234k" or similar. Note that different AMIP compsets can be found here: ``<noresm-base>/components/cam/cime_config/config_compsets.xml``. 

3) List all available branches for checkout:
  ``git branch --all``
  
.. admonition:: user_nl_cam

  &chem_surfvals_nl
  
    ch4vmr         = -1.0D0
    
    co2vmr         = -1.0D0    
    
    f11vmr         = -1.0D0
    
    f12vmr         = -1.0D0
    
    flbc_file      = '/cluster/shared/noresm/inputdata/atm/waccm/lb/LBC_1750-2015_CMIP6_GlobAnnAvg_c180926.nc'
    
    flbc_list      = 'CO2','CH4','N2O','CFC11eq','CFC12'
    
    flbc_type      = 'SERIAL'
    
    n2ovmr         = -1.0D0
    
    scenario_ghg   = 'CHEM_LBC_FILE'
    
  /

4) However, instead of checking out a branch/release-tag with model version 2.0.x, check out the branch remotes/origin/noresm2.2, e.g.:
  ``git checkout -b noresm2.2 origin/noresm2.2``

For issues related to model installation (e.g. svn-related) see `NorESM webpage <https://noresm-docs.readthedocs.io/en/latest/access/download_code.html#make-a-clone-of-the-noresm-repository/>`_.

