+++
title = "Uitlegbaar Forensische Gezichtsherkenning (EFFR) Gebaseerd op FISWG-kenmerken"
description = ""
weight = 1
date = 2026-05-29
[extra]
tags = ["ROS2", "Gazebo", "python", "C++"]
local_image = "/projects/Explainable Face Recognition/thumbnail.png"
+++

![thumbnail](thumbnail.png)


Je kunt het volledige artikel hier lezen:  [Download PDF (Explainable Forensic Face Recognition based on FISWG Features.pdf)](<Explainable Forensic Face Recognition based on FISWG Features.pdf>)
# Introductie

Ontwikkeling van een Explainable Forensic Face Recognition (EFFR) model; een innovatief biometrisch systeem dat 'uitlegbaar-by-design' is, speciaal ontworpen voor forensisch en juridisch gebruik. In tegenstelling tot traditionele deep learning 'black-box'-systemen, integreert deze architectuur de richtlijnen van de internationale Facial Identification Scientific Working Group (FISWG) om gezichtsgegevens op te splitsen in door mensen verifieerbare kenmerken. Door deep learning te combineren met klassieke computer vision, vertaalt het model complexe kenmerkvergelijkingen naar Likelihood Ratios (LR) om de kracht van statistisch bewijs aan te tonen.

# Projectdetails

- **Kerntechnologie:** Python, OpenCV, NumPy, PyTorch, Scikit-Learn.
- **AI-componenten:** HRNet (High-Resolution Network voor gezichtskenpunten), BiSeNet (Bilateral Segmentation Network), YOLOv11M (Objectdetectie voor gezichtsmarkeringen).
- **Klassieke Computer Vision:** Fourier Shape Descriptors (FSD), Local Binary Patterns (LBP), Gray-Level Co-occurrence Matrix (GLCM), Haralick Features.
- **Machine Learning:** Logistische Regressie, Isolation Forest (Anomaliedetectie), Agglomerative Clustering.
- **Forensisch:** Score-based Likelihood Ratios (SLR).
- **Dataset:** PUT Face Database (10.000 afbeeldingen, 100 personen).

# De Uitdaging

- **De Black-Box:** Geavanceerde gezichtsherkenningsmodellen genereren complexe, hoogdimensionale embeddings die onbegrijpelijk zijn voor jury's en forensisch onderzoekers.
- **Tekortkoming van Post-Hoc Verklaringen:** Reactieve tools zoals Class Activation Mapping (CAM) of LIME produceren eenvoudige heatmaps die wel laten zien _welke_ pixels een model heeft beoordeeld, maar niet verklaren _waarom_ een biometrische beslissing is genomen.
- **Vertaling van Menselijke Linguïstiek naar Kwantitatieve Kenmerken:** Het vertalen van puur kwalitatieve FISWG-beschrijvingen (zoals de vorm van de oorschelp of de curve van wenkbrauwen) naar nauwkeurige, reproduceerbare kwantitatieve datastructuren.

# Belangrijkste Kenmerken

- **Hybride AI/Klassieke Architectuur:** Inzet van deep learning (HRNet & BiSeNet) voor uiterst nauwkeurige semantische segmentatie en het detecteren van gezichtskenpunten. Deze output op pixel-niveau wordt vervolgens doorgegeven aan deterministische klassieke computer vision-pipelines.
- **Anatomische Kenmerkextractie:**
    - **Oren:** Het oorgebied werd geïsoleerd via gezichtsparsing, waarna specifieke punten werden gedetecteerd om de curve wiskundig in kaart te brengen met behulp van tweedegraadspolynoom en RMS-hoekovergangen.
    - **Wenkbrauwen:** Wenkbrauwen werden opgedeeld in 4 kwadranten, waarna een uniform rotatie-invariant LBP-histogram werd ingezet om onderscheid te maken tussen randen/hoeken (die individuele haren vertegenwoordigen) en vlakke delen (huid) om zo de dichtheidsverdeling te bepalen.
    - **Mond & Lippen:** Fourier Shape Descriptors werden toegepast op 4 contouren om de lipvorm vast te leggen.
    - **Huid:** Valide huiddelen werden geïsoleerd via erosie, waarna 50 willekeurige segmenten werden gekozen om microtexturen te evalueren via multi-radius LBP- en GLCM-matrices.
- **Gezichtsmarkeringen Volgen (YOLOv11M):** Een middelzwaar objectdetectiemodel werd getraind op hoge-resolutiebeelden ($1280 \times 1280$ pixels) om onregelmatigheden zoals moedervlekken of sproeten te detecteren. Er is gebruikgemaakt van Perspective-n-Point poseberekening (solvePnP) om 2D-beeldcoördinaten te projecteren op een 3D-cilindrisch hoofdmodel om ruimtelijke afstanden te monitoren.
- **Hiërarchische Statistische Fusie:** Ruwe vergelijkingskenmerken werden gestandaardiseerd via een Yeo-Johnson-machtstransformatie. Vervolgens werd een logistisch regressiemodel getraind op deze genormaliseerde invoer om de kenmerken samen te voegen tot eenheden van een hoger niveau.
- **Vermenigvuldigde Likelihood Ratios:** Scores werden omgezet in forensische Likelihood Ratios op basis van de match/non-match-dichtheden binnen de gehele dataset om tot een definitieve verificatiescore te komen.

# Resultaten

![results](25.png)

- **Prestaties:** Er werd een Equal Error Rate (EER) van 3,0% behaald (en 4,2% in bredere, niet-gecontroleerde omgevingen). Hiermee presteerde het model beter dan oudere deep learning-modellen zoals OpenFace (19,36% EER) en DeepID (16,08% EER).
- **Forensische Rapportage-Engine:** Bouw van een volledig transparante rapportgenerator die de machinale logica interpreteerbaar maakt voor een rechter.