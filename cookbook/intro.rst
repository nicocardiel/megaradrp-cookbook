

Introduction
============

Scope
-----

The goal of this document is to guide any potential user of the MEGARA
instrument in its data processing, from the raw data provided by the GTC
to wavelength- and flux-calibrated scientific-valid data. The MEGARA
data processing described in this document will be done using the MEGARA
Data Reduction Pipeline (DRP) which is available through *github* at
https://github.com/guaix-ucm/. The different releases of this document
will cope with any major change in the MEGARA DRP.

MEGARA instrument
-----------------

MEGARA (*Multi-Espectrógrafo en GTC de Alta Resolución para Astronomía*)
is a fiber-fed spectrograph with both Integral-Field (IFU) and
Multi-Object (MOS) capabilities that was installed and commissioning at
the 10.4m GTC telescope in the Spring of 2017. Since semester 2018B,
MEGARA is available to the GTC community (Spain, Mexico and UF) in its
two modes (LCB and MOS). The reader is referred to Gil de Paz et al.
(2020, submitted) for more details.

The MEGARA IFU, which is called Large Compact Bundle (LCB hereafter),
covers a field of 12.5 x 11.3 arcsec\ :sup:`2` using 567 hexagonal
spaxels of 0.62 arcsec in size plus 56 sky spaxels of equal size
distributed in 8 bundles of 7 fibers distributed in the outskirts of the
field at about 2 arcmin from the center of the LCB. The MOS makes use of
a set of 92 robotic positioners each hosting a minibundle of 7 spaxels
also of 0.62 arcsec in size each spaxel. These can patrol overlapping
circular regions of 28 arcsec in diameter. These robotic positioners a
distributed in a square region of 3.5 x 3.5 arcmin\ :sup:`2`, which
roughly corresponds to the flat and non-vignetted focal plane of GTC at
its Folded-Cassegrain F (FC-F) focus (see **Figure 1**). The MOS can be
reconfigured starting from a list of target potions in matter of roughly
a minute to a few minutes, depending on the level of number of
overlapping patrol areas to be explored in a given configuration.

|image1| |image2|

Figure 1: LCB and MOS in the focal plane of MEGARA at the Folded-Cass F
focus of GTC. Left: Layout of the monolithic microlens array of the LCB
placed at the optical axis of the instrument. Center: Hexagons
representing the patrol areas of the 92 robotic positioners of the
MEGARA MOS (in light grey) along with the positions of the eight sky
bundles that are mounted along the LCB pseudo-slit (in orange). Note
that the actual patrol areas are overlapping circular regions of 28
arcsec in diameter, while the distance between adjacent positioners is
24.5 arcsec. Right: MEGARA focal plane before the field lens was
installed at the Laboratorio de Instrumentación Científica Avanzada
(LICA-UCM) laboratory.

Both the LCB and the MOS along with other subsystems (focal-plane cover,
Folded-Cassegrain rotator adapter, etc.) are located at the FC-F focus
of GTC. The 623 (567+56) fibers of the LCB and the 644 fibers of the 92
robotic positioners of the MOS are routed through from the FC-F rotator
to the Nasmyth A platform following a 44.5m-long path until they reach
the MEGARA spectrograph. The MEGARA spectrograph is a fixed-angle (68º)
collimator-camera system that is fed by two interchangeable curved
pseudo-slits (LCB/MOS). The collimator is an all-refractive F/3 system
composed by 5 lenses (1 aspheric singlet and 2 doublets) while the also
all-refractive camera is composed by 7 lenses (two doublets, one with a
CaF\ :sub:`2` lens, and 3 singlets). In between collimator and camera,
the spectrograph pupil can host different types of Volume-Phase
Holographic (VPH) disperser elements, namely the low- (LR), mid- (MR),
and high-resolution (HR) VPHs. Six LR VPHs cover the entire optical
window at R=6,000, while 10 MR VPHs provide also full optical coverage
but at R=12,000. Finally, the two HR VPHs allow observing in the
Hα+[NII] region and in the CaT region with R=20,000, although the
optical design could in principle accommodate HR VPHs at any other
optical wavelength. In **Figure 2** we show the resolving power and
spectral coverage for each VPH as measured during the integration and
commissioning of the instrument [1]_.

|image3|\ |image4|\ |image5|\ |image6|

**Figure 2:** *Plots showing the relation between resolving power
(RFWHM) and wavelength coverage for all 18 MEGARA VPHs and for the LCB
(left) and MOS (right) modes. Design values (colored lines) and
measurements (grey lines that correspond to individual fiber spectra,
while black thick and thin lines represent the mean and mean*\ ±1σ
*curves when all fiber spectra are used) are both shown.*

The details on the different VPHs that can be used with MEGARA is given
in Table 1. This table also includes the reciprocal (linear) dispersion
(CDELT) and wavelength for the initial pixel (CRVAL for CRPIX=1) as
adopted for the MEGARA DRP for different VPHs. The user is referred to
different publications to learn more about the MEGARA instrument,
including [R.1], [R.2] and [R.3].

+----------+------+-----+---------+----+-------+-----+------+------+
| VPH Name | S    | R\  | λ\      | λc | Δλ (@ | Δv  | lin  | λ(p  |
|          | etup |  :s |  :sub:` |    | λc)   |     | res  | ix1) |
|          |      | ub: | 1`-λ\ : | Å  |       | k   |      |      |
|          |      | `FW | sub:`2` |    | Å     | m/s | Å    | Å    |
|          |      | HM` |         |    |       |     | /pix |      |
|          |      |     | Å       |    |       |     |      |      |
+==========+======+=====+=========+====+=======+=====+======+======+
| V        | LR-U | 6   | 3653 –  | 40 | 0.672 | 50  | 0    | 3620 |
| PH405-LR |      | 028 | 4386    | 51 |       |     | .186 |      |
+----------+------+-----+---------+----+-------+-----+------+------+
| V        | LR-B | 6   | 4332 –  | 48 | 0.792 | 49  | 0.23 | 4280 |
| PH480-LR |      | 059 | 5196    | 00 |       |     |      |      |
+----------+------+-----+---------+----+-------+-----+------+------+
| V        | LR-V | 6   | 5143 –  | 56 | 0.937 | 49  | 0.27 | 5060 |
| PH570-LR |      | 080 | 6164    | 95 |       |     |      |      |
+----------+------+-----+---------+----+-------+-----+------+------+
| V        | LR-R | 6   | 6094 –  | 67 | 1.106 | 49  | 0.31 | 6030 |
| PH675-LR |      | 099 | 7300    | 47 |       |     |      |      |
+----------+------+-----+---------+----+-------+-----+------+------+
| V        | LR-I | 6   | 7220 –  | 79 | 1.308 | 49  | 0.37 | 7140 |
| PH799-LR |      | 110 | 8646    | 91 |       |     |      |      |
+----------+------+-----+---------+----+-------+-----+------+------+
| V        | LR-Z | 6   | 8043 -  | 89 | 1.455 | 49  | 0.41 | 7960 |
| PH890-LR |      | 117 | 9630    | 00 |       |     |      |      |
+----------+------+-----+---------+----+-------+-----+------+------+
| V        | MR-U | 12  | 3917 -  | 41 | 0.326 | 24  | 0    | 3905 |
| PH410-MR |      | 602 | 4277    | 04 |       |     | .089 |      |
+----------+------+-----+---------+----+-------+-----+------+------+
| V        | M    | 12  | 4225 –  | 44 | 0.358 | 24  | 0.10 | 4210 |
| PH443-MR | R-UB | 370 | 4621    | 31 |       |     |      |      |
+----------+------+-----+---------+----+-------+-----+------+------+
| V        | MR-B | 12  | 4586 –  | 48 | 0.395 | 25  | 0.11 | 4568 |
| PH481-MR |      | 178 | 5024    | 14 |       |     |      |      |
+----------+------+-----+---------+----+-------+-----+------+------+
| V        | MR-G | 12  | 4963 –  | 52 | 0.433 | 25  | 0    | 4944 |
| PH521-MR |      | 035 | 5443    | 13 |       |     | .122 |      |
+----------+------+-----+---------+----+-------+-----+------+------+
| V        | MR-V | 11  | 5393 –  | 56 | 0.476 | 25  | 0    | 5375 |
| PH567-MR |      | 916 | 5919    | 67 |       |     | .132 |      |
+----------+------+-----+---------+----+-------+-----+------+------+
| V        | M    | 11  | 5869 –  | 61 | 0.522 | 25  | 0    | 5850 |
| PH617-MR | R-VR | 825 | 6447    | 70 |       |     | .145 |      |
+----------+------+-----+---------+----+-------+-----+------+------+
| V        | MR-R | 11  | 6241 –  | 65 | 0.558 | 25  | 0.16 | 6210 |
| PH656-MR |      | 768 | 6859    | 63 |       |     |      |      |
+----------+------+-----+---------+----+-------+-----+------+------+
| V        | M    | 11  | 6764 –  | 71 | 0.608 | 26  | 0.17 | 6735 |
| PH712-MR | R-RI | 707 | 7437    | 15 |       |     |      |      |
+----------+------+-----+---------+----+-------+-----+------+------+
| V        | MR-I | 11  | 7382 –  | 77 | 0.666 | 26  | 0.   | 7360 |
| PH777-MR |      | 654 | 8120    | 67 |       |     | 1845 |      |
+----------+------+-----+---------+----+-------+-----+------+------+
| V        | MR-Z | 11  | 8800 -  | 92 | 0.796 | 26  | 0    | 8770 |
| PH926-MR |      | 638 | 9686    | 62 |       |     | .225 |      |
+----------+------+-----+---------+----+-------+-----+------+------+
| V        | HR-R | 18  | 6445 -  | 66 | 0.355 | 16  | 0.   | 6390 |
| PH665-HR |      | 700 | 6837    | 46 |       |     | 0974 |      |
+----------+------+-----+---------+----+-------+-----+------+------+
| V        | HR-I | 18  | 8372 -  | 86 | 0.462 | 16  | 0.13 | 8350 |
| PH863-HR |      | 701 | 8882    | 34 |       |     |      |      |
+----------+------+-----+---------+----+-------+-----+------+------+

Table 1: MEGARA VPHs: scientific requirements (The resolution,
R\ :sub:`FWHM`\ =λ/∆λ\ :sub:`FWHM`, is derived from the FWHM
(∆λ\ :sub:`FWHM`) of the 1D spectra). The values of the linear
reciprocal dispersion and the wavelength of pixel 1 correspond to the
linear solution implemented in the MEGARA DRP after the images are
wavelength calibrated.

Note that the reciprocal dispersion is the one used for the linear
solution in the images processed by the MEGARA Data Reduction Pipeline.

.. [1]
   Note that in some of the cases the spectral coverage shown is shorter
   than the one actually achieved simply because the spectral lamp lacks
   bright spectral features (on which to measure the spectral resolution
   and resolving power), especially at the blue end of the optical
   spectral range.

.. |image1| image:: _static/image2.png
   :width: 3.65278in
   :height: 2.34722in
.. |image2| image:: _static/image3.jpeg
   :width: 2.60208in
   :height: 2.04792in
.. |image3| image:: _static/image4.png
   :width: 6.81319in
   :height: 3.43194in
.. |image4| image:: _static/image5.png
   :width: 6.81319in
   :height: 3.43194in
.. |image5| image:: _static/image6.png
   :width: 6.81319in
   :height: 3.43194in
.. |image6| image:: _static/image6.png
   :width: 6.81319in
   :height: 3.43194in
.. |image7| image:: _static/image10.png
   :width: 6.63681in
   :height: 3.09306in
