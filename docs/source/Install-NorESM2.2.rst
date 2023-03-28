Install NorESM2.2
=============================================

To install NorESM2.2 follow instructions on `NorESM webpage <https://noresm-docs.readthedocs.io/en/latest/access/download_code.html#make-a-clone-of-the-noresm-repository/>`_:

1) First clone the NorESM repository to a folder <noresm-base>: 
  `` git clone https://github.com/NorESMhub/NorESM.git <noresm-base> `` 

2) Then enter the specified directory:
  `` cd <noresm-base> ``

3) List all available branches for checkout:
  `` git branch --all ``

4) However, instead of checking out a branch/release-tag with model version 2.0.x, check out the branch remotes/origin/noresm2.2, e.g.:
  `` git checkout -b noresm2.2 origin/noresm2.2 ``

For issues related to model installation (e.g. svn-related) see `NorESM webpage <https://noresm-docs.readthedocs.io/en/latest/access/download_code.html#make-a-clone-of-the-noresm-repository/>`_.


