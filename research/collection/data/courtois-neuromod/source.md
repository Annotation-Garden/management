# DEPFET Active Pixel Sensors

# DEPFET Active Pixel Sensors

Norbert Meidinger and Johannes Müller-Seidlitz

Abstract An array of DEPFET pixels is one of several concepts to implement an active pixel sensor. Similar to PNCCD and SDD detectors, the typically  $450\mu \mathrm{m}$  thick silicon sensor is fully depleted by the principle of sideward depletion. They have furthermore in common to be back-illuminated detectors, which allows for ultra-thin and homogeneous photon entrance windows. This enables relatively high quantum efficiencies at low energies and close to  $100\%$  for photon energies between  $1\mathrm{keV}$  and  $10\mathrm{keV}$ . Steering of the DEPFET sensor is enabled by a so-called Switcher ASIC and readout is performed by e.g. a VERITAS ASIC. The configuration enables a readout time of a few microseconds per row. This results in full frame readout times of a few milliseconds for a  $512\times 512$  pixel array in a rolling shutter mode. The read noise is then typically three electrons equivalent noise charge RMS. DEPFET detectors can be applied in particular for spectroscopy in the energy band from  $0.2\mathrm{keV}$  to  $20\mathrm{keV}$ . For example, an energy resolution of about  $130\mathrm{eV}$  FWHM is achieved at an energy of  $6\mathrm{keV}$  which is close to the theoretical limit given by Fano noise. Pixel sizes of a few tens of microns up to a centimetre are feasible by the DEPFET concept.

Dr. Norbert Meidinger
Max Planck Institute for Extraterrestrial Physics, Gießenbachstraße 1, 85748 Garching, Germany, e-mail: norbert.meidinger@mpe.mpg.de

Dr. Johannes Müller-Seidlitz
Max Planck Institute for Extraterrestrial Physics, Gießenbachstraße 1, 85748 Garching, Germany, e-mail: johannes.mueller-seidlitz@mpe.mpg.de

* corresponding author

---

1 Introduction

The DEPFET concept had already been proposed by Kemmer and Lutz in 1987 [11]. Since then, various implementations were developed for different applications and scientific fields. They serve as particle trackers in the high radiation environments near the collision point of particle accelerators. Mounted at an X-ray free-electron laser, they can help to unveil the nature of fast processes on tiny scales in various disciplines.

The first spectroscopic DEPFETs for space applications were developed for the Mercury Imaging X-ray Spectrometer aboard the BepiColombo mission orbiting the planet Mercury [28]. The next space project with the employment of DEPFETs is the Wide Field Imager (WFI) of ATHENA, ESA’s Advanced Telescope for High-Energy Astrophysics [22].

These silicon-based DEPFET concepts have been designed and the devices fabricated in the Semiconductor Laboratory of the Max-Planck-Society [15]. They are similar to those of PN-implanted Charge Coupled Devices (PNCCD) [19] and Silicon Drift Detectors (SDD). All three detector types feature a sideward depletion [8] which enables a sensitivity over the full chip thickness. Therefore, all three sensor types can be back illuminated which allows for a thin and homogeneous photon entrance window over the sensor area. In PNCCDs, the signal charge needs to be transferred along the channel to a readout node, which is not necessary for DEPFETs. An SDD detector has a very high time resolution in the order of a microsecond but comprises typically a small number of large cells. The generated signal is readout immediately and not stored. In a DEPFET, each pixel has a transistor implemented for charge storage and signal amplification as well as a second transistor for the signal charge clear afterwards.

## 2 Detector Concept

An active pixel sensor like the DEPFET features the first signal amplification already inside each pixel of the imaging sensor. Since such a readout node is implemented in every pixel, there is no need of charge transfer and no risk of potential charge loss due to traps in a transfer channel. As a drawback, the complexity of the detector is increased significantly because every pixel needs two transistors and the necessary steering and readout contacts.

The implementation and the readout concept will be explained first. The photon detection and charge collection as well as the electronics necessary to steer and read out the sensor are described afterwards.

The starting point for the sensor is a thin slice (wafer) of monocrystalline silicon. Such a semiconductor can be doped to influence its resistivity characteristics. Dopants are atoms with a number of outer shell electrons—the valence electrons—that differs from the four electrons in a silicon atom’s outer electron shell. If silicon atoms in the crystal lattice are replaced by such a dopant atom, the additional

---

electron or the missing one, a hole, change the electrical properties. A region with arsenic or phosphorus dopants—elements with five valence electrons—is called n-doped. The additional, weakly bound electrons with their negative charge are the majority charge carriers while the holes are called minority charge carriers. Doping with boron—an element with three valence electrons—leads to weakly bound holes, positively charged quasiparticles, that are the majority charge carriers in such a p-doped region. In both cases, the opposite charge in the atomic nucleus is stationary. The overall electric charge of a doped region is neutral.

At a p-n junction, where a p-doped and an n-doped region adjoin each other in the same crystal, the majority charge carriers of both regions diffuse into the other region and recombine. The stationary dopant atoms remain with four electrons. Thus, they are electrically charged. An electrical field between the now positive dopants in the n-doped region and the negative dopant atoms in the p-doped region is established. The resulting drift and the diffusion act in opposite directions and thereby an equilibrium is set up. The volume without majority charge carriers is called space charge region. By applying an external voltage, the space charge region can be extended (reverse bias, no current is possible) or it can be shrunken, even down to zero (forward bias, current in one direction).

For a more precise and deeper introduction into the terms introduced above, especially about the band model in solids, it is referred to the literature [12].

### 2.1 DEPFET Principle

An X-ray photon interacts in silicon and generates electrons, which drift to the storage region underneath the transistor in the centre of a pixel. The resulting transistor current increase is measured and, after calibration, gives the X-ray photon energy.

As transistor, a DEPFET is used. It is a DEpleted P-channel Field Effect Transistor, which performs amplification and switching. For a MOSFET—a Metal Oxide Semiconductor FET—a source and a drain region are implanted into the silicon wafer material. For the DEPFET, these are strong p-implants (p+) in initially slightly n-doped (n-) material. Space charge regions are formed around the source and drain regions. The surface is covered with an isolating layer, typically silicon dioxide and silicon nitride. Between the source and the drain implants on top of the isolating layer, a metallic contact is placed—the transistor gate [10]. In case of the DEPFET, it is formed of polycrystalline silicon. With a sufficiently negative voltage at the gate, holes will be collected below. They form a conductive layer, the p-channel, between source and drain. The assignment of the p+ implant being source or drain is performed via proper bias voltages. Since there is a hole current in the p-channel, the source is the contact with the more positive voltage level. In addition to such a simple MOSFET, a shallow n-doping is implanted below the transistor channel for the DEPFET. It is the potential minimum for electrons collected in the sensitive volume of the sensor. To avoid recombination and to facilitate the collection of signal electrons, the entire sensing device is depleted by applying a sufficient high

---

Norbert Meidinger and Johannes Müller-Seidlitz

![img-0.jpeg](source_images/depfet-active-pixel-sensors-4aec10-fig-1.jpg)
Fig. 1 The DEPFET concept. Electrons collected in the Internal Gate increase the conductivity of the transistor channel between source and drain proportionally to their number. Afterwards, the collected electrons are removed by the clear transistor. The barrier below the clear shields the electrons in the bulk from a drift directly into the clear contact.

reverse bias to remove all majority charge carriers. The collected electrons generate mirror charges that are additional holes in the conductive channel which increase the conductivity of the transistor channel proportional to the number of collected electrons. The region is called Internal Gate because its function is similar to that of the (external) transistor gate. This increase of the transistor current allows for the determination of the X-ray photon energy.

The so-called charge gain $g_{q}$ quantifies the change in the current between source and drain $I_{DS}$ as a function of the collected signal charge $Q_{sig}$. For constant voltages between source and drain ($U_{DS}$) as well as source and gate ($U_{GS}$) the charge gain is proportional to square root of the current $I_{DS}$ between source and drain.

$g_{q}=\frac{\delta I_{DS}}{\delta Q_{sig}}\propto\sqrt{\frac{2\mu_{h}}{WL^{3}C_{ox}}I_{DS}}$ (1)

$C_{ox}$ is the capacity per unit area of the gate oxide, $L$ the length and $W$ the width of the gate, $\mu_{h}$ the hole mobility [14]. Due to the fact that the number of mirror charges is smaller than the number of collected electrons, the charge gain is proportional and not equal to the right term of Eq. 1.

To remove the collected charge carriers from the Internal Gate, a second transistor of NMOS type is implemented which allows for a controlled drift of the electrons towards the positive clear contact. A barrier below the clear contact shields it against the bulk to avoid the drift of signal electrons after their generation directly to the clear contact (see Fig. 1). A DEPFET pixel comprises both transistors, an adapted PMOS FET for signal sensing and the NMOS FET for the charge reset afterwards. To build an imaging detector, an appropriate pixel array is created. If pixels larger than 50 µm are needed, drift rings can be added around the transistors similar to a silicon drift detector (SDD) [14]. By a full depletion of the sensor thickness, back-illumination is feasible (see subsection 2.3). For a typical thickness of 450 µm, a reverse bias in the order of 100 V is necessary at the back side.

---

DEPFET Active Pixel Sensors

![img-1.jpeg](source_images/depfet-active-pixel-sensors-4aec10-fig-2.jpg)
Fig. 2 First most likely interactions of an absorbed X-ray photon with an energy below a few ten kiloelectron volts. The photon ionises a silicon atom. The empty position is then occupied by an electron from an outer shell. The surplus energy is emitted via a photon. This photon can ionise the same atom again and a so-called Auger electron is ejected from the atom.

### 2.2 Photon Interaction

When an X-ray photon of up to an energy of a few ten kiloelectron volts interacts with the silicon sensor, typically a photo electron is generated. As depicted in Fig. 2, a fluorescence photon or an Auger electron are emitted in addition. These processes will continue until thermalisation is reached. This results in a number of signal electrons proportional to the photon energy. The mean energy needed for the generation of an electron-hole pair is about $w = 3.71$ eV at 200 K [13]. The number of generated electrons varies according to Fano statistics [6] and causes a noise contribution called Fano noise.

$\sigma_{\rm Fano}=\sqrt{FwE}=\sqrt{0.118\cdot 3.71\,\rm eV\cdot E}$ (2)

with $\sigma_{\rm Fano}$ as the standard deviation, $F = 0.118$ the material specific Fano factor for silicon [13] and E the energy of the incident photon in electron volts.

### 2.3 Charge Collection

The concept of full depletion enables X-ray photon detection over the entire chip thickness of 450 µm [8]. This allows for a high quantum efficiency up to more than 15 keV. For this purpose, a negative voltage of about $-100$ V has to be applied at the photon entrance window in order to create a drift field for electrons towards the front side of the sensor. To enable an immediate sideward drift in large pixels, a structured front side in combination with a gradient in the bias voltages is necessary as shown in Fig. 3. The electrons generated by an incident X-ray photon drift along the electric field towards the potential minimum in each pixel. There, in the Internal Gate, the signal electrons are stored until they are measured and afterwards cleared.

A further advantage of full depletion is the possibility to have the photon entrance window at the back side of the sensor chip. It can be realised as an ultrathin layer with an uniform thickness over the entire sensor area. The structures at the front

---

Norbert Meidinger and Johannes Müller-Seidlitz

![img-2.jpeg](source_images/depfet-active-pixel-sensors-4aec10-fig-3.jpg)
Fig. 3 Charge collection in a sideways depleted sensor [8]. Electrons drift along the electric field towards the potential minimum (blue). In vertical direction, an asymmetric, parabolic, electric potential separates the electrons and holes. A sideward drift is induced by a static gradient of the applied voltages at the front side  $\mathfrak{p}+$  implants at the top.

side would prevent such a layer (see Fig. 1). A thin layer is required to reduce the region where generated electrons recombine with holes and are lost for the signal measurement. Due to their lower absorption length, this is in particular important for low energetic X-ray photons.

# 2.4 Steering and Readout Electronics

As shown in Fig. 4, the pixels of the current DEPFET X-ray sensors are connected row-wise to steering ASICs (Application Specific Integrated Circuit), the so-called Switcher [7]. The switchable contacts of a DEPFET (gate, clear gate and clear) are supplied with appropriate voltage levels for on- and off-state of the DEPFET transistors. For the readout of the signal charges collected in the DEPFET pixels, a second type of ASIC is needed. It performs the further amplification and shaping. By use of a multi-channel readout ASIC like the VERITAS [24], a DEPFET column is connected to a dedicated ASIC channel. Thereby, the signals of these channels are processed simultaneously. After the processing is completed, the individual voltage signals are serialised to an output buffer. By this method, just one ADC (Analogue to Digital Converter) is needed per readout ASIC.

# 3 Operation

To reduce the complexity of the detector system and its power consumption, a DEPFET detector for space applications is typically operated in a rolling shutter mode. The Switcher ASIC turns on just one row of the DEPFET sensor while all other rows are switched off. Switched off pixels are still collecting incoming signal charges but consume no power. After the readout by the VERITAS is finished, the row is switched off and the next one is switched on and read out. This will be con

---

DEPFET Active Pixel Sensors

![img-3.jpeg](source_images/depfet-active-pixel-sensors-4aec10-fig-4.jpg)
Fig. 4 Equivalent circuit diagram for a DEPFET detector. Four by two pixels are shown. The gates (connected via light blue lines), clears (green) and clear gates (dark blue) are connected to the steering ASIC. The sources are biased globally (yellow) and the drains are read out via the readout ASIC (orange).

tinued until all the rows of a frame are read out and the sequence starts again with the next frame.

The readout itself is split into two parts: In a first step, the baseline signal of the pixel is read together with the collected electrons in the Internal Gate. Then, the electrons are removed from the Internal Gate via the clear transistor. Afterwards, a second signal sampling of the empty pixel is done. The VERITAS ASIC calculates the difference between the two levels (see Fig. 5). This correlated double sampling is applied to reduce the read noise.

Each electron collected in the Internal Gate of a DEPFET pixel increases the voltage level in the ASIC by a certain amount. The voltage difference measured by the readout ASIC gives thus the photon energy after calibration.

The main operating voltages for the operation of a DEPFET sensor are typically as follows:

Source:  $0\mathrm{V}$  (reference voltage)
$\diamond$  Drain:  $-6\mathrm{V}$  to  $-3\mathrm{V}$
$\diamond$  Gate:  $-2\mathrm{V}$  (on) and  $&gt; + 3\mathrm{V}$  (off)
$\diamond$  Clear Gate:  $+5\mathrm{V}$  to  $+10\mathrm{V}$  (on) and  $0\mathrm{V}$  (off)
$\diamond$  Clear:  $+15\mathrm{V}$  to  $+20\mathrm{V}$  (on) and  $+1\mathrm{V}$  (off)
$\diamond$  Back Contact:  $-100\mathrm{V}$

For larger pixels with drift structures, additional voltages at the front side may be needed.

To achieve a higher time resolution, the readout can be optimised. The VERITAS ASIC allows for a parallel signal processing and serialisation of the previously processed row. In addition, only a part of the sensor, a window, can be read out while the rest of the frame is discarded. The readout time scales with the number of rows inside the window [21].

Optimal spectroscopy requires a sufficiently low dark current. Thus, cooling of the DEPFET sensor is necessary, typically below  $-40^{\circ}\mathrm{C}$ . Furthermore, a constant temperature is needed for precise calibration (section 6).

---

Norbert Meidinger and Johannes Müller-Seidlitz

![img-4.jpeg](source_images/depfet-active-pixel-sensors-4aec10-fig-5.jpg)
Fig. 5 Readout scheme of a spectroscopic X-ray DEPFET with (green) and without (blue) signal. It consists of a first sampling, a clear of the signal electrons and a second, inverted sampling. The difference between the two samplings gives the signal and is proportional to the collected charge. Settling times need to be introduced to stabilise the signal level.

# 4 Performance Characteristics

The spectral performance is dominated by the Fano noise for photon energies above  $1\mathrm{keV}$ . At lower photon energies, the recombination of electron-hole pairs at the entrance window and thus signal loss contributes significantly to the energy resolution. The use of DEPFETs is best suited for an energy range of  $0.2\mathrm{keV}$  to  $15\mathrm{keV}$ . At a line energy of  $0.2\mathrm{keV}$ , the spectrum is still of Gaussian shape. The quantum efficiency (QE) at  $10\mathrm{keV}$  is  $96\%$  and at  $15\mathrm{keV}$  it is still  $63\%$ . The QE at low energies depends largely on the need for an optical blocking filter which can be deposited directly on the entrance window. A further key performance parameter is a read noise of about 3 electrons ENC (Equivalent Noise Charge) RMS. The pixel size which determines the spatial resolution can be matched in the range from about  $50\mu \mathrm{m}$  to centimetre scale to the angular resolution of the optics. The time resolution scales with the number of sensor rows. A typical readout time per row is in the order of a few microseconds.

# 4.1 Energy Resolution

The energy resolution of a DEPFET detector is not only determined by the Fano noise and the read noise which includes the dark current contribution. Additional noise contributions are given by:

- Charge losses due to recombination of electron-hole pairs close to the entrance window where the separating electric field is weak.
$\circ$  Incomplete charge collection because of a drift of signal electrons directly to the clear contact instead of to the Internal Gate.
$\circ$  Energy misfits describe signal read losses [21]. These can be caused by charge clouds arriving in the Internal Gate during the first signal sampling (see Fig. 5) or at the end of the clear pulse.

---

DEPFET Active Pixel Sensors

![img-5.jpeg](source_images/depfet-active-pixel-sensors-4aec10-fig-6.jpg)
Fig. 6 Energy resolutions for different emission lines. From lower to higher energies, these are: C K-α, O K-α, Cu L-α, Al K-α, Ti K-α, Ti K-β, Cr K-α, Mn K-α. Entrance window effects degrade the spectral performance at lower energies. The measurements were taken with a  $256 \times 256$  pixel prototype sensor for ATHENA's WFI at a readout speed of  $6.1\mu s$  per row [27].

The signal charge can be split over more than one pixel. For energy determination, the signal values have to be recombined. In space missions, the telemetry rate is limited and thus, data reduction is necessary. For this purpose, an event threshold needs to be set to discriminate between signal and noise events. Small signal fractions below the event threshold are lost for recombined events.
$\circ$  Instrument background mimicking X-ray source photons is caused by interaction of cosmic rays with the detector surrounding material. It consists typically of secondary electrons and photons [5]. The background can be reduced by the Self-Anti-Coincidence technique [9] that detects heavily ionising particles with the DEPFET detector itself and requires no additional Anti-Coincidence detector.

All these effects result in a broadening of a spectral line and apart from the background also in a signal loss. The energy resolution is parameterised by the Full Width at Half Maximum (FWHM) of the line. The shape of the spectrum is described by the detector response function which is energy dependent and accounts for the various charge loss effects.

In Fig. 6, the energy resolution of different emission lines is shown. For higher energies, the measured FWHMs are close to the Fano limit while at energies below  $1\mathrm{keV}$  the above mentioned effects degrade the spectral performance [27].

# 4.2 Performance Degradation in Space

There are three potential effects that can reduce the detector performance in space.

Radiation damage is caused by protons and alpha particles. They can destroy the silicon lattice which results in an increase of the dark current. To mitigate radiation damage effects, an appropriate shielding thickness depending on the orbit and mission lifetime and sufficient low DEPFET temperatures are necessary to lower the thermal generation current. An advantage of an active pixel sensor like the DEPFET compared to a Charge Coupled Device (CCD) is that no charge transfer is needed.

---

Norbert Meidinger and Johannes Müller-Seidlitz

![img-6.jpeg](source_images/depfet-active-pixel-sensors-4aec10-fig-7.jpg)
Fig. 7 The drawing shows the WFI detector assembly including the mechanical structure and the thermal architecture. The Fast Detector (FD) has an image area of  $8.3\mathrm{mm} \times 8.3\mathrm{mm}$  whereas the Large Detector Array (LDA) has a sensitive area of  $133\mathrm{mm} \times 133\mathrm{mm}$ .

Radiation damage effects in CCDs typically affect the charge transfer efficiency and thus the energy resolution even if the average transfer loss is corrected. Soft protons focused by the mirror on the focal plane do not cause critical radiation damage on the back-illuminated DEPFET. The reason is, that the transistors are accommodated on the front side.

A second potential performance degradation is caused by contamination of the photon entrance window. Molecules from inside or outside of the instrument can accumulate on the cold sensor surface. As a result the QE is reduced, primarily for low photon energies. The standard mitigation strategy is a bake-out of all instrument and satellite components before assembly to minimise outgassing in space. A further prevention measure is a warm optical blocking filter in front of the detector as the higher temperature minimises the accumulation of contamination from outside. A cold trap with a temperature below the one of the sensor could also reduce molecular contamination on the sensor and filter.

With the increasing mirror area of nowadays missions, the probability that micrometeoroids are deflected on the sensors rises as well. When a micro-meteoroid hits a pixel, the dark current can increase by a large amount and the spectroscopic performance of the hit pixel is deteriorated. An advantage of a DEPFET and its fast readout is the short time of dark current accumulation. A further mitigation is the choice of a low operating temperature.

---

DEPFET Active Pixel Sensors

![img-7.jpeg](source_images/depfet-active-pixel-sensors-4aec10-fig-8.jpg)
Fig. 8 Photo of an ATHENA WFI pixel  $(130\mu \mathrm{m}\times 130\mu \mathrm{m})$  In the centre, the DEPFET with the two clear contacts is accommodated. Two drift structures focus the charge carriers to the Internal Gate located below the (external) transistor gate. A metal supply line grid connects the pixel contacts to the ASICs and the global supplies (see Fig. 4).

# 5 Example Case: ATHENA WFI detector

The novel DEPFET detector concept was for the first time used in space for the Mercury Imaging X-ray Spectrometer (MIXS) on BepiColombo, a satellite for the exploration of planet Mercury [4] realised as joint mission of ESA and JAXA. The purpose of the MIXS instrument is the analysis of the elemental composition of the planet's surface by imaging X-ray spectroscopy of the fluorescence lines [16]. The DEPFET sensors consist of  $64 \times 64$  pixels with a pixel size of  $300\mu \mathrm{m} \times 300\mu \mathrm{m}$ . They are steered by Switcher ASICs and read out by two Asteroid readout ASICs [23]. This enables a readout time per frame of  $170\mu \mathrm{s}$ . The required energy resolution is  $\leq 200\mathrm{eV}$  FWHM at  $1\mathrm{keV}$  energy. BepiColombo was launched in October 2018 and will reach an orbit around Mercury end of 2025. The MIXS detector performance was verified during the travel to Mercury. The measured energy resolution was  $139\mathrm{eV}$  FWHM at an energy of  $5.9\mathrm{keV}$  [4].

The next application for DEPFETs in space is planned for the ATHENA Wide Field Imager (WFI), one of two focal plane instruments. ATHENA is ESA's next generation large class X-ray mission [22]. The launch to the first Lagrange point of the Sun-Earth system is scheduled for 2034. The WFI instrument is designed for imaging and spectroscopy over a large field of view of  $40^{\prime} \times 40^{\prime}$  and high count rate observations of up to and beyond 1 Crab source intensity [17, 18]. The WFI focal plane comprises therefore two complementary and independent detectors: A large detector array (LDA) consisting of four quadrants (LD) with  $512 \times 512$  pixels each and a fast detector (FD) with  $64 \times 64$  pixels, operated in split frame readout to improve the time resolution (see Fig. 7). The pixel size of both detectors is  $130\mu \mathrm{m} \times 130\mu \mathrm{m}$ , which matches the envisaged angular resolution of the silicon pore X-ray optics of  $5^{\prime \prime}$  half energy width (HEW). A photo of such a pixel is shown in Fig. 8.

At the beginning of the project, a technology development was performed to identify the optimum transistor design and technology for the WFI instrument [25]. To fulfil the timing requirements, a linear transistor gate design was selected (see section 7). Furthermore, the chosen thin gate oxides allow for self-aligned implants that enable a better uniformity of the pixel performance.

---

Norbert Meidinger and Johannes Müller-Seidlitz

![img-8.jpeg](source_images/depfet-active-pixel-sensors-4aec10-fig-9.jpg)
Fig. 9  $^{55}\mathrm{Fe}$  spectrum measured with a  $512 \times 512$  pixel DEPFET developed for ATHENA's WFI. The FWHM of the Mn K-  $\alpha$  line at  $5.9\mathrm{keV}$  is  $131\mathrm{eV}$  for a readout time of the entire sensor of  $2\mathrm{ms}$  and a DEPFET temperature of  $-60^{\circ}\mathrm{C}$ . In addition, the Mn K-  $\beta$  line at  $6.5\mathrm{keV}$ , the associated Si-escape lines and various fluorescence lines appear.

The ATHENA science cases require a time resolution of  $\leq 5\mathrm{ms}$  for the large detector array and  $\leq 80\mu s$  for the fast detector. In addition, an energy resolution of  $170\mathrm{eV}$  FWHM at an energy of  $7\mathrm{keV}$  and  $80\mathrm{eV}$  FWHM at  $1\mathrm{keV}$  energy is required until the end of life. The overall detection efficiency needs to achieve  $4.4\%$  at  $0.2\mathrm{keV}$ ,  $80\%$  at  $1\mathrm{keV}$ ,  $93\%$  at  $7\mathrm{keV}$  and  $90\%$  at  $10\mathrm{keV}$  for both detectors.

In Fig. 9, an energy spectrum measured with a large DEPFET detector of  $512 \times 512$  pixels is shown. Apart from the dominant emission lines generated by the  $^{55}\mathrm{Fe}$  source, further peaks appear. First, the silicon escape peaks which are caused by an escape of a silicon K-  $\alpha$  fluorescence photon (see Fig. 2) from the sensitive sensor volume. Thereby, the signal of the Mn K photon is reduced by the  $1.7\mathrm{keV}$  of the silicon escape photon. Second, fluorescence lines are observed which are generated when source photons hit material in the vicinity of the detector.

Fig. 10 shows a quadrant of the LDA and Fig. 11 the FD. To fulfil the performance requirements, the sensor needs to be cooled down to a temperature range between  $-80^{\circ}\mathrm{C}$  and  $-60^{\circ}\mathrm{C}$ . The lowest temperature is necessary to meet the energy resolution requirements until the end of the mission. The reason is that the DEPFET thermal generation current increases over mission time due to radiation damage. The front end electronics including the ASICs are operated at a higher temperature to minimise the radiator area on the satellite. The WFI camera uses passive cooling via radiators only. While the power consumption of the FD is  $3\mathrm{W}$ , the LDA dissipates  $44\mathrm{W}$  due to the large number of 64 ASICs that are needed for the fast readout of more than one million pixels. The detectors are connected via flexible leads to the electronics boxes. There, the necessary supply voltages and the timing sequence are generated. In total, 43 supply voltages and 22 steering signals per LD and nearly the same amount for the FD are required. In addition, the analogue output from the VERITAS ASICs are digitised and processed in the detector electronics box. This includes basic pixel signal corrections, e.g. subtraction of a dark image, and event detection to reduce the amount of data generated by  $&gt;260\mathrm{M}$  pixels/s for the detectors that needs to be transmitted to ground. Including all further required signals like housekeeping or the programming interface of the VERITAS ASIC, connectors with more than 200 pins are needed for each LD and FD to be operated by the electronics boxes.

---

DEPFET Active Pixel Sensors

![img-9.jpeg](source_images/depfet-active-pixel-sensors-4aec10-fig-10.jpg)
Fig. 10 Large DEPFET detector with  $512 \times 512$  pixels. Eight Switcher steering ASICs (left) with 64 channels each select the rows to be switched on and trigger the reset in the DEPFET. The eight 64-channel VERITAS ASICs (right) read the signal from the pixels that are switched on by the Switcher ASICs. The photon entrance window is located on the opposite side.

In front of the detector, a filter wheel is accommodated (Fig. 12). It provides the following functionalities. First, optical blocking filters made of aluminium deposited on polyimide [3]. Second, an onboard calibration source based on a radioactive  $^{55}\mathrm{Fe}$  source. Third, an open position which allows for observations with higher QE at low energies of optical faint objects. Fourth, a closed position to measure the instrumental background without source photons.

# 6 Calibration

Due to the fact, that each pixel has its own readout node, a pixel-wise calibration of the gain is necessary. This requires sufficient high photon statistics for every pixel in each operating mode (full frame, window modes).

The QE depends strongly on the photon energy, in particular for low energies below  $0.5\mathrm{keV}$  and for absorption edges of optical blocking filters and the photon entrance window materials. The photon entrance window of the DEPFET sensor consists of aluminium (optional, as optical blocking filter), silicon nitride and silicon oxide. The total thickness is in the order of a tenth of a micrometre.

The non-linearity of signal and photon energy needs to be calibrated in particular for low energies. The reasons are event detection threshold effects for split events and the electron-hole pair recombination near the photon entrance window.

---

Norbert Meidinger and Johannes Müller-Seidlitz

![img-10.jpeg](source_images/depfet-active-pixel-sensors-4aec10-fig-11.jpg)
Fig. 11 The Fast Detector's front side. The readout of the sensor is split into two parts and, therefore, is surrounded by the two steering and the two readout ASICs as well as the corresponding printed circuit board with its electronic components.

For the determination of the detector response, measurements of a series of monochromatic lines from the lowest to the highest energy are necessary. Instead of a line spectrum, a continuous spectrum is obtained due to the effects mentioned in section 4 and Fig. 9. Based on these measurements, the detector energy response function is developed.

On ground, calibration measurements are typically performed at a synchrotron. In space, regular recalibrations may be necessary due to changes caused e.g. by radiation damage and contamination. The in-orbit calibration can be performed by either an onboard calibration source (e.g.  $^{55}\mathrm{Fe}$  and stimulated fluorescence lines) or well known, bright cosmic sources.

Calibration in space is an ongoing activity to ensure an optimum detector performance during mission lifetime. Contamination would affect the QE and radiation damage degrades the energy resolution globally and accumulates continuously. In contrast, micro-meteoroid impacts occur as single events that cause a localised, single pixel damage in case of a DEPFET.

# 7 Outlook for DEPFET Options

The implementation of a DEPFET as introduced in subsection 2.1 can be approached in many ways. The usage of a circular gate as shown in Fig. 1 reduces the necessary structures to a minimum. The separation of the source and the drain

---

DEPFET Active Pixel Sensors

![img-11.jpeg](source_images/depfet-active-pixel-sensors-4aec10-fig-12.jpg)
Fig. 12 The WFI instrument with the camera head, that houses the detectors of FD and LDA. A filter wheel including the optical stray-light baffle is mounted in front of it. Each detector has its dedicated electronics box for supply, signal digitisation and event pre-processing. The bipods (dark blue) are the mechanical interfaces to the instrument platform of the satellite.

regions is realised only by the gate itself. One clear contact on one side serves as reset node. This DEPFET design is used for the MIXS instrument onboard Bepi-Colombo.

# 7.1 Linear Gate Layout

However, the circular gate layout sets limits to its gate dimensions and, thereby, to the achievable spectral performance in combination with high readout speeds [26]. The size of the drain limits the gate width to at least  $40\mu \mathrm{m}$  with the current technology. This sets also constraints on the distance an electron has to drift during the clear process. A long drift distance requires a long clear time. In addition, the contact for the gate needs to be placed directly onto the gate structure, which limits the gate length to a minimum of  $5\mu \mathrm{m}$ . By shifting to a linear gate design, the gate width and length can be further reduced. The design enables the introduction of a contact interface above a clear transistor. Therefore, the gate length is independent of the minimum contact hole size to the metal supply grid. The reduced transistor channel area results in an increased amplification of collected electrons (see Eq. 1) and a lower input capacitance. Both parameters predominately determine the noise of the detector system [26]. As a drawback, two clear contacts have to be used, one at each end of the gate as shown in Fig. 13. Since the clear contacts are regions of poten

---

Norbert Meidinger and Johannes Müller-Seidlitz

![img-12.jpeg](source_images/depfet-active-pixel-sensors-4aec10-fig-13.jpg)
Fig. 13 DEPFET with a linear gate as it is implemented for ATHENA's WFI (see also Fig. 8). The linear gate design allows for narrower gates. Due to the on average shorter distance to the clear, the reset of the internal gate charge is improved. The gate contact interface for the contact hole placed on the side enables shorter gate lengths in addition.

tial charge loss, it may degrade the performance. However, for a back illuminated device the effect should be negligible because signal charge generation next to the clear contact is very unlikely. For such a layout, source and drain have no immanent separation. Therefore, an extended clear gate structure was used for the pixel layout of ATHENA's WFI. This avoids the implementation of additional contacts and ensures a proper charge clearing.

# 7.2 Prevention of Energy Misfits

The best time resolution in the order of a few microseconds can be achieved using a full parallel readout of all pixels simultaneously [21]. This requires a direct coupling of each pixel to a readout channel. With an increasing fraction of the readout time to the total exposure time, the fraction of energy misfits (see subsection 4.1) can rise up to almost  $50\%$  and degrade the spectral performance significantly. The use of a shutter would result in a substantial loss of photons and is thus not the optimum solution. To avoid the occurrence of a large fraction of misfits, the charge collection and the readout regions need to be decoupled by spatial separation. One implementation of such a concept is the so-called Infinipix [2]. Each pixel is subdivided into two sub-pixels as shown in Fig. 14 with a common source contact. The two Internal Gates act as potential minima for electrons either for the charge collection or for the readout. The sub-pixels' functionalities are defined via the drain voltages. The drain of the collecting sub-pixel is as positive as the source contact and thus much more attractive to signal electrons. The drain voltages are switched for all pixels simultaneously and define the beginning of a new frame. Therefore, every sub-pixel is read out only every second frame.

The working principle has been successfully demonstrated [1, 20]. Already for the operation in rolling shutter mode, small Infinipix test matrices of  $32 \times 32$  pixels showed a noticeable increase in the performance. The FWHM at  $5.9\mathrm{keV}$  energy could be improved from  $131.4\mathrm{eV}$  to  $125.6\mathrm{eV}$  by using the Infinipix concept instead of a standard DEPFET. In a three row window mode, the difference is even more

---

DEPFET Active Pixel Sensors

![img-13.jpeg](source_images/depfet-active-pixel-sensors-4aec10-fig-14.jpg)
Fig. 14 DEPFET with two Internal Gates to avoid energy misfits. In the upper figure, sub-pixel B is read out via the common source contact in a frame n. Sub-pixel A is used to collect the incoming electrons in the meanwhile. The sub-pixels' functionalities (readout and collection) are changed after every frame defined by the two switchable drain voltages. Therefore, in the frame  $n + 1$  (lower figure), sub-pixel B collects electrons while sub-pixel A is read out. By switching the global drain voltages, the beginning of a frame is defined for all pixels at the same time. Charge clouds split between two frames can be recombined in a subsequent analysis. In principle, this avoids any charge loss due to the readout process.

![img-14.jpeg](source_images/depfet-active-pixel-sensors-4aec10-fig-15.jpg)

significant. Compared to a standard DEPFET, the FWHM at  $5.9\mathrm{keV}$  energy was enhanced from  $144.4\mathrm{keV}$  to  $131.2\mathrm{keV}$ . The spectral performance of the Infinipix is degraded for the three row window mode measurement because in the preliminary data analysis events split between two frames were not recombined [21]. In near future, a matrix wired to be read out fully parallel will be tested.

# 8 Conclusion

The DEPFET active pixel sensor offers a novel detector concept for future X-ray missions. Meanwhile, the design and technology are so mature to allow for application in a space mission. A first DEPFET detector was launched into space onboard the BepiColombo satellite in 2018. The next application will be the Wide Field Imager of ESA's ATHENA X-ray observatory. The challenging requirements of the ATHENA mission, e.g. high time resolution, led to a further improvement of the DEPFET concept. As a result, an optimal DEPFET transistor design has been developed for ATHENA and large-scale sensors have been manufactured and successfully tested. The DEPFET concept provides a high flexibility to optimise the

---

detector parameters for individual mission objectives like even higher time resolution or scalable pixel sizes from a few tens of microns up to a centimetre.

## References

- (1) Bähr A et al (2014) Development of DEPFET active pixel sensors to improve the spectroscopic response for high time resolution applications, Proc. of SPIE, volume 9144, doi: 10.1117/12.2055411
- (2) Bähr A, Richter R, Schopper F, Treis J (2018) DETECTOR ASSEMBLY AND CORRESPONDING OPERATING METHOD, EP Patent 15001242
- (3) Barbera M et al (2018) ATHENA WFI optical blocking filters development status toward the end of the instrument phase-A, Proc. of SPIE, volume 10699, 373-385, doi: 10.1117/12.2314448
- (4) Bunce EJ et al (2020) The BepiColombo Mercury Imaging X-Ray Spectrometer: Science Goals, Instrument Performance and Operations, Space Sci Rev 216, 126, doi: 10.1007/s11214-020-00750-2
- (5) Eraerds T et al (2021) Enhanced simulations on the Athena/Wide Field Imager instrumental background, Journal of Astronomical Telescopes, Instruments, and Systems, SPIE, 7, 1-22, doi: 10.1117/1.JATIS.7.3.034001
- (6) Fano U (1947) Ionization Yield of Radiations. II. The Fluctuations of the Number of Ions, Phys. Rev., 72:26–29, doi: 10.1103/PhysRev.72.26
- (7) Fischer P et al (2003) Readout concepts for DEPFET pixel arrays, Nucl. Instr. Meth. Phys. Res. A, 512(1):318-325, doi: 10.1016/S0168-9002(03)01909-0
- (8) Gatti E, Rehak P (1984) Semiconductor drift chamber - An application of a novel charge transport scheme, Nucl. Instr. Meth. Phys. Res., 225(3):608-614, doi: 10.1016/0167-5087(84)90113-3
- (9) Grant CE et al (2020) Reducing the Athena WFI charged particle background: results from Geant4 simulations, Proc. of SPIE, 1144442, doi: 10.1117/12.2561124
- (10) Kahng D, Atalla MM (1960) Silicon-Silicon Dioxide Field Induced Surface Devices, IRE-AIEE Solid-state Device Res. Conf.
- (11) Kemmer J, Lutz G (1987) New detector concepts, Nucl. Instr. Meth. Phys. Res. A 253 365, doi: 10.1016/0168-9002(87)90518-3
- (12) Kittel C (2004) Introduction to Solid State Physics, Wiley, 8th edition
- (13) Lowe BG, Sareen RA (2007) A measurement of the electron–hole pair creation energy and the Fano factor in silicon for 5.9 keV X-rays and their temperature dependence in the range 80–270 K, Nucl. Instr. Meth. Phys. Res. A, 576(2–3):367–370, doi: 10.1016/j.nima.2007.03.020
- (14) Lutz G (1999) Semiconductor Radiation Detectors, Springer, 1st edition
- (15) Lutz G (2005) DEPFET development at the MPI semiconductor laboratory, Nucl. Instr. Meth. Phys. Res. A, 549(1):103-111, doi: 10.1016/j.nima.2005.04.034

---

DEPFET Active Pixel Sensors

[16] Majewski P et al (2014) Calibration measurements on the DEPFET Detectors for the MIXS instrument on BepiColombo, Experimental Astronomy, 37:525–538, doi: 10.1007/s10686-014-9374-5
- [17] Meidinger N et al (2014) Wide field imager instrument for the Advanced Telescope for High Energy Astrophysics, Journal of Astronomical Telescopes, Instruments, and Systems, SPIE, 1, 1-8 , doi: 10.1117/1.JATIS.1.1.014006
- [18] Meidinger N et al (2020) Development status of the wide field imager instrument for Athena, Proc. of SPIE, volume 11444, 120-132, doi: 10.1117/12.2560507
- [19] Meidinger N et al (2021) eROSITA camera array on the SRG satellite, Journal of Astronomical Telescopes, Instruments, and Systems, 7, 1-19, doi: 10.1117/1.JATIS.7.2.025004
- [20] Müller-Seidlitz J et al (2018) Performance Study of Spectroscopic DEPFET Arrays with a Pixel-wise Storage Functionality, Journal of Instrumentation, volume 13 (11), doi: 10.1088/1748-0221/13/11/P11018
- [21] Müller-Seidlitz J et al (2018) Spectroscopic DEPFETs at High Frame Rates using Window Mode, Journal of Instrumentation, volume 13 (12), doi: 10.1088/1748-0221/13/12/P12021
- [22] Nandra K et al (2013) The Hot and Energetic Universe - A White paper presenting the science theme motivating the Athena+ mission
- [23] Porro M et al (2010) ASTEROID: A 64 channel ASIC for source follower readout of DEPFET arrays for X-ray astronomy. Nucl. Instr. Meth. Phys. Res. A, 617(1):351–357, doi: 10.1016/j.nima.2009.10.040
- [24] Porro M et al (2014) VERITAS 2.0 a multi-channel readout ASIC suitable for the DEPFET arrays of the WFI for Athena, Proc. of SPIE, volume 9144, doi: 10.1117/12.2056097
- [25] Treberspurg W et al (2018) Measurement results of different options for spectroscopic X-ray DEPFET sensors, Journal of Instrumentation, volume 13 (09), doi: 10.1088/1748-0221/13/09/P09014
- [26] Treberspurg W et al (2018) Achievable noise performance of spectroscopic prototype DEPFET detectors. Journal of Instrumentation, volume 13 (12), doi: 10.1088/1748-0221/13/12/P12001
- [27] Treberspurg W et al (2019) Characterization of a 256$\times$256 pixel DEPFET detector for the WFI of Athena, Nucl. Instr. Meth. Phys. Res. A, 162555, doi: 10.1016/j.nima.2019.162555
- [28] Treis J et al (2010) MIXS on BepiColombo and its DEPFET based focal plane instrumentation, Nucl. Instr. Meth. Phys. Res. A, 624(2):540-547, doi: 10.1016/j.nima.2010.03.173
