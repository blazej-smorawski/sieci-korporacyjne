---
title: "Sieć dla superkomputera"
author: [Aleksanda Hein, Wiktor Kawka, Błażej Smorawski]
date: "11.05.2023"
keywords: [Markdown, Linux]
titlepage: true
titlepage-color: "3C9F53"
titlepage-text-color: "FFFFFF"
titlepage-rule-color: "FFFFFF"
titlepage-rule-height: 2
...

# Warunki początkowe
 1. Dla tego komputera powstanie nowy budynek o powierzchni około 800m2


# Plan budynku
![](plan.svg "Plan budynku")
### Pomieszczenia
 1. Pomieszczenie dla węzłów obliczeniowych
 2. Pomieszczenie dla ochrony
 3. Magazyn
 4. Schowek dla osób dbających o porządek
   
# Sieci
### Sieć Obliczeniowa

Celem sieci obliczeniowej jest dostarczenie szybkiego połączenia pomiędzy wszystkimi węzami obliczeniowymi klastra. Podstawowym medium komunikacyjnym jest **InfiniBand** wykorzystując złącze **QSFP56** z prędkością **HDR**. Każda grupa będzie wyposażona w cztery przełączniki *NVIDIA MQM8790-HS2R Quantum HDR InfiniBand Switch* w rozmiarze 1U wyposażone w 40 portów wyjściowych. 

Urządzenia zostały wybrane ze względu na wykorzystanie w węzłach obliczeniowych akceleratrów firmy NVidia, co umożliwia ścisłą współpracę pomiędzy nimi i wykorzystanie protokołu **SHARP** służącego do wykonywania obliczeń **\`in network\`**. Przykładem jest operacja redukcji buforów między urządeniami, która może zostać wykonana na pierwszym napotkanym przełączniku, co znacznie zmniejsza obciążenie sieci oraz zwalnia zasoby węzłów obliczeniowych.

Przełączniki dodatkowo gwarantują nam nieprzerwaną dostępność i możliwość realizowania napraw w trakcie pracy urządzenia:
 * 1+1 zasilaczez z możliwością **\`hot plug\`**
 * N+1 redundantne wentylatory z możliwością **\`hot plug\`**
 * certyfikowane zasilacze 80 gold+

Cztery przełączniki w grupie 128 węzłów pozostawiają nam 32 wolne porty, które są wykorzystywane do gęstego połączenia grupy z piętnastoma pozostałymi za pomocą dwóch zaagregowanych łącz optycznych.

Potrzebny sprzęt:
 * Przełącznik *NVIDIA MQM8790-HS2R Quantum HDR InfiniBand Switch* x 16 x 4 = **32**
 * Przewody miedziane *Mellanox® MCP1650-H0xxEyy DA* x **2048**
 * Przewody optyczne *Mellanox® MFS1S00-HxxxE* x 30 x 16 = **480**

### Administracyjna
### Bezpieczeństwa
### Dostępowa
   
# Plan adresacji

### Sieć obliczeniowa
    1. ddasdas
   
### Sieć administracyjna
    1. dasdasdsa
