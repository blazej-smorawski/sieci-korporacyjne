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
 1. Dla tego komputera powstanie nowy budynek o powierzchni około 800m2 (20m x 40m).

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

Wybrane zostały przewody firmy NVidia ze względu na:
 * Zgodność z **InfiniBand HDR**
 * Przepływność 200 Gb/s
 * BER lepsze niż 1e-15

Potrzebny sprzęt:
 * Przełącznik *NVIDIA MQM8790-HS2R Quantum HDR InfiniBand Switch* x 16 x 4 = **64**
 * Przewody miedziane *NVIDIA MCP1650-H00AE30 DAC 1m* x **2048**
 * Przewody optyczne *NVIDIA MFS1S00-H015V AOC 15m* x 30 x 16 = **480**

### Administracyjna

Sieć administracyjna jest siecią odseparowaną fizycznie od sieci, która pozwala nam na kontrolowanie pracy klastra bez wpływu na jego parametry obliczeniowe. Ze względu na mniejsze wymagania wydajnościowe będzie to sieć **Ethernetowa**.

Wybraliśmy przełączniki firmy *NVidia* ze względu na bardzo dobre zdolności telemetryczne, niskie opóźnienia i złożone mechanizmy zarządania ruchem. 

Każda grupa będzie wyposażona w cztery 64. portowe ethernetowe przełączniki *NVIDIA MSN4600-CS2F Spectrum-3 100GbE 2U Open Ethernet Switch*. Tak jak wcześniejsze przełączniki są wyposażone w 2 zasilacze i N+1 wymienialnych wentylatorów.

Wybrane przewody to *NVIDIA MCP2M00-A005E26L DAC 5m* oraz
*NVIDIA MCP1650-V001E30 DAC 1M*.

Potrzebny sprzęt:
 * Przełącznik *NVIDIA MSN4600-CS2F Spectrum-3 100GbE 2U Open Ethernet Switch* x 16 x 4 = **64**
 * Przewody miedziane *NVIDIA MCP1650-V001E30 DAC 1m* x **2048**
 * Przewody miedziane *NVIDIA MCP2M00-A005E26L DAC 5m* x 30 x 16 = **480**

### Bezpieczeństwa

Do zadań realizowanych przez sieć bezpieczeństwa należą:
- monitorowanie budynku za pomocą kamer
- kontrola dostępu do budynku, jak i jego poszczególnych pomieszczeń za pomocą kart
- monitorowanie i regulacja temperatury w pomieszczeniu, w którym znajduje się superkomputer
- monitorowanie i powiadamianie o włamaniach do budynku
- wykrywanie i powiadamianie o pożarze w budynku
- wyświetlanie obrazu z kamer i danych z czujników na komputerach pracowników

Potrzebne urządzenia:
- 25 kamer do monitoringu,
- 7 czytników NFC oraz kart dla każdego pracownika budynku,
- 12 czujników temperatury,
- 8 urządzeń chłodzących i 8 urządzeń pobierających ciepło,
- 40 czujników antywłamaniowych,
- 20 czujników dymu.
- 6 podwójnych gniazdek Ethernet

Wybranym medium komunikacyjnym jest kabel Ethernet kategorii 5E. Dokonano takiego wyboru, gdyż medium to zapewnia wystarczającą przepustowość oraz zasięg. 

Potrzebny sprzęt:
- przewody miedziane Ethernet kat.5E -> 3800m
- 6 przełączników *Cisco CBS350-48T-4X-EU Managed 48-port GE*

### Dostępowa

Celem sieci dostępowej jest zapewnienie dostępu z sieci internet do dwóch węzłów obliczeniowych pełniących rolę węzłów dostępowych. Firma telekomunikacyjna dostarcza dostarcza  nam 8 łącz ethernetowych 200Gb. Routery są bezpośrednio połączone dwoma optycznymi przewodami *NVIDIA MFS1S00-H015V AOC 15m* do każdego węzła dostępowego. Taka instalacja pozwala nam na osiągnięcie łącza rzędu 400Gb/s do jednego węzła dostępowego, co może być konieczne ze względu na wielu użytkowników oraz dużą zajętość danych przetwarzanych w takim klastrze.

Router został wybrany ze względu na:
 * Dużą moc obliczeniową - dwa procesory *Intel Xeon scalable processor Platinum*
 * 1+1 redundantne zasilacze klasy 80 Plus platinum

Potrzebny sprzęt:
 * Router *NVIDIA MGA100-HS2 Skyway* x 2
 * Przewody optyczne *NVIDIA MFS1S00-H015V AOC 15m* x 4


# Plan adresacji

### Sieć obliczeniowa
    1. ddasdas
   
### Sieć administracyjna
    1. dasdasdsa


### Sieć bezpieczeństwa

| Sieć                | Podsieć           | Adres            |
|---------------------|-------------------|------------------|
| sieć bezpieczeństwa | monitoring        | 192.168.0.0/27   |
| 192.168.0.0/24      | temperatura       | 192.168.0.32/27  |
|                     | pożar             | 192.168.0.64/27  |
|                     | dostęp i włamania | 192.168.0.128/26 |

### Kosztorys

|                                                     | Liczba | Cena        | Suma          |
| --------------------------------------------------- | ------ | ----------- | ------------- |
| *NVIDIA MQM8790-HS2R Quantum HDR InfiniBand Switch* | 64     | $65,159.00  | $4,170,176.00 |
| *NVIDIA MCP1650-H00AE30 DAC 1m*                     | 2048   | $351.00     | $718,848.00   |
| *NVIDIA MFS1S00-H015V AOC 15m*                      | 484    | $2,282.00   | $1,104,488.00 |
| *NVIDIA MCP2M00-A005E26L DAC 5m*                    | 480    | $222.00     | $106,560.00   |
| *NVIDIA MCP1650-V001E30 DAC 1m*                     | 2048   | $314.00     | $643,072.00   |
| *NVIDIA MGA100-HS2 Skyway*\*                        | 2      | $55,795.00* | $111,590.00   |

\* Cena routera przed przejęciem firmy *Mellanox* przez *NVidia*

Suma: $6,854,734.00
