+++
title = "ROS2 Autonome Waypoint Robot"
description = ""
weight = 1
date = 2021-06-10 
[extra]
tags = ["ROS2", "Gazebo", "python", "C++"]
+++

{{ video(src="video.mp4", autoplay=true) }}

# Introductie

Ontwikkeling van een differentieel aangedreven mobiele robot (twee wielen met een zwenkwiel) die in staat is tot autonome waypoint-navigatie en real-time obstakelvermijding. Dit project overbruggede de kloof tussen virtuele prototyping en fysieke hardware door eerst een simulatie in Gazebo te bouwen en de besturing vervolgens rechtstreeks op een fysieke robot te implementeren.

# Projectdetails

- **Kerntechnologie:** ROS2 (Robot Operating System), Gazebo, Python/C++.
- **Hardware:** Differentieel aangedreven mobiel platform (2 actief aangedreven wielen, 1 passief zwenkwiel), 3x ultrasone afstandssensoren (naar voren gericht).
- **Concepten:** Robotkinematica, state machines, sensorfusie, algoritmen voor obstakelvermijding.

# Belangrijkste kenmerken & acties

- **Virtuele Prototyping (Gazebo):** Ontwierp een 3D-simulatie van de robot in Gazebo, waarbij de fysieke eigenschappen en sensoren werden gesimuleerd om de navigatie te testen.
- **ROS2 Besturingsstack:** Bouwde modulaire ROS2-nodes voor het verwerken van sensorgegevens, het volgen van waypoints en het aansturen van de wielsnelheid (`/cmd_vel`), met gebruik van ROS2-topics en -parameters voor schone communicatie tussen de nodes.
- **Reactieve Obstakelvermijding:** Programmeerde een algoritme dat de drie naar voren gerichte afstandssensoren analyseerde om de koers van de robot dynamisch aan te passen wanneer er obstakels werden gedetecteerd.
- **Waypoint Navigatie State Machine:** Ontwikkelde een coördinatiesysteem dat de afstand en koers naar een doelcoördinaat berekende, waardoor de robot soepel vooruitreed terwijl het traject actief werd aangepast als een obstakel het pad kruiste.