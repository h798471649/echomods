# The EchoModules

## Next steps from [Murgen](http://github.com/kelu124/murgen-dev-kit/) 

1. Playing with the design and fab the modules: 3 to go in CMS (HV/TGC/MD, enveloppe detection, SPI ADC) and 2 in stripboard mode (alim, based on the breadboard 3.3V and 5V, as well as the controler, maybe an arduino nano at first) - and start the github repo / [echOmods](https://hackaday.io/project/10899-echomods) hackaday pages as well. Work on this with Sofian and Vlad. See also the [echOmods repo](https://github.com/kelu124/echomods/).
2. Playing with an electronic emulator of the transducer - as well as an electronic model. Work on this with a partner/supplier.
3. Play with a ultrasound durable fantom. Work on this with **staticdet5** (comment on HAD). Started a [project with Virginie and Static on HAD.io](https://hackaday.io/project/11478-open-source-ultrasound-phantoms).
4. Play with the BeagleBone PRUs. Work on this with Vanderbilt.
5. Playing with some intelligent uC of FPGA. uC has my preference at first for ease of use. WifiMCU seems fun (has a 8$ STM32F411CE - 100MHz, 2.4Msps ADC, FPU, DSP instructions and WiFi to stream!) or the [Feather Wiced](https://www.adafruit.com/product/3056) (arduino IDE compatible, based on a 34$ STM32F205 ARM Cortex M3 processor running at 120MHz. Project codename would be [Croaker](https://github.com/kelu124/echomods/croaker), not created yet. Who's volunteering?

## Brief

Mostly, the thing would be to separate the
[Murgen](http://github.com/kelu124/murgen-dev-kit/) PCB in 4 different
modules (similar to the arduino trinket pro for example), so to have
them ready to be used on a stripboard which would have already headers.

The strips would have the 19 tracks as on the attached picture below.

There would be 2 modules :

-   HV + pulser + md0100
-   TGC + enveloppe + SPI ADC

(Two other modules, Alim, and controler, will be stripboard based)

Given that the boards would be separated, would it make sense to try
to \*\*design the PCBs to have only 2 layers PCB\*\* ? The width of the
PCBs would not really matter, only to be sure they'd fit on a strip
board. It would be interesting to have a form factor of the modules PCB
comparable to one trinket pro =)

### Adjusting the specs for a research module

* 10ms between lines - 64 lines gives 640ms / image)
* 200us at 2Msps is 400 points is 5600 bits is 700 bytes
* 5600 bits per 10ms is 560,000 bits/s is 70kbytes/s.. should be OK with ESP8266 ;)

### Details about the modules

1\. HV+Pulser+MD0100 don't change. The module will need to have a SMA
connector (same as on existing board).

2\. VGA + enveloppe + ADC

* VGA+enveloppe detector can remain the same. I just need to remove the
filter that is between t	he TestPoints4 and 5 and the transformer. The
module output is the output of the ADL5511.
* SPI can be replaced, this one was an overkill. 10Msps is too much, so
instead a 2 or 3 Msps at 12 or 14 bits in SPI could be used on the ADC
module.

### Controls

The "controls" listed would be a potentiometer for the HV (as was done
for murgen), a potentiometer for the TGC Gain (not an ADC, bit of
overkill, rather a jumper to allow one to select the gain from either
the track or a potentiometer which would feed in from 0 to 1V).

### ADC details

The ADC can be as low as 12bits 2Msps when we're talking about envelope
detection (what about MAX11105?). (btw, the signal output by it is
offset by around 1.32V) on top of which we have 1.25V of signal. For the
sake of the experiment, I would add another ADC board, clone of the
11105, with a MAX11103, to comparatively test both.

### The motherboard

What is expected is to break down logic blocks into modules that could be put on a motherboard ( a 2.54mm stripboard), 19 tracks high.

## Todo

### Still to do

* TODO: Mech-athon - Coming soon
* TODO: Module: ESP8266+ADC
* TODO: Design Croaker and Silent
* TODO: Contact Frederic Patat
* TODO: Add status to track progress of the works
* TODO: Jan
* TODO: Imprimer une tof a afficher
* TODO: Contact Edgeflex
* TODO: Schemas de fonctionnement des modules
* TODO: Hack RPi0 CSI (Camera)
* TODO: Voir PCMLab (Jussieu)

### Ongoing

* Ongoing: Document the motherboard -- thanks to Prof Charles
* TODO: Goblin - 2Msps SPI ADC -- Play with BBB and RPi0 SPI

### Done

* Done: schemas a taper, puis processing dans le makedoc.py
* Done: A draft for the analog pulser, [Tobo](/tobo/) -- April 20th 2016
* Done: [Automating Documentation](https://github.com/kelu124/echomods/blob/master/makedoc.py)
* Done: Cahier des charges modules - See __Adjusting the specs for a research module__ on this log
* Done: Silkscreening with the murgen-series logo =)
* Cancelled: Module: Detection (Merged in Goblin)


## Description

Board 1, aka [Tobo](/tobo/Readme.md):

* The HV part of murgen is kept. The pulser of the first board is trigged by Pulse On (stripe 9) and shut by Pulse Off (stripe 10) (coming from the stripes). The pulser alimentation is fed through the RECOM component, with a potentiometer to select the HV level.
* Signal is sent to a sideway SMA connector. 
* Signal is protected by a MD0100 + LC.
* Low voltage signal is sent out of the board through a SMA connector.

Board 2, aka [Goblin](/goblin/Readme.md):

* Low amplitude signal comes from the SMA connector.
* It is fed through to the TGC.
* The Gain of the TGC can come either from the Analog Gain Ramp stripe (stripe 7) or from a potentiometer which gives it 0 to 1V - selection through a jumper.
* The filter part of the murgen board is removed (between TP2/3 and TP5/6)
* Raw signal is either send to stripe 3 or sent to the ADL5511, selection through a jumper.
* If output of the TGC goes to the ADL5511, it is then sent to the stripe 5 or to the 2/3Msps ADC (SPI).

Two other modules are being worked on, namely:

* controler
* alimentation


Worklog -- Starting April 5th 2016
-------

#### 2016-04-05 Captech

* Validation of the approach by the Captech

#### 2016-04-08 Tracks of interest

* Validation of tracks of interest

#### 2016-04-15 Tracks

* Validation of tracks and their orders
* Alexandr

#### 2016-04-16 uC

* Studying microcontrolers... See  [microcontrollers](notes_uC.md)

#### 2016-04-17 PCB

* Getting a first design for the pulser module
 
![A PCB for PCB](https://raw.githubusercontent.com/kelu124/echomods/master/tobo/viewme.png)

#### 2016-04-18 ADL5511

* Playing a bit with ADL5511 : there's an EREF 
* We use offset remover (suiveur + gain de 2.5), and second op will do amplification, cause envelope output swing is saturated at 1.2-1.3V, We can use 2..2,5 gain to deliver nice and neat 2,6 ..3V input swing for ADC. 

#### 2016-04-20 Modules

##### Previous Generation

* [Murgen](http://github.com/murgen-dev-kit/) : the annalist.. already done, a former project !

##### Current batch

* [Goblin](/goblin/Readme.md): the analog heart, was drafted as well during Murgen. 
* [Tobo](/tobo/Readme.md): the HV/pulser, based on a drafted close to Murgen. 
* [One-Eye](/oneeye/Readme.md): MicroControler - Arduinos
* [Mogaba](/mogaba/Readme.md): Alimentation

Second generation of fun! Learning microcontrolers and advanced simulations

* Croaker: M3/M4 microcontroler 
* Silent : physical emulateur

#### 2016-04-23 Servos

* A stepper based on a servo : https://hackaday.io/project/11224-mechaduino (pour @bivi)

#### 2016-04-24 Maintainers

* Starting to document [Tobo](/tobo/Readme.md)
* Reading __"Maintaining Open Source Projects"__ by Tute Costa : _A project maintainer should feel comfortable shaping the community, promoting the library, keeping good communication with different people, deciding when to release new versions, and prioritizing all these tasks._
* Getting a _TL-MR3040 TP-Link_ for a project PirateBox (an __echObox__ ?)
* __2016 strategy__ being done

#### 2016-04-25 Working IRL and motivation

* http://bengarvey.com/2016/04/24/real-work/ _How many times today did a customer notice something you did?_
* http://www.stubbornella.org/content/2013/02/26/why-i-run-my-business-like-an-open-source-project/
* http://www.atlasobscura.com/articles/the-rise-of-illegal-pirate-libraries?utm_source=facebook.com&utm_medium=atlas-page

_I define Real Work as_

* Work that creates an immediate and positive change in your product/service
* Work that is a direct constraint to the completion of A
* Work you have been uniquely hired to do.

#### 2016-04-26 Motivation

_"I am not a visionary, I'm an engineer," Torvalds says. "I'm perfectly happy with all the people who are walking around and just staring at the clouds ... but I'm looking at the ground, and I want to fix the pothole that's right in front of me before I fall in."_

* http://gggritso.com/human-git-aliases
* http://neo4j.com/blog/technical-documentation-graph/

#### 2016-04-27 Documenting

* Meetings (virginie)
* Doc of modules : https://github.com/kelu124/echomods/
* Preparation of Testing tools for the doc 
* Materials : some awesome resources : Il existe des tables sur les plastiques (http://www.ondacorp.com/images/Plastics.pdf) et autres caoutchoucs (http://www.ondacorp.com/images/Rubbers.pdf ) mais rien de concluant (ref, eau a 1.5MRayl). Il y a des choses comme le Polyurethane, RP-6400, a voir.
* Documentation echomods 
* Premier module OK : (HV, + pulser) sources publiees (same github), fab-ready, quasi documente
* Deuxieme module OK : (TGC, Enveloppe, ADC) sources publiees (same github), fab-ready, documentation en cours

#### 2016-04-30 MBTI and DDS

* Am an INTJ-A ... so what?
* R-2R DDS -- =) MHz DDS with arduino ?
* http://www.tek.com/blog/tutorial-digital-analog-conversion-%E2%80%93-r-2r-dac
* https://hackaday.io/project/9469-misc-arm-projects/log/31489-quick-dirty-dds-for-around-1

#### 2016-04-29 Some stuff

Fun to read

* NT: [The evolutionary argument against reality](https://www.quantamagazine.org/20160421-the-evolutionary-argument-against-reality/).
* [Beard things...](http://www.smbc-comics.com/comics/1461854994-20160428.png)
* Autodocumenting with [makedoc.py](https://github.com/kelu124/echomods/blob/master/makedoc.py) - which updates the [Readme.md](/Readme.md) automatically.

#### 2016-04-30 Graphs

* Adding graphs for all modules with [makedoc.py](https://github.com/kelu124/echomods/blob/master/makedoc.py).
* TODO: https://www.coursera.org/course/fin4devmooc
* TODO: https://www.coursera.org/course/effectiveppp
* TODO: https://www.coursera.org/course/healthcareinnovation

##### 2016-05-01 A bit of work

* Done: TOBO and GOBLIN
* Done: Autodocumentation
* Comment gerer les transducers de Jan?
* Projet Fantomes commence sur HAD : phantoms are starting to appear on [Hackaday](https://hackaday.io/project/11478-open-source-ultrasound-phantoms)

* http://electronics.stackexchange.com/questions/50577/what-ultrasonic-sensoremitter-should-i-use-for-my-medical-ultrasound-project
* http://electronics.stackexchange.com/questions/129582/what-is-the-current-consumed-by-ultrasonic-sensors-transducers-1-2mhz-to-gener?rq=1 for power use

#### 2016-05-02 What

* http://uk.businessinsider.com/interview-with-estonia-cio-taavi-kotka-2016-4


#### 2016-05-03 Max Hold Reset

* http://hackaday.com/2016/04/29/saving-lives-with-open-source-electrocardiography/
__Max-Hold-Reset__
* https://fr.wikipedia.org/wiki/Circuit_d%C3%A9tecteur_d%27enveloppe -> Schema a amplificateur operationnel  (peak detector)
* http://electronics.stackexchange.com/questions/112347/how-to-make-a-peak-detector-circuit
ou peut etre encore mieux :
* http://www.planetanalog.com/author.asp?section_id=396&doc_id=562072
* __Got it !!__ http://www.falstad.com/circuit/e-peak-detect.html
* ESP8266: exploration: SPI-ADC+ESP.overclocked ? : http://stackoverflow.com/questions/37014547/esp8266-and-high-speed-external-adc

#### 2016-05-04 May the fourth

* http://stackoverflow.com/questions/13447538/how-to-avoid-overlapping-nodes-in-graphviz
* http://stackoverflow.com/questions/3967600/how-to-prevent-edges-in-graphviz-to-overlap-each-other

* http://circuit-diagram.hqew.net/Peak-detect-and-hold_17262.html
* http://www.tradeofic.com/Circuit/4885-POSITIVE_PEAK_DETECTOR.html
* PKD01 : trop lent

#### 2016-05-07 Websocket

* https://forum.pjrc.com/threads/34095-Teensy-3-2-ESP8266-12Q-High-Speed-ADC-Websocket

#### 2016-05-10 KiCAD

* https://contextualelectronics.com/gtb-kicad-4-0/ :  10 Part Tutorial On Designing/Building A PCB (Using FOSS)

#### 2016-05-14 Work in Indonesia

* Off to Jakarta =)
* Next prios : Feather and [ESP8266](notes_ESP8266.md)

#### 2016-05-23 Transducers

* Restarting work with transducer and boards makers, Jan and Jerome

#### 2016-05-24 RPi

* Bass inspiration : https://www.youtube.com/watch?v=6ZDTelKz4G0
* Working on [Raspberry Pi Zero notes](notes_RPi0.md)
* Updated existing notes on [microcontrollers](notes_uC.md) and the [ESP8266](notes_ESP8266.md)
* Thinking about video / photos port to raspberry (even better than USB transfer, it manages quite high speed ( The two data lanes on the CSI-2 bus provide a theoretical 2 Gbps bandwidth, which approximates to around 5 MP resolution.  ) [here](http://www.petervis.com/Raspberry_PI/Raspberry_Pi_CSI/Raspberry_Pi_CSI_Camera_Module.html)

#### 2016-05-25 Markdown and downs

* http://stackoverflow.com/questions/4823468/comments-in-markdown
* Article on Projects http://teambit.io/blog/all-your-teammates-will-be-gone/
* www.theatlantic.com/health/archive/2014/06/the-dark-knight-of-the-souls/372766/
* http://www.certwise.com/blog/31-ways-know-project-doomed/
* http://gettingreal.37signals.com/toc.php

#### 2016-05-27 Partenariats

* Exploring the partnerships with J&J

#### 2016-05-30 ESP and such

* http://www.esp8266.com/viewtopic.php?t=669&p=3624 HPSI on ESP8266
* Nicolas from V.
* Lancement des PCBs (Jerome)
* Go for Piezos (Jan)

#### 2016-05-31 hackaday fun

* Redirection de visiteurs de Hackaday vers nos ressources
* Reflexion sur l'EMW3165 -- 8$, ADC à 2.4Msps, WiFi.
* Extraction de la connaissance à partir du BC3: petit souci, le contenu BC3 ne semble pas exportable (pas de dump possible comme avec BC2), et n'a pas d'API d'integration.
* Petit truc sympa, mais pas encore sorti : un SoC pour le RPi : https://hackaday.io/project/11981-rppsoc-system-on-a-chip-for-the-raspberry-pi
* Pas possible de créeer le Wall of Contributors, tjrs ce probleme de reset de mot de passe, aucun email n'arrive.
* TODO: réorganiser les Readme entre echomods et medicotechnical et leur prod automatisée =) 
* [EMW3165](notes_EMW3165.md) : "All I see is an under 8 USD STM32F411CE dev board with some wifi gadget" ( http://www.emw3165.com/ ) 

#### 2016-06-02 Some awesome OSH for medical issues

An endoscope pill

* https://hackaday.io/project/10845-tiny-wireless-capsule-camera
* https://github.com/friarbayliff/PillEndoscope

What about XRays?

* http://hackaday.com/2016/05/12/to-see-within-making-medical-x-rays/#more-204360
* https://hackaday.io/project/4740-100-xray-desktop-ct-scanner

And CT Scanners?

* http://hackaday.com/2013/10/23/towards-a-low-cost-desktop-ct-scanner/
* https://hackaday.io/project/5946-openct
* http://www.tricorderproject.org/blog/tag/openct/
* https://github.com/tricorderproject/openct

and MRI ?

* https://hackaday.io/project/5030-low-field-mri

and *CG ?

* See http://mobilecg.hu/
* http://hackaday.com/2016/04/29/saving-lives-with-open-source-electrocardiography/
* http://hackaday.com/2016/03/13/ekg-business-card-warms-our-hearts/


#### 2016-06-04 Learning more on STM32

* [Note d'application des timers par STM](http://www.st.com/web/en/resource/technical/document/application_note/DM00042534.pdf)
* Un très gros bon post sur les timers : un mois de travail d'après l'auteur - [post de blog](http://embedded-lab.com/blog/stm32-timers/)
* Et son [petit frère sur les ADC](http://embedded-lab.com/blog/stm32-digital-analogue-converter-dac/)
* Getting comments on scan conversion at [HAD](https://hackaday.io/project/9281-murgen/log/39271-ultrasound-and-scan-conversion/discussion-58228)


#### 2016-06-06 Weekly monday

* Weekly meeting at the HD
* Prof Charles and Zach start playing with Murgen, so I'm starting to experiment with Jekyll for murgen on the corresponding [Github murgen page](http://kelu124.github.io/murgen-dev-kit/)


#### 2016-06-07 Hall of fame

* Preparing a hall of fame on echopen's wiki
* Getting a copy of an excellent book : [buy here](http://www.lulu.com/shop/st%C3%A9phane-ribas-and-st%C3%A9phane-ubeda-and-patrick-guillaud/logiciels-et-objets-libres-animer-une-communaut%C3%A9-autour-dun-projet-ouvert/paperback/product-22702396.html)
* Reading more about open science hardware with [GOSH](http://openhardware.science/gosh-manifesto/).. and finding a good [OSH journal](http://openhardware.science/2016/05/20/292/) which leads to there : [http://www.journals.elsevier.com/hardwarex](http://www.journals.elsevier.com/hardwarex)
* Awesome DIY approach and techniques for [ultrasound gel](http://journals.plos.org/plosone/article/asset?id=10.1371%2Fjournal.pone.0134332.PDF) -- already republished on HAD


#### 2016-06-08 Zach

* Semifinalist for HACKADAY's challenge !!
* lending a hand to Zack on GitHub et al : https://github.com/ZTaylor39/murgen-dev-kit
* Interrupts on Arduino for the emulator : https://learn.adafruit.com/multi-tasking-the-arduino-part-2/external-interrupts

Some research on DACs:

* DAC0800LCN 8-Bit D to A Converter -- http://www.makertronics.co.uk/images/detailed/5/Ext-2254-010.jpg?t=1437747336
* http://forum.arduino.cc/index.php?topic=179410.0
* http://www.ti.com.cn/cn/lit/ds/symlink/dac0800.pdf
* http://hackaday.com/2011/02/17/your-first-digital-to-analog-converter-build/
* Example : https://labarqui.wordpress.com/2012/07/03/emulador-de-notas/

R2RlLadders

* http://id.motd.org/pivot/entry.php?id=10
* http://www.mouser.fr/Passive-Components/Resistors/Resistor-Networks-Arrays/_/N-e89l?P=1z0sqtq&Keyword=resistor+network&FS=True
* http://store.digilentinc.com/pmodr2r-resistor-ladder-d-a-converter/

#### 2016-06-09 Week end !

And nothing.

#### 2016-06-13 News

* Moving forward with Zach
* Creating a 8 bit R2R resistor ladder

#### 2016-06-14 Super hacks!

* Discussion engaged with [Muth](https://hackaday.io/muth) (et son pi-print) for a thermal printer addon
* This hack of a [eink display](https://davidgf.net/page/41/e-ink-wifi-display) is awesome. Hacking a STM32F103ZE and plugging a ESP8266
* Working on [CSV images library](https://github.com/kelu124/murgen-dev-kit/tree/master/software/examples_csv) for images using the CSV+dict format

#### 2016-06-17 Printing and budgets

* Printing  with the thermal printer: a success with https://learn.adafruit.com/networked-thermal-printer-using-cups-and-raspberry-pi/network-printing
* No news from Zach ?

Shopping à faire: 1000$ = 840€

* RPi0 : 42€
* Lulu - book on opensource projects : 17€
* Work on EMW3165: 230€
* Transducteur : 150€
* Matos en rab EdgeF: (125€)*3/4
* Deux modules echomods : 110+140 (-125/4)€
* Reste: 101€ for contigencies + SMA cables + matos (bois)

#### 2016-06-18

* Awesome [CapMED](https://docs.google.com/document/d/1GOPfu91g4AG9QSKEKXoJd4JmZWLB6M4NtTwfT9k_dX4/edit)
* Retroengineering [a 10PV probe](https://github.com/kelu124/echomods/tree/master/retro10PV).. only 10PV? Ain't much.
* Drinking beer
* Admiring an [IA work at recontructing blade runner](https://medium.com/@Terrybroad/autoencoding-blade-runner-88941213abbe#.tn5whktwl)

#### 2016-06-19 Hmm 

* Followup with Zach
* Ping Michael T
* Ping Edgeflex: quid microcircuits

Beaglebone black : Max SPI 32MHz
* http://fr.mathworks.com/help/supportpkg/beagleboneio/ug/use-the-beaglebone-black-spi-interface-to-connect-to-a-device.html?requestedDomain=www.mathworks.com
* http://beaglebone.cameon.net/home/reading-the-analog-inputs-adc
* Comment faire un DAC à 1MHz http://www.mikrocontroller.net/attachment/147272/Figure_8_Datenblatt_DAC0800.png

Available probes, one of which being a 10PV:

* http://www.ebay.fr/itm/ATL-Access-10PV-5-7-5-10-MHz-Multi-Frequency-Transducer-3337-/291685156080?hash=item43e9ca44f0:m:md6YQd3EstKy9--Am0X2fdg
* http://www.ebay.fr/itm/ATL-A6-3mhz-Ultrasound-Transducer-Probe-/282069422915?hash=item41aca5d343:g:F6wAAOSw~bFWKk9O

#### 2016-06-21 Financing

* http://www.fse.gouv.fr/archives/article/associations
* http://www.centre-francais-fondations.org/ressources-pratiques/solliciter-le-soutien-dun-fonds-ou-dune-fondation
* http://www.centre-francais-fondations.org/fondations-fonds-de-dotation/annuaire/annuaires-1
* http://www.centre-francais-fondations.org/annuaire-des-fondations/5172
* https://www.vivalto-sante.com/recherche-et-innovation/recherche-clinique/

* http://stackoverflow.com/questions/19950648/how-to-write-lists-inside-a-markdown-table
* https://blog.bolt.io/demystifying-hardware-jargon-9d7a0cda9b55#.wbophjmdk

#### 2016-06-22 Slides, and VDB

* Resources sympas : http://bafflednerd.com/learn-python-online/
* http://pandoc.org/README.html#producing-slide-shows-with-pandoc


#### 2016-06-24 Mechathon

* Working at the mechaton at the CRI
* Playing with Zach's acquisition and testing his filters
* Processing!
* Old.. mais retrouvé: https://web.archive.org/web/20151204121552/http://www.ncl.ac.uk/eee/research/groups/coms2ip/ultrasound-imaging.htm


#### 2016-06-27 Nothing new

* Discussion with NF@V -- interesting. Could be partnering for some cool ideas. Vets, hackers. Maybe soon for docs.
* Has contacts with electronics experts
* Tests of transducers by Jerome

Some ideas on RPi and SPI:

* https://www.raspberrypi.org/documentation/hardware/raspberrypi/spi/README.md
* https://www.raspberrypi.org/forums/viewtopic.php?f=44&t=130616
* https://www.raspberrypi.org/forums/viewtopic.php?f=107&t=132494
* https://www.raspberrypi.org/forums/viewtopic.php?f=44&t=43442&p=347073
* http://richardhayler.blogspot.fr/2016/02/getting-started-with-esp8266-iot-phat.html

#### 2016-06-30 Recycler un minitel

Pour recycler un Minitel, ca se passe la
* http://pila.fr/wordpress/?p=361
* https://x0r.fr/blog/5


#### 2016-06-30 New probes et al

Deux sondes d'occasions assez sympa pour démontage et analyse (mécanique / materiaux / piezos):

* http://www.ebay.com/itm/Philips-ATL-Access-A-3Mhz-Ultrasound-Scanhead-Transducer-Probe-/262496926313?hash=item3d1e093a69:g:psAAAOSwcL5XMe0n (50$)
* http://www.ebay.com/itm/Hitachi-Ultrasound-Probe-EZU-PM3-/400943782280?hash=item5d5a1c9988:g:cdAAAOSwyQtVga8m (30$)

IA and US:

* http://sci-hub.cc/10.1109/TBCAS.2015.2431272

#### 2016-07-01 Meeting with Nicolas

* Terribly instructive. Lots to learn.

#### 2016-07-02 Strategy

* Just doing it!
* Key learning: will be having fun soon =)


#### 2016-07-03 Playing with a trifrequency probe

* Won the probe http://www.ebay.com/itm/Philips-ATL-Access-A-3Mhz-Ultrasound-Scanhead-Transducer-Probe-/262496926313?hash=item3d1e093a69:g:psAAAOSwcL5XMe0n (50$) -- that's a purely 3MHz probe, should be OK and we won't get too many issues with too high frequencies
* Played with the ATL10PV at [https://github.com/kelu124/murgen-dev-kit/blob/master/worklog/Session_9_ATL.md](https://github.com/kelu124/murgen-dev-kit/blob/master/worklog/Session_9_ATL.md). Not good results, high frequency elements are buggy.
* Any impact of the polarity of the pulse?? 
* TODO: Compare the polarity by switching polarity.

#### 2016-07-04 Meeting

* Long one, instructive.
*BBB : https://groups.google.com/forum/#!topic/beagleboard/3AFiCNtxGis and https://www.element14.com/community/external-link.jspa?url=http%3A%2F%2Fhipstercircuits.com%2Fbeaglebone-pru-ddr-memory-access-the-right-way%2F
* Digging into https://developer.mbed.org/platforms/LPC1114FN28/:  a DIP M0

#### 2016-07-05 RTL-SDR

* Bivi's playing with RTL-SDR.. a simple short and one can get to the 0-30MHz, without any upverter. Fun. To explore.

#### 2016-07-06 Making progress with EMW3165

* With the help of Igor, preparing a UDP server of EMW3165 and getting a throughput of 9Mbit/s on average.
* Getting one of the modules
* Requesting Nicolas' help on getting HV7360LA (fab's suppliers are lost)
* Thinking of the overall structure of the maker kit. I need a wooden box and an aquarium (plexiglass, glue = solvent cement)
* Review of the HAD budget (probe, transducer, fab, et al?). Some euros may be saved.


uControllers and other stuff
-------


### Croaker

#### Case of Feather WICED
 
* 12 bits ADC
* 150 us acquisition, single channel
* 6 Msps interleaved mode

In 150 us you will get 6x12x150 = 10800 bits of data. On Wi-Fi speed 54Mb/s it will take 10800/54000000=0.0002s (200us) to send these data.

In practice, we rather see 8Mbit/s, thats 1.2ms to send it. E

#### Case of ESP8266

Lower specs (for dev kit - 1 to 2 image / s OK)

* SPI is 40MHz
* 14 bit
* 2 Msps
* Comm through SPI
* 10ms between lines - 64 lines gives 640ms / image)
* 200us at 2Msps is 400 points is 5600 bits is 700 bytes
* 5600 bits per 10ms is 560,000 bits/s is 70kbytes/s.. should be OK with ESP8266/EMW3165/equivalent ;)

__More [ESP8266 notes](notes_ESP8266.md)__

#### Case of Rasberry Zero

__More [Raspberry Pi Zero notes](notes_RPi0.md)__

### Tofs

![Cartes](/include/images/600px-Cartes.png)


![Motherboard](/include/images/600px-Motherboard.png)

### Graphing

![mindmap](/include/GraphMyMind.png)

#### April 29th -- initial fill in

* HAD->Murgen
* HAD->AutoFinancement->OpenSourceHardwareContest
* Sofian->Murgen
* Serveur Matthieu->Output Image->Benchmark->Image processing->Jean-Francois
* Image processing->Output Image->Print
* Modules->Tester
* Modules->Transducer
* Mech->BiVi
* echOmods->WoodBox->Arthur
* WoodBox->LogoLaserCut
* Transducer->Jan->2 types to test
* Croaker->STM32F205RG->STM32F205RG->M3
* STM32F205RG->6Msps
* uC->Croaker->TFT Screen
* Croaker->SD Card
* uC->Vlad
* Modules->Alim->Mogaba
* Modules->echOmods
* Modules->HV
* Modules
* Modules->TGC
* Modules->Controler
* uC->Feather Wiced
* uC->Wifi
* uC->EspruinoPico->BiVi
* HAD->Phantoms
* Phantoms->Virginie->HAD
* Phantoms->Static->HAD
* Phantoms->Materials->RP-6400->Latex->Virginie
* Modules->Doc
* Modules->Motherboard
* Documentation->DocBuilder->BiVi
* Documentation->GitAliases
* Documentation->MakeDoc
* Documentation->CreateSchemaBlock->GraphViz
* Wifi->Format->TCP
* Modules->DDS->R-2R
* AG->Strat->AutoFinancement
* Modules->Fab->MacroFab
* Vlad->MacroFab
* DDS->Arduino
* Acquisition->PRU->Vanderbilt->EdgeFlex
* FlyLabs->EdgeFlex
* PRU->Up to 10Msps+
* Acquisition->RedPitaya
* Pedagogie->Aforp->Tao
* Pedagogie->ESIA
* Pedagogie->ENSCachan
* Pedagogie->Isep->Frederic
* Pedagogie->ENS->MichelB
* MichelB->Modules
* Aforp->Apprenti
* Pedagogie->Vanderbilt

#### April 30th

* EdgeFlex->Fab
* ENSCachan->Satie->Constant->Transducer
* Fabs->AutoFinancement

#### April 30th

* Inspiration->MakerFaireParis
* AutoFinancement->Fiverr
* ENS->MichelB

#### May 3rd

* Wifi->ESP8266->ESP32
* ESP8266->ADCSPI->Send
* Wifi->Igor
* Acquisition->Enveloppe->max-hold-reset
* max-hold-reset
* BiVi->LPC810->NE555 du 21eme

#### May 7th

* ADCSPI->Feather Wiced
* ESP8266->Comm2RPi0->RPi0

#### May 24th

* Igor->ESP8266
* RPi0->Oscillo->CA3306
* RPi0->CSI->Camera->ToHack->Hack RPi0 CSI (Camera)
* Igor->Feather Wiced

#### May 25th

* Mech->Mech-athon
* Format->UDP->Broadcast
* Enveloppe->ADL5511

#### May 29th

* ESP8266->ESP8266.ADC->HSPI
* ESP8266.ACD->AD7274

#### May 30th

* Edgeflex->Modules Ready->PiZero->Modules SPI
* Modules Ready->BBB->Modules SPI
* ESP8266->Modules SPI
* ESP8266->Igor->Code
* Igor->PCB
* WICED->KGhosh
* Todo->Comm->An->Nicolas Felix
* Vermon->Nicolas Felix
* Vermon->An
* Comm->Langevinium
* Comm->Tanter
* TODO: Tanter
* TODO: Nicolas Felix
* Comm->P6->V2->FabLab->Voir PCMLab (Jussieu)
* Partenariat->Edgeflex->Revenues
* WICED->Wifi

#### June 7th

* TODO: Hall Of Fame
* Done: DDSTest
* Done: DDSTestWith
* TODO: ProdEdgeFlex
* Sofian->KiCAD->OpenSource
* Virginie->Phantoms
* Murgen->KiCAD
* BlogJanice->OpenSource Gel
* Phantoms->OpenSource Gel->Publis
* OpenSource Gel->Analog Two
* OpenSource->GOSH
* SendMiniCircuits->ProdEdgeFlex->Tests
* ArduinoNano->DDSTest
* DAC->DDSTest->Tests->RPi0

#### June 17th

* Comm->Publication
* Murgen->Caskey->Zach->Todo: Merge all doc
* GitHub->Zach->Caskey
* EMW3165->Igor
* HAD->1000$->Matos
* Comm->AutresBlogs->Andre
* DDSTest->AOP

#### June 18th

* NextSteps->Industralisation->Bitmaker
* Industralisation->Vermon->Nicolas F.
* Industralisation->PRS->Find PRS
* TODO: Find PRS

#### June 27th

* NF@V->Conseil
* NF@V->Mecenat
* NF@V->Experts->TI/MAXIM/ANALOG&Al
* NF@V->Expert Normes
* NF@V->IEEE
* Caskey->IEEE

#### June 30th

* HAD->HAD Followers->Gros->BBB Foundation->Financement
* HAD Followers->Gros->Atmel Corporation
* HAD Followers->Individus->anfractuosity->Chris->zymeter
* HAD Followers->Gros->Texas Instruments
* HAD Followers->Gros->TODO: Démarcher Gros
* TODO: Démarcher Gros
* Caskey->Partenariats->Gros->Experts
* uC->Liste uC
* Zach->PRU
* Caskey->Vanderbilt

