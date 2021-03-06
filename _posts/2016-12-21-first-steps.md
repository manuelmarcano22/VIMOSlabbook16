---
layout: post
title: "First Steps"
categories: [log]
tags: [VIMOS,data]
---

# The Context:

## The Galatic Bulge Survey

As described in detail [here](https://personal.sron.nl/~peterj/gbs/index.html):

> The Galactic Bulge Survey is a multiwavelength survey of 12 square degrees of the Galactic bulge in the vicinity of the Galactic center.

The first paper introducing the Galactic Bulge Survey (GBS) is <span class="citation" data-cites="jonker11">P. G. Jonker et al. (2011)</span>

It included near infrared, X-ray and optical wavelengths. In the X-ray it was done with the Chandra X-ray observatory. The optical photometry observations in r’, i’and H<span class="math inline">\(\alpha\)</span> filters were taken with the MOSAIC-II imager and the Dark Energy Camera (DECam) mounted in the 4-m Victor M. Blanco telescope at Cerro Tololo Inter-American Observatory in Chile. And the near infrared photometry with ESOs VISTA telescope as part of the VISTA Variables in The Via Lactea (VVV) public survey survey.

Several multiwavelength follow-up have been done. For example in the radio matching the GBS sources with the National Radio Astronomy Observatory (NRAO) Very Large Array (VLA) Sky Survey have been published by <span class="citation" data-cites="Maccarone11112012">T. J. Maccarone et al. (2012)</span> .

Also an optical spectroscopic survey have been on going with instruments like the **Visible Multi-Object Spectrograph (VIMOS)**. This is the data I will be working with.

## The catalog 

[Here](http://iopscience.iop.org/0067-0049/194/2/18/suppdata/apjs386787t3_mrt.txt). 



## Visible Multi-Object Spectrograph (VIMOS)

From the ESO [instrument description](http://www.eso.org/sci/facilities/paranal/instruments/vimos.html):

> VIMOS <span class="citation" data-cites="vimospaper2003">(Le Fèvre et al. 2003)</span> is a visible (360 to 1000 nm) wide field imager and multi-object spectrograph mounted on the Nasmyth focus B of UT3 Melipal.

VIMOS has three different modes: Imaging (IMG), Integral Field Unit (IFU), and Multi-Object-Spectroscopy (MOS) mode. The observation for the data I am going to use was in the MOS mode.

### Multi-Object-Spectroscopy (MOS) and Imaging mode

The multi-object mode of VIMOS uses grisms (6 grating prism) and masks, that depending on location, the spectral range can be up to ~370-620 nm. Depending on the grism used, the spectral resolution varies from 200 to 2500, and the observable range is from 360 to 1000 nm. The maximum number of slits per mask (quadrant) varies from ~40 at R=2500 to ~150-200 at R=200, for a field of view of 4 x 7’ x 8’.

For imaging the field of view in imaging mode consists in **4 quadrants** of 7’ x 8’ each, separated by a cross 2’ wide. Imaging with VIMOS is offered with a set of 6 broad band filters. Each arm of VIMOS is equipped with its own set of filters and some minor difference may exist in the transmission curve of the 4 quadrants. Imaging is possible in UBVRIz filters in a 4 x 7’ x 8’ field of view.

Information for the filters can be found [here](http://svo2.cab.inta-csic.es/svo/theory/fps3/index.php?id=Paranal/VIMOS.R&&mode=browse&gname=Paranal&gname2=VIMOS#filter).

A summary can be found in [here](http://www.eso.org/sci/facilities/paranal/instruments/vimos/inst/mos.html).

### Some resources and papers:

*   Website: [The Galactic Bulge Survey](https://personal.sron.nl/~peterj/gbs/index.html)

*   Presentation: [The Chandra Galactic Bulge Survey by Dr. Torres](http://cxc.harvard.edu/symposium_2014/presentations/macTalks/Nov21/Torres_Manuel.pdf)

*   Presentation: [Galactic Bulge Survey by Jonker](http://cxc.cfa.harvard.edu/ChandraDecade/PDFs/Jonker_11.pdf)

## The goal:

My goal will be to:

> Identify if the target was centered (or partially located) on the slit by looking to the slit region files projected on the pre-images. If so, identify the corresponding slit and target spectrum in the 2D spectra and do the extraction.

### Example for CX25

#### Theory

From Simbad is an LMXB at _FK5 coord. (ep=J2000 eq=2000) : 17 48 04.831 -24 46 48.87_. In the preimage it is _17 45 03 -31 59 34_. But Dr. Torres says that the astrometry is not the best in the pre-images.

In <span class="citation" data-cites="patruno12cx25">(Patruno et al. 2012)</span> it says:

> The low mass X-ray binary (LMXB) IGR J17480–2446 in the globular cluster Terzan 5 harbors an 11 Hz accreting pulsar. […] The source is in core of Terzan 5, one of the densest among globular clusters.[…] The accreting pulsar spins with a frequency of 11 Hz and the LMXB has a period of 21.3 hr around a companion with mass M > 0.4 <span class="math inline">\(M_{\odot}\)</span>AAlthough this pulsar is not a millisecond one, its location in a globular cluster makes it a unique system whose properties are of particular importance for studying the recycling mechanism.

#### VIMOS Data

#### **Pre-image**

From pre-images with the region file generated by Dr. Torres script and displayed in ds9 using:

`ds9 VI_SREI_544351_2011-04-01T09:22:43.312_R_Q4_lo.fits -scale zscale -regions 544351_577734_Q4.reg &`

<figure>![](/VIMOSlabbook16/images/preimagecx25.png)

<figcaption>CX25 Preimage</figcaption>

</figure>

**Why he says source is off center?** Imaging is possible in UBVRIz filters in a 4 x 7’ x 8’ field of view. It is in the R filter according to the header entry:

`[...] FILT4 NAME = 'R ' / Filter name`

For this filter the range is 560-723 nm. **Does that have to do that it is quadrant 4?**

It is category **IMG_SCIENCE_REDUCED** so created by: vmimpreimaging, vmimobsstare, vmimobsjitter. Since it used the

`HIERARCH ESO PRO REC1 RAW1 CATG = 'IMG_SCIENCE' / Category of raw frame`

I think it was produced by the recipe **vmimobsstare**.

#### **The spectrum**

<figure>![](/VIMOSlabbook16/images/spectracx25.png)

<figcaption>broad slit</figcaption>

</figure>

Dr. Torres says that there it is a broad slit with 2 objects associated to the slit containing CX25 and there are **other 3 slits**.

It says:

> When only one slit is found in the VIMOS quadrant, the pipeline likes to add the spectra of stars on the reference boxes. The reference boxes are used to align the slit-maks during the observations. These boxes are 5 x 5 arcsec wide compare to the 1" -width slits

This won’t be always the same and might have SLIT1 through 4 in the pre-images and in the same order or inverse in the spectra fits. Things to remeber about the 2D spectra:

*   2D have been **rectified**
*   2D are **wavelenght calibrated**. But do **not* trust** radial velocities**.
*   The 2D spectra are in count rates (counts/second). So you need to multiply ([imarith](http://stsdas.stsci.edu/cgi-bin/gethelp.cgi?imarith)) the data by the integration time before extracting the spectrum. **Is it the header file EXPTIME**?. For CX25 looking at the spectra: `EXPTIME = 874.99 / Total integration time. 00:14:34.990`

# References

<div id="refs" class="references">

<div id="ref-jonker11">

Jonker, P. G., C. G. Bassa, G. Nelemans, D. Steeghs, M. A. P. Torres, T. J. Maccarone, R. I. Hynes, et al. 2011\. “The Galactic Bulge Survey: Outline and X-Ray Observations.” _The Astrophysical Journal Supplement Series_ 194 (2): 18\. [http://stacks.iop.org/0067-0049/194/i=2/a=18](http://stacks.iop.org/0067-0049/194/i=2/a=18).

</div>

<div id="ref-vimospaper2003">

Le Fèvre, O., M. Saisse, D. Mancini, S. Brau-Nogue, O. Caputi, L. Castinel, S. D’Odorico, et al. 2003\. “Commissioning and performances of the VLT-VIMOS instrument.” In _Instrument Design and Performance for Optical/Infrared Ground-Based Telescopes_, edited by M. Iye and A. F. M. Moorwood, 4841:1670–81\. SPIE. doi:[10.1117/12.460959](https://doi.org/10.1117/12.460959).

</div>

<div id="ref-Maccarone11112012">

Maccarone, Thomas J., Manuel A. P. Torres, Christopher T. Britt, Sandra Greiss, Robert I. Hynes, Peter G. Jonker, Danny Steeghs, Rudy Wijnands, and Gijs Nelemans. 2012\. “Radio Sources in the Chandra Galactic Bulge Survey.” _Monthly Notices of the Royal Astronomical Society_ 426 (4): 3057–69\. doi:[10.1111/j.1365-2966.2012.21782.x](https://doi.org/10.1111/j.1365-2966.2012.21782.x).

</div>

<div id="ref-patruno12cx25">

Patruno, Alessandro, M. Ali Alpar, Michiel van der Klis, and Ed P. J. van den Heuvel. 2012\. “The Peculiar Evolutionary History of Igr J17480-2446 in Terzan 5.” _The Astrophysical Journal_ 752 (1): 33\. [http://stacks.iop.org/0004-637X/752/i=1/a=33](http://stacks.iop.org/0004-637X/752/i=1/a=33).

</div>

</div>

</div>


</article>

</div>

</div>

