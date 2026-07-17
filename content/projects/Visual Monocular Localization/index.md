+++
title = "Visuele Monoculaire Lokalisatie met behulp van een Kaart en Rijstrooklijnen"
description = "Self Driving Challenge"
weight = 1
date = 2025-06-10
[extra]

local_image = "/projects/Visual Monocular Localization/SDC.jpeg"
tags = ["opencv", "python"]
mathjax = true
+++

<p align="center">
  <img src="SDC.jpeg" width="80%" alt="Visual Odometry Keypoint Matching"/>
  <br>
</p>

Je kunt het volledige artikel hier lezen: [Download PDF (Self Driving Challenge Article Thimo Veldema.pdf)](<Self Driving Challenge Article Thimo Veldema.pdf>)
# Introductie

Voor de jaarlijkse Dutch RDW (Rijksdienst voor het Wegverkeer) Self Driving Challenge is een realtime monoculair lokalisatiesysteem ontwikkeld en ingezet op een autonoom voertuig dat over een gesloten testcircuit navigeerde. Door uitsluitend gebruik te maken van een enkele, naar voren gerichte camera, slaagde het systeem erin om de positie en oriëntatie van het voertuig op de baan te schatten. Dit werd bereikt door visuele bewegingsregistratie (odometrie) te combineren met realtime rijstrookdetectie, waarmee het pad van het voertuig continu werd gecorrigeerd aan de hand van een vooraf gedefinieerde kaart.

# Uitdagingen

- **Hardware- & sensorbeperkingen:** Traditionele lokalisatiesensoren zoals IMU's (Inertial Measurement Units) en wielomwentelingssensoren waren volledig onbeschikbaar. Dit betekende dat het voertuig puur op basis van videobeelden moest navigeren.
- **Cumulatieve drift:** Pure visuele registratie (odometrie) bouwt naverloop van tijd van nature kleine rekenfouten op, waardoor de geschatte positie van het voertuig aanzienlijk van de koers afwijkt.
- **Strikte rekenbeperkingen:** De hardware van het voertuig had een zeer beperkte rekenkracht, wat vroeg om lichtgewicht algoritmen die in realtime konden draaien.

# Belangrijkste functionaliteiten

- **Realtime Bird's-Eye View (BEV):** Transformeerde de beelden van de naar voren gerichte camera naar een bovenaanzicht (perspectief van bovenaf) om wegmarkeringen nauwkeurig in kaart te brengen en te matchen.
- **Lichtgewicht rijstrooksegmentatie:** Ontwikkelde een pipeline met HSV-kleurfiltering en Gaussian blur om de rijstrookmarkeringen op de weg te isoleren.


<p align="center">
  <img src="3.png" width="48%" alt="Original Camera Input"/>
  <img src="4.png" width="48%" alt="Lane Line Mask"/>
  <br>
  <em>Figuur 1: Ruwe camera-input (links) en het resulterende binaire rijstrookmasker met hoog contrast (rechts).</em>
</p>

- **Robuuste bewegingsregistratie:** Implementeerde een visuele odometrie-pipeline met STAR-keypointdetectie en ORB-descriptors om de relatieve beweging van het voertuig tussen frames te volgen, waarbij RANSAC werd gebruikt om visuele ruis weg te filteren.

<p align="center">
  <img src="7.png" width="80%" alt="Visual Odometry Keypoint Matching"/>
  <br>
  <em>Figuur 2: Microtextuur-matches op het asfaltoppervlak om de frame-tot-frame verplaatsing te schatten.</em>
</p>

- **Probabilistische lokalisatie (MCL):** Ontwikkelde een deeltjesfilter (_particle filter_) dat gedetecteerde rijstrooklijnen vergelijkt met een referentiekaart, gebruikmakend van gedownscalede HOG-features ($128 \times 64$ pixels) voor realtime matching.
- **Sensorfusie via Kalman-filter:** Fusioneerde de vloeiende, kortetermijn-bewegingsschattingen van de odometrie met de langetermijn-correcties van het deeltjesfilter, wat resulteerde in een stabiele en continue positiebepaling.

<p align="center">
  <img src="12.png" width="100%" alt="Particle Filter Tracking"/>
  <br>
  <em>Figuur 3: Kaartweergave. De groene pijl is de Kalman-gefilterde voertuigpositie, omringd door rode deeltjes die de ruimtelijke waarschijnlijkheidsverdeling vertegenwoordigen.</em>
</p>

# Resultaten

- **Uitlijning:** Behaalde een gemiddelde absolute fout (MAE) in de breedte (zijwaarts) van slechts 7 cm op rechte weggedeelten.
- **Richtingsnauwkeurigheid:** Behield een rotatiefout (MAE) van slechts 0,028 radialen op rechte stukken.
- **Adaptief herstel bij driften:** Navigeerde succesvol door complexe bochten, over voetgangersoversteekplaatsen en stopstrepen. Het systeem bleek robuust genoeg om "onzekere" positieschattingen direct te corrigeren zodra er een herkenbaar baankenmerk in beeld kwam.
- **Modulaire architectuur:** De volledige codebase is modulair opgebouwd, waardoor de rijstrookdetector of de odometriemodules eenvoudig kunnen worden vervangen.