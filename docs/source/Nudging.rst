Regional Nudging
=============================================

.. warning::
  * Again, care must be taken when using the results of this model version (pre-release). 
  * Regional Nudging presented below only works in `NorESM2.2 <https://noresm22-nudging-regional.readthedocs.io/en/latest/Install-NorESM2.2.html>`_ (i.e., not in earlier versions). 
  * Also, only `historical AMIP experiment <https://noresm22-nudging-regional.readthedocs.io/en/latest/AMIP-configuration.html>`_ on Betzy/Sigma2 has been tested.

---------------------

**This page is still under development.**

Below is "non-relevant" text.

---------------------

Regional nudging has been implemented in the latest version of the CESM (CESM2.2, CAM6.3) model, thus the details of the implementation can be found  `here <https://ncar.github.io/CAM/doc/build/html/users_guide/physics-modifications-via-the-namelist.html#nudging>`_. Below we merely show an example (a summary) of such implementation in NorESM2.2, which is based on the CESM2.2.

One you have created a case folder ``<case-name>`` (e.g., see `here <https://noresm22-nudging-regional.readthedocs.io/en/latest/AMIP-configuration.html>`_), you can specify nudging (global or regional) in ``user_nl_cam``. Below is an example for regional nudging over midlatitude North Pacific.

.. admonition:: user_nl_cam

  &nudging_nl
  
    Nudge_Model = .true.
    
    Nudge_Path = '/cluster/projects/nn9039k/CAM_Nudging/met_data/era5_PSUV_f09L32_6hrAnomalySingleRecord/'
    
    Nudge_File_Template= 'era5-ano_PSUV_f09L32_6hr_r0_%y%m%d%s.nc'
    
    Nudge_Force_Opt = 1
    
    Nudge_TimeScale_Opt = 0 ! (=0 for weak nudging & =1 for strong nudging)
    
    Nudge_Times_Per_Day= 4 ! for 6-hourly target data for nudging (e.g. ERA5)
    
    Model_Times_Per_Day= 48 ! for a model with a 30-minute timestep (like NorESM2.2-AMIP)
    
    Nudge_Uprof = 2
    
    Nudge_Ucoef =1.00
    
    Nudge_Vprof = 2
    
    Nudge_Vcoef =1.00
    
    Nudge_Tprof =0
    
    Nudge_Tcoef =1.00
    
    Nudge_Qprof =0
    
    Nudge_Qcoef =1.00
    
    Nudge_PSprof =0
    
    Nudge_PScoef =0.00
    
    Nudge_Beg_Year = 1979
    
    Nudge_Beg_Month= 1
    
    Nudge_Beg_Day = 1
    
    Nudge_End_Year = 2013
    
    Nudge_End_Month= 12
    
    Nudge_End_Day = 31
    
    Nudge_Hwin_lat0 = 45. ! 0.0
    
    Nudge_Hwin_latWidth= 45. ! set to 999. for full longitudinal circle
    
    Nudge_Hwin_latDelta= 5.0 !2.0
    
    Nudge_Hwin_lon0 = 180. !180.
    
    Nudge_Hwin_lonWidth= 100. ! set to 999. for full latitudinal circle
    
    Nudge_Hwin_lonDelta= 5. 
    
    Nudge_Hwin_Invert =.false. ! set to .true. for inverted nudging window
    
    Nudge_Vwin_Hindex = 33. 
    
    Nudge_Vwin_Hdelta = 0.001 ! const vertical window ! set to a larger value (number of levels over which it tapers off)
    
    Nudge_Vwin_Lindex = 13. !0.  full vertical extent !13.  troposphere only & taper off in lower stratosphere (lev 13 ~150 hPa; lev 15 ~200 hPa; lev 11 ~100 hPa) !32.  surface layer only
    
    Nudge_Vwin_Ldelta = 2. 
    
    ! 2. taper-off over +/- 2 levels ! 0.001 const. vertical window
    
    Nudge_Vwin_Invert =.false. ! set to .true. for inverted nudging window
    
  /

The variables are described `here <https://ncar.github.io/CAM/doc/build/html/users_guide/physics-modifications-via-the-namelist.html#nudging>`_ in more detail, but we provide a short summary here:

* bla

* Nudge_Uprof (and equivalents for V, T, Q, PS) - states what kind of nudging in, e.g.,  U we want (=0 no nudging, =1 global nudging, =2 regional nudging):

  * For global nudging of U,V specify ``Nudge_Uprof = Nudge_Vprof = 1, Nudge_PSprof = Nudge_Tprof = Nudge_Qprof = 0``

  * For regional nudging of U,V specify ``Nudge_Uprof = Nudge_Vprof = 2, Nudge_PSprof = Nudge_Tprof = Nudge_Qprof = 0``
  


At the moment there is the following capability for nudging in NorESM2.2:

* Anomaly nudging to `historical AMIP experiment <https://noresm22-nudging-regional.readthedocs.io/en/latest/AMIP-configuration.html>`_ climatology with ERA5 anomalies over the period 1979-2016. Data is available for PS, U, V variables only. Set the following path & file-name in ``user_nl_cam``:
  ``Nudge_Path = '/cluster/projects/nn9039k/CAM_Nudging/met_data/era5_PSUV_f09L32_6hrAnomalySingleRecord/'``
  ``Nudge_File_Template= 'era5-ano_PSUV_f09L32_6hr_r0_%y%m%d%s.nc'``
  
* bla
  
For now, we have only tested U & V nudging, while PS nudging is also available. We expect to increase the number of variables available for nudging (to, e.g., T, Q). If you do not have access to the data specified above please contact us (lina.boljka@uib.no).

----------------

To visualise the nudging window used (e.g., prior to implementing it in the model) do the following:

1) ...

2) ...


----------------

Also, topography data from a reanalysis can be specified in ``user_nl_cam``, although be aware that ERA5 topography may be very different from model topography and thus care must be taken!

.. admonition:: user_nl_cam

  &cam_initfiles_nl
  
    use_topo_file=.true.
    
    bnd_topo = '/cluster/shared/noresm/inputdata/noresm-only/inputForNudging/ERA_f09f09_32L_days/ERA_bnd_topo_noresm2_20191023.nc'
    
  /

At the moment only the ERA-Interim topography data is available (as specified above), i.e., it has not been tested with ERA5 topography.

