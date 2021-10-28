---
title: "PAMAI : Passive Acoustic Monitoring Using AI"
date: 2021-10-20
description: PAMAI is a project I have been working on for the past two years. By collaborating with Kyoto University's Bio-informatics Laboratory, I became a research Assistant, and have been providing my insight as an Applied Deep Learning researcher. 
menu:
  sidebar:
    name:  Ecology
    identifier: pamai-eco
    weight: 10
    parent: pamai
hero: pipeline2.png
draft: false
---

# Introduction 

*Pteropus dasymallus* or flying foxes (from the *{Pteropus Genus)* is an insular solitary island fruit bat inhabiting the Ryukyu archipelago in Japan and some Taiwanese islands. 
The important and widespread decline of this species, while mostly related to habitat loss and hunting [^1] [^2] [^3] , raises concern about their level of protection. 


Currently, $60\%$ of *Pteropus* for which data are available are listed as **vulnerable**, **endangered** or **critically endangered** on the IUCN (2020) Red List[^4].



Flying fox is a keystone species in tropical forest ecosystems as they provide seed dispersal and pollination services important for forest regeneration, especially in insular ecosystems[^5]. 

Flying foxes disperse seeds by dropping them in the form of fecal pellets. 
Below a certain density population threshold, flying foxes disperse almost no seed.Therefore, it is important to keep the number of flying foxes above the critical threshold necessary to provide ecosystem services. Unexpected food shortages due to typhoons decrease the abundance of flying foxes and subsequently disrupts forest ecology. Additionally, increases in flying fox abundance may cause conflicts with agriculture. Hence the need to asses and control the population of flying foxes, as well as support ecological studies and conservation programs.

Monitoring can be done in two forms[^6] 

**Active** monitoring is used on the field studies, and needs to be conducted on a large scale. It is subject to observational and process uncertainties, and requires a lot of means, both financial and human. Moreover, it is invasive and can disturb the studied individuals. Whereas, *passive* monitoring is stealthy and non invasive. Passive Acoustic Monitoring (PAM) in particular is one of the most promising monitoring approaches. Although PAM is widely used to study microbats, it has not been used for flying foxes. PAM relies on sound recorders placed in wildlife, which provide environment sounds that are analysed. Flying Foxes do not use echolocation, and interact using audible sounds. 

Although an automated detection system is necessary to develop a PAM system for Ryukyu flying foxes, there are no studies or database of vocalizations for this species. Furthermore, studies about the vocalization of *Pteropus* are scarce. 

The main goal consists in creating a 3-step pipeline including the following: 

1. **Audio Segmentation (Audio Event Detection)**:  all bat calls recorded have to be isolated from background noises, natural sounds and other species such as frogs and birds.
2. **Audio Event Classification**: each call can fall in one of the twelve call categories, which provides information on the context of the call, and the interaction.
3.  **Speaker Recognition**: each emitter has to be identified in order to asses the density population and the possible movements, using the previously known location of identification. 

This study was supervised by Christian E. Vincenot, in collaboration with Kyoto University's Biosphere Informatics Laboratory which provided the problematic. 


[^1]: https://doi.org/10.1371/journal.pone.0177748
[^2]: Vincenot CE, Florens FB, Kingston T. Can we protect island flying foxes? Science. 2017 Mar 31;355(6332):1368-1370. doi: 10.1126/science.aam7582. PMID: 28360279.
[^3]:Adelman ZN, Albritton LM, Boris-Lawrie K, Buchmeier MJ, Cannon P, Cho M, DiGiusto D, Donahue JK, Federoff HJ, Hammarskjold ML, Hardison AD, Hearing P, Lee B, Lee DA, Porteus MH, Ross LF, Ross SR, Wooley DP, Zoloth L. Protect NIH's DNA advisory committee. Science. 2018 Oct 26;362(6413):409-410. doi: 10.1126/science.aav2483. PMID: 30361364.
[^4]:https://www.iucnredlist.org/search?taxonomies=119113&searchType=species
[^5]:COX, P.A., ELMQVIST, T., PIERSON, E.D. and RAINEY, W.E. (1991), Flying Foxes as Strong Interactors in South Pacific Island Ecosystems: A Conservation Hypothesis. Conservation Biology, 5: 448-454. https://doi.org/10.1111/j.1523-1739.1991.tb00351.x. Aziz SA, Clements GR, McConkey KR, et al. Pollination by the locally endangered island flying fox (<i>Pteropus hypomelanus</i>) enhances fruit production of the economically important durian (<i>Durio zibethinus</i>). Ecology and Evolution. 2017 Nov;7(21):8670-8684. DOI: 10.1002/ece3.3213. PMID: 29152168; PMCID: PMC5677486.

[^6]:https://doi.org/10.7717/peerj.103 