---
title: Oblicz wyniki testów porównawczych dla maszyn wirtualnych systemu Linux platformy Azure
description: Porównaj wyniki testów porównawczych dla maszyn wirtualnych platformy Azure z systemem Linux.
ms.service: virtual-machines
ms.subservice: sizes
ms.collection: linux
ms.topic: conceptual
ms.date: 04/29/2020
ms.reviewer: davberg
ms.openlocfilehash: ef60bbfe19e10dcd98ca3691e1fdf0d03d07be24
ms.sourcegitcommit: 7edadd4bf8f354abca0b253b3af98836212edd93
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/10/2021
ms.locfileid: "102558665"
---
# <a name="compute-benchmark-scores-for-linux-vms"></a>Oblicz wyniki testów porównawczych dla maszyn wirtualnych z systemem Linux
Poniższe wyniki testu porównawczego przedstawiają wydajność obliczeń w przypadku wysokiej wydajności zestawienia maszyn wirtualnych platformy Azure z systemem Ubuntu. Wyniki testów porównawczych obliczeń są również dostępne dla [maszyn wirtualnych z systemem Windows](../windows/compute-benchmark-scores.md).

## <a name="standard_das_v4"></a>Standard_Das_v4
(12/11/2019 2:28:52 AM PBI 5851281)

|Rozmiar maszyny wirtualnej| Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
|---| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
|Standard_D2as_v4| AMD EPYC 7452 32 — procesor Core | 2 | 1 | 7,8 | 29 726 | 693 | 2,33% | 42 |
|Standard_D4as_v4| AMD EPYC 7452 32 — procesor Core | 4 | 1 | 15,7 | 59 224 | 1 595 | 2,69% | 42 |
|Standard_D8as_v4| AMD EPYC 7452 32 — procesor Core | 8 | 1 | 31,4 | 116 412 | 3 613 | 3,10% | 42 |
|Standard_D16as_v4| AMD EPYC 7452 32 — procesor Core | 16 | 2 | 62,9 | 229 489 | 7 209 | 3,14% | 35 |
|Standard_D32as_v4| AMD EPYC 7452 32 — procesor Core | 32 | 4 | 125,9 | 461 916 | 6 746 | 1,46% | 35 |

## <a name="standard_da_v4"></a>Standard_Da_v4
(12/12/2019 12:01:48 AM PBI 5851281)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standard_D2a_v4 | AMD EPYC 7452 32 — procesor Core | 2 | 1 | 7,8 | 30 023 | 333 | 1,11% | 35 |
| Standard_D4a_v4 | AMD EPYC 7452 32 — procesor Core | 4 | 1 | 15,7 | 59 685 | 1 141 | 1,91% | 77 |
| Standard_D8a_v4 | AMD EPYC 7452 32 — procesor Core | 8 | 1 | 31,4 | 118 346 | 1 130 | 0,95% | 42 |
| Standard_D16a_v4 | AMD EPYC 7452 32 — procesor Core | 16 | 2 | 62,9 | 231 131 | 3 830 | 1,66% | 35 |
| Standard_D32a_v4 | AMD EPYC 7452 32 — procesor Core | 32 | 4 | 125,9 | 457 266 | 10 208 | 2,23% | 35 |
| Standard_D48a_v4 | AMD EPYC 7452 32 — procesor Core | 48 | 6 | 188,9 | 664 078 | 17 241 | 2,60% | 35 |
| Standard_D64a_v4 | AMD EPYC 7452 32 — procesor Core | 64 | 8 | 251,9 | 863 911 | 24 818 | 2,87% | 35 |
| Standard_D96a_v4 | AMD EPYC 7452 32 — procesor Core | 96 | 12 | 377,9 | 1 290 455 | 13 640 | 1,06% | 35 |

## <a name="standard_eas_v4"></a>Standard_Eas_v4
(12/11/2019 2:28:50 AM PBI 5851281)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standard_E2as_v4 | AMD EPYC 7452 32 — procesor Core | 2 | 1 | 15,7 | 29 217 | 654 | 2,24% | 42 |
| Standard_E4as_v4 | AMD EPYC 7452 32 — procesor Core | 4 | 1 | 31,4 | 58 356 | 480 | 0,82% | 42 |
| Standard_E8as_v4 | AMD EPYC 7452 32 — procesor Core | 8 | 1 | 62,9 | 115 943 | 3 526 | 3,04% | 35 |
| Standard_E16as_v4 | AMD EPYC 7452 32 — procesor Core | 16 | 2 | 125,9 | 227 383 | 5 619 | 2,47% | 35 |
| Standard_E32as_v4 | AMD EPYC 7452 32 — procesor Core | 32 | 4 | 251,9 | 454 609 | 12 746 | 2,80% | 35 |
| Standard_E48as_v4 | AMD EPYC 7452 32 — procesor Core | 48 | 6 | 377,9 | 682 769 | 9 257 | 1,36% | 35 |
| Standard_E64as_v4 | AMD EPYC 7452 32 — procesor Core | 64 | 8 | 503,9 | 881 311 | 28 357 | 3,22% | 35 |
| Standard_E96as_v4 | AMD EPYC 7452 32 — procesor Core | 96 | 12 | 661,4 | 1 299 233 | 14 997 | 1,15% | 70 |

##  <a name="standard_ea_v4"></a>Standard_Ea_v4
(12/11/2019 2:29:06 AM PBI 5851281)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standard_E2a_v4 | AMD EPYC 7452 32 — procesor Core | 2 | 1 | 15,7 | 29 561 | 422 | 1,43% | 42 |
| Standard_E4a_v4 | AMD EPYC 7452 32 — procesor Core | 4 | 1 | 31,4 | 58 303 | 1 280 | 2,20% | 42 |
| Standard_E8a_v4 | AMD EPYC 7452 32 — procesor Core | 8 | 1 | 62,9 | 114 650 | 2 726 | 2,38% | 42 |
| Standard_E16a_v4 | AMD EPYC 7452 32 — procesor Core | 16 | 2 | 125,9 | 226 947 | 4 661 | 2,05% | 35 |
| Standard_E32a_v4 | AMD EPYC 7452 32 — procesor Core | 32 | 4 | 251,9 | 453 666 | 10 058 | 2,22% | 42 |
| Standard_E48a_v4 | AMD EPYC 7452 32 — procesor Core | 48 | 6 | 377,9 | 665 200 | 18 714 | 2,81% | 35 |
| Standard_E64a_v4 | AMD EPYC 7452 32 — procesor Core | 64 | 8 | 503,9 | 894 718 | 25 214 | 2,82% | 35 |
| Standard_E96a_v4 | AMD EPYC 7452 32 — procesor Core | 96 | 12 | 661,4 | 1 298 074 | 15 948 | 1,23% | 35 |

## <a name="av2---general-compute"></a>Av2 — ogólne obliczenia
(3/15/2019 12:06:55 AM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standardowa_A1_v2 | Procesor Intel (R) Xeon (R) E5-2660 0 @ 2.20 GHz | 1 | 1 | 1.9 | 6 483 | 120 | 1,85% | 273 |
| Standardowa_A1_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 1 | 1 | 1.9 | 6 059 | 208 | 3,43% | 217 |
| Standardowa_A1_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 1 | 1 | 1.9 | 6 367 | 453 | 7,12% | 217 |
| Standardowa_A2_v2 | Procesor Intel (R) Xeon (R) E5-2660 0 @ 2.20 GHz | 2 | 1 | 3.9 | 13 161 | 194 | 1,48% | 266 |
| Standardowa_A2_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 2 | 1 | 3.9 | 12 067 | 401 | 3,32% | 203 |
| Standardowa_A2_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 2 | 1 | 3.9 | 12 527 | 797 | 6,37% | 238 |
| Standardowa_A2m_v2 | Procesor Intel (R) Xeon (R) E5-2660 0 @ 2.20 GHz | 2 | 1 | 15,7 | 13 167 | 179 | 1,36% | 273 |
| Standardowa_A2m_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 2 | 1 | 15,7 | 12 133 | 336 | 2,77% | 210 |
| Standardowa_A2m_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 2 | 1 | 15,7 | 12 401 | 656 | 5,29% | 224 |
| Standardowa_A4_v2 | Procesor Intel (R) Xeon (R) E5-2660 0 @ 2.20 GHz | 4 | 1 | 7,8 | 26 307 | 231 | 0,88% | 231 |
| Standardowa_A4_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 4 | 1 | 7,8 | 24 552 | 720 | 2,93% | 224 |
| Standardowa_A4_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 4 | 1 | 7,8 | 24 963 | 1 625 | 6,51% | 252 |
| Standardowa_A4m_v2 | Procesor Intel (R) Xeon (R) E5-2660 0 @ 2.20 GHz | 4 | 1 | 31,4 | 26 238 | 292 | 1,11% | 259 |
| Standardowa_A4m_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 4 | 1 | 31,4 | 24 250 | 491 | 2,02% | 189 |
| Standardowa_A4m_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 4 | 1 | 31,4 | 24 725 | 1 553 | 6,28% | 259 |
| Standardowa_A8_v2 | Procesor Intel (R) Xeon (R) E5-2660 0 @ 2.20 GHz | 8 | 1 | 15,7 | 53 237 | 687 | 1,29% | 266 |
| Standardowa_A8_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 8 | 1 | 15,7 | 49 655 | 585 | 1,18% | 147 |
| Standardowa_A8_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 8 | 1 | 15,7 | 49 005 | 2 162 | 4,41% | 294 |
| Standardowa_A8m_v2 | Procesor Intel (R) Xeon (R) E5-2660 0 @ 2.20 GHz | 8 | 2 | 62,9 | 52 627 | 902 | 1,71% | 266 |
| Standardowa_A8m_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 8 | 1 | 62,9 | 49 838 | 633 | 1,27% | 182 |
| Standardowa_A8m_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 8 | 1 | 62,9 | 49 123 | 2 483 | 5,05% | 259 |

> [!NOTE]
> Maszyny wirtualne z serii Av2 można wdrażać na różnych typach sprzętu i procesorach (jak pokazano powyżej). Maszyny wirtualne z serii Av2 mają wydajność procesora CPU i konfiguracje pamięci, które najlepiej pasują do obciążeń poziomu wejścia, takich jak programowanie i testowanie. Rozmiar jest ograniczany w celu zapewnienia stosunkowo spójnej wydajności procesora dla uruchomionego wystąpienia, niezależnie od sprzętu, na którym jest wdrożony. jednak oprogramowanie, które korzysta z konkretnych nowszych optymalizacji procesora, może zobaczyć bardziej znaczące różnice między różnymi typami procesorów.

## <a name="b---burstable"></a>B — do serii
(3/15/2019 12:27:08 AM PBI 3897709) (Zaktualizowano 6/14/2019 7:09:29 AM PBI 4777081)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standard_B1ms | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 1 | 1 | 1.9 | 13 593 | 307 | 2,26% | 28 |
| Standard_B1ms | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 1 | 1 | 1.9 | 14 069 | 495 | 3,52% | 672 |
| Standard_B1s | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 1 | 1 | 0,9 | 13 736 | 211 | 1,54% | 28 |
| Standard_B1s | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 1 | 1 | 0,9 | 13 965 | 457 | 3,27% | 672 |
| Standard_B2ms | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 2 | 1 | 7,8 | 27 361 | 1 110 | 4,06% | 28 |
| Standard_B2ms | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 2 | 1 | 7,8 | 27 432 | 771 | 2,81% | 672 |
| Standard_B2s | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 2 | 1 | 3.9 | 27 488 | 822 | 2,99% | 28 |
| Standard_B2s | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 2 | 1 | 3.9 | 27 548 | 864 | 3,14% | 672 |
| Standard_B4ms | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 4 | 1 | 15,7 | 54 951 | 1 868 | 3,40% | 28 |
| Standard_B4ms | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 4 | 1 | 15,7 | 54 051 | 1 260 | 2,33% | 672 |
| Standard_B8ms | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 8 | 1 | 31,4 | 111 929 | 1 562 | 1,40% | 35 |
| Standard_B8ms | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 8 | 1 | 31,4 | 109 537 | 1 354 | 1,24% | 665 |
| Standard_B12ms | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 12 | 1 | 47,1 | 170 777 | 3 421 | 2,00% | 70 |
| Standard_B12ms | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 12 | 1 | 47,1 | 166 676 | 1 368 | 0,82% | 70 |
| Standard_B16ms | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 16 | 1 | 62,9 | 208 373 | 30 383 | 14,58% | 63 |
| Standard_B16ms | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 16 | 1 | 62,9 | 223 203 | 1 232 | 0,55% | 70 |
| Standard_B20ms | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 20 | 1 | 78,6 | 269 561 | 25 095 | 9,31% | 77 |
| Standard_B20ms | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 20 | 1 | 78,6 | 274 007 | 3 669 | 1,34% | 70 |


> [!NOTE]
> Maszyny wirtualne z serii B są przeznaczone do obciążeń z wymaganymi możliwościami wydajności. Wystąpienia maszyn wirtualnych gromadzą kredyty przy użyciu mniejszej niż jej podstawy. Gdy maszyna wirtualna ma Zakumulowany kredyt, maszyna wirtualna może przekroczyć poziom odniesienia do 100%, aby spełnić krótkie wymagania dotyczące obciążeń procesora. Czas szeregowania zależy od dostępnych kredytów, które są funkcją rozmiaru i czasu maszyn wirtualnych.  
>
> Jest to krótki test, który zwykle kończy się w ramach dostępnych kredytów na korzystanie z serii.  W związku z tym powyższe numery zwykle reprezentują wydajność maszyn wirtualnych, co odzwierciedla znaczenie krótkich, obciążeń (typowych dla serii B) wydajności.

## <a name="dsv3---general-compute--premium-storage"></a>DSv3 — ogólne obliczenia i Premium Storage
(3/12/2019 6:52:03 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standardowa_D2s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 2 | 1 | 7,8 | 20 153 | 838 | 4,16% | 147 |
| Standardowa_D2s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 2 | 1 | 7,8 | 20 903 | 1 324 | 6,33% | 553 |
| Standardowa_D4s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 4 | 1 | 15,7 | 39 502 | 1 257 | 3,18% | 189 |
| Standardowa_D4s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 4 | 1 | 15,7 | 40 547 | 1 935 | 4,77% | 511 |
| Standardowa_D8s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 8 | 1 | 31,4 | 80 191 | 1 054 | 1,31% | 168 |
| Standardowa_D8s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 8 | 1 | 31,4 | 79 884 | 3 073 | 3,85% | 532 |
| Standardowa_D16s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 16 | 1 | 62,9 | 160 319 | 1 213 | 0,76% | 105 |
| Standardowa_D16s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 16 | 1 | 62,9 | 156 325 | 2 176 | 1,39% | 588 |
| Standard_D32s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 32 | 2 | 125,9 | 315 457 | 2 647 | 0,84% | 105 |
| Standard_D32s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 32 | 1 | 125,9 | 312 058 | 1 661 | 0,53% | 595 |
| Standard_D64s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 64 | 2 | 251,9 | 627 378 | 4 447 | 0,71% | 700 |

## <a name="dv3---general-compute"></a>Dv3 — ogólne obliczenia
(3/12/2019 6:54:27 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standardowa_D2_v3 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 2 | 1 | 7,8 | 20 359 | 799 | 3,93% | 154 |
| Standardowa_D2_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 2 | 1 | 7,8 | 20 737 | 1 422 | 6,86% | 546 |
| Standardowa_D4_v3 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 4 | 1 | 15,7 | 40 095 | 1 501 | 3,74% | 147 |
| Standardowa_D4_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 4 | 1 | 15,7 | 41 147 | 2 706 | 6,58% | 546 |
| Standardowa_D8_v3 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 8 | 1 | 31,4 | 80 383 | 1 486 | 1,85% | 133 |
| Standardowa_D8_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 8 | 1 | 31,4 | 80 511 | 3 916 | 4,86% | 560 |
| Standardowa_D16_v3 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 16 | 1 | 62,9 | 160 932 | 2200 | 1,37% | 140 |
| Standardowa_D16_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 16 | 1 | 62,9 | 158 679 | 4 550 | 2,87% | 560 |
| Standard_D32_v3 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 32 | 2 | 125,9 | 314 208 | 4 250 | 1,35% | 189 |
| Standard_D32_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 32 | 1 | 125,9 | 312 472 | 3 173 | 1,02% | 511 |
| Standard_D64_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 64 | 2 | 251,9 | 627 470 | 9 651 | 1,54% | 700 |

## <a name="dsv2---storage-optimized"></a>DSv2 — zoptymalizowane pod kątem magazynu
(3/15/2019 12:53:13 AM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standardowa_DS1_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 1 | 1 | 3.4 | 14 642 | 600 | 4,10% | 259 |
| Standardowa_DS1_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 1 | 1 | 3.4 | 14 808 | 904 | 6,10% | 434 |
| Standard_DS2_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 2 | 1 | 6.8 | 28 654 | 877 | 3,06% | 301 |
| Standard_DS2_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 2 | 1 | 6.8 | 29 089 | 1 421 | 4,89% | 406 |
| Standardowa_DS3_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 4 | 1 | 13,7 | 57 255 | 1 633 | 2,85% | 238 |
| Standardowa_DS3_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 4 | 1 | 13,7 | 57 255 | 2 265 | 3,96% | 462 |
| Standardowa_DS4_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 8 | 1 | 27,5 | 116 681 | 1 097 | 0,94% | 231 |
| Standardowa_DS4_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 8 | 1 | 27,5 | 112 512 | 1 261 | 1,12% | 462 |
| Standard_DS5_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 16 | 1 | 55,0 | 225 661 | 2 370 | 1,05% | 189 |
| Standard_DS5_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 16 | 2 | 55,0 | 229 145 | 2 878 | 1,26% | 21 |
| Standard_DS5_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 16 | 1 | 55,0 | 226 818 | 1 797 | 0,79% | 497 |
| Standardowa_DS11_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 2 | 1 | 13,7 | 28 571 | 920 | 3,22% | 238 |
| Standardowa_DS11_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 2 | 1 | 13,7 | 29 049 | 1 614 | 5,56% | 469 |
| Standard_DS11 — 1_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 1 | 1 | 13,7 | 14 594 | 617 | 4,23% | 287 |
| Standard_DS11 — 1_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 1 | 1 | 13,7 | 14 951 | 852 | 5,70% | 413 |
| Standardowa_DS12_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 4 | 1 | 27,5 | 57 503 | 1 398 | 2,43% | 217 |
| Standardowa_DS12_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 4 | 1 | 27,5 | 57 082 | 2 372 | 4,16% | 483 |
| Standard_DS12 — 1_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 1 | 1 | 27,5 | 14 698 | 564 | 3,84% | 238 |
| Standard_DS12 — 1_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 1 | 1 | 27,5 | 15 127 | 941 | 6,22% | 462 |
| Standard_DS12 — 2_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 2 | 1 | 27,5 | 28 711 | 981 | 3,42% | 259 |
| Standard_DS12 — 2_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 2 | 1 | 27,5 | 29 305 | 1 241 | 4,24% | 441 |
| Standardowa_DS13_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 8 | 1 | 55,0 | 116 875 | 1 286 | 1,10% | 203 |
| Standardowa_DS13_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 8 | 1 | 55,0 | 112 318 | 1 356 | 1,21% | 504 |
| Standard_DS13 — 2_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 2 | 1 | 55,0 | 29 105 | 1 154 | 3,97% | 224 |
| Standard_DS13 — 2_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 2 | 1 | 55,0 | 29 936 | 1 720 | 5,75% | 483 |
| Standard_DS13 — 4_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 4 | 1 | 55,0 | 56 992 | 1 814 | 3,18% | 280 |
| Standard_DS13 — 4_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 4 | 1 | 55,0 | 57 781 | 2 122 | 3,67% | 427 |
| Standardowa_DS14_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 16 | 2 | 110,2 | 224 149 | 3 450 | 1,54% | 196 |
| Standardowa_DS14_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 16 | 1 | 110,2 | 227 108 | 1 267 | 0,56% | 504 |
| Standard_DS14 — 4_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 4 | 2 | 110,2 | 56 211 | 2 154 | 3,83% | 189 |
| Standard_DS14 — 4_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 4 | 1 | 110,2 | 59 651 | 2 560 | 4,29% | 518 |
| Standard_DS14 — 8_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 8 | 2 | 110,2 | 112 280 | 4 430 | 3,95% | 196 |
| Standard_DS14 — 8_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 8 | 1 | 110,2 | 113 375 | 1 442 | 1,27% | 511 |
| Standard_DS15_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 20 | 2 | 137,7 | 279 359 | 4 032 | 1,44% | 665 |

## <a name="dv2---general-compute"></a>Dv2 — ogólne obliczenia
(3/12/2019 6:53:48 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standardowa_D1_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 1 | 1 | 3.4 | 14 730 | 663 | 4,50% | 385 |
| Standardowa_D1_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 1 | 1 | 3.4 | 15 057 | 1 319 | 8,76% | 322 |
| Standardowa_D2_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 2 | 1 | 6.8 | 29 395 | 1 073 | 3,65% | 329 |
| Standardowa_D2_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 2 | 1 | 6.8 | 29 564 | 2 145 | 7,26% | 378 |
| Standardowa_D3_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 4 | 1 | 13,7 | 58 150 | 1 340 | 2,30% | 343 |
| Standardowa_D3_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 4 | 1 | 13,7 | 57 820 | 2 944 | 5,09% | 364 |
| Standardowa_D4_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 8 | 1 | 27,5 | 117 448 | 1 612 | 1,37% | 308 |
| Standardowa_D4_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 8 | 1 | 27,5 | 114 082 | 3 369 | 2,95% | 399 |
| Standardowa_D5_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 16 | 1 | 55,0 | 226 370 | 4 722 | 2,09% | 147 |
| Standardowa_D5_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 16 | 2 | 55,0 | 225 035 | 5 026 | 2,23% | 119 |
| Standardowa_D5_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 16 | 1 | 55,0 | 227 883 | 3 259 | 1,43% | 441 |
| Standardowa_D11_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 2 | 1 | 13,7 | 29 260 | 1 012 | 3,46% | 308 |
| Standardowa_D11_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 2 | 1 | 13,7 | 29 306 | 1 763 | 6,02% | 399 |
| Standardowa_D12_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 4 | 1 | 27,5 | 58 322 | 1 391 | 2,39% | 329 |
| Standardowa_D12_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 4 | 1 | 27,5 | 57 999 | 3 533 | 6,09% | 371 |
| Standardowa_D13_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 8 | 1 | 55,0 | 117 218 | 1 514 | 1,29% | 329 |
| Standardowa_D13_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 8 | 1 | 55,0 | 114 344 | 3 307 | 2,89% | 378 |
| Standardowa_D14_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 16 | 2 | 110,2 | 224 348 | 5 477 | 2,44% | 280 |
| Standardowa_D14_v2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 16 | 1 | 110,2 | 228 221 | 2 733 | 1,20% | 427 |
| Standard_D15_v2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 20 | 2 | 137,7 | 281 494 | 7 976 | 2,83% | 672 |

## <a name="esv3---memory-optimized--premium-storage"></a>Esv3 — zoptymalizowane pod kątem pamięci + Premium Storage
(3/12/2019 7:17:33 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standardowa_E2s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 2 | 1 | 15,7 | 20 957 | 1200 | 5,73% | 672 |
| Standardowa_E4s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 4 | 1 | 31,4 | 40 420 | 1 993 | 4,93% | 672 |
| Standard_E4 — 2s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 2 | 1 | 31,4 | 20 774 | 1 133 | 5,45% | 672 |
| Standardowa_E8s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 8 | 1 | 62,9 | 80 153 | 3 308 | 4,13% | 665 |
| Standard_E8 — 2s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 2 | 1 | 62,9 | 21 178 | 1 334 | 6,30% | 665 |
| Standard_E8 — 4s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 4 | 1 | 62,9 | 40 614 | 2 216 | 5,46% | 672 |
| Standardowa_E16s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 16 | 1 | 125,9 | 156 137 | 2 160 | 1,38% | 672 |
| Standard_E16 — 4s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 4 | 1 | 125,9 | 41 950 | 2 309 | 5,50% | 637 |
| Standard_E16 — 8s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 8 | 1 | 125,9 | 81 196 | 3 179 | 3,91% | 658 |
| Standard_E20s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 20 | 1 | 157,4 | 196 619 | 1 325 | 0,67% | 672 |
| Standardowa_E32s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 32 | 2 | 251,9 | 304 707 | 5 719 | 1,88% | 672 |
| Standard_E32 — 8s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 8 | 2 | 251,9 | 83 576 | 3 693 | 4,42% | 672 |
| Standard_E32 — 16s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 16 | 2 | 251,9 | 158 023 | 4 317 | 2,73% | 672 |
| Standardowa_E64s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 64 | 2 | 425,2 | 628 540 | 3 982 | 0,63% | 49 |
| Standard_E64 — 16s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 16 | 2 | 425,2 | 169 611 | 3 265 | 1,92% | 42 |
| Standard_E64 — 32s_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 32 | 2 | 425,2 | 307 584 | 3 569 | 1,16% | 56 |

## <a name="eisv3---memory-opt--premium-storage-isolated"></a>Eisv3-Memory opt + Premium Storage (izolowany)
(4/11/2019 10:07:29 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standard_E64is_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 64 | 2 | 425,2 | 627 745 | 4 062 | 0,65% | 196 |

## <a name="ev3---memory-optimized"></a>EV3 — zoptymalizowane pod kątem pamięci
(3/12/2019 6:52:13 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standardowa_E2_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 2 | 1 | 15,7 | 21 171 | 1 772 | 8,37% | 693 |
| Standardowa_E4_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 4 | 1 | 31,4 | 41 181 | 3 148 | 7,64% | 700 |
| Standardowa_E8_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 8 | 1 | 62,9 | 81 211 | 5 055 | 6,22% | 700 |
| Standardowa_E16_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 16 | 1 | 125,9 | 158 152 | 4 033 | 2,55% | 700 |
| Standard_E20_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 20 | 1 | 157,4 | 197 739 | 2 731 | 1,38% | 693 |
| Standardowa_E32_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 32 | 2 | 251,9 | 307 286 | 8 353 | 2,72% | 700 |
| Standardowa_E64_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 64 | 2 | 425,2 | 628 451 | 9 235 | 1,47% | 707 |

## <a name="eiv3---memory-optimized-isolated"></a>Eiv3 — zoptymalizowane pod kątem pamięci (izolowany)
(3/12/2019 6:57:51 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standard_E64i_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 64 | 2 | 425,2 | 625 855 | 4 881 | 0,78% | 7 |
| Standard_E64i_v3 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 64 | 2 | 425,2 | 629 151 | 9 756 | 1,55% | 217 |

## <a name="fsv2---compute--storage-optimized"></a>Fsv2-COMPUTE + magazyn zoptymalizowany
(3/12/2019 6:51:35 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standard_F2s_v2 | Procesor Intel (R) Xeon (R) Platinum 8168 CPU @ 2.70 GHz | 2 | 1 | 3.9 | 28 219 | 1 843 | 6,53% | 700 |
| Standard_F4s_v2 | Procesor Intel (R) Xeon (R) Platinum 8168 CPU @ 2.70 GHz | 4 | 1 | 7,8 | 53 911 | 1 002 | 1,86% | 707 |
| Standard_F8s_v2 | Procesor Intel (R) Xeon (R) Platinum 8168 CPU @ 2.70 GHz | 8 | 1 | 15,7 | 106 467 | 1 101 | 1,03% | 707 |
| Standard_F16s_v2 | Procesor Intel (R) Xeon (R) Platinum 8168 CPU @ 2.70 GHz | 16 | 1 | 31,4 | 211 311 | 1 724 | 0,82% | 707 |
| Standard_F32s_v2 | Procesor Intel (R) Xeon (R) Platinum 8168 CPU @ 2.70 GHz | 32 | 1 | 62,9 | 423 175 | 4 346 | 1,03% | 707 |
| Standard_F64s_v2 | Procesor Intel (R) Xeon (R) Platinum 8168 CPU @ 2.70 GHz | 64 | 2 | 125,9 | 829 537 | 21 574 | 2,60% | 707 |
| Standard_F72s_v2 | Procesor Intel (R) Xeon (R) Platinum 8168 CPU @ 2.70 GHz | 72 | 2 | 141,7 | 933 800 | 26 783 | 2,87% | 707 |

## <a name="fs---compute-and-storage-optimized"></a>FS — zoptymalizowane pod kątem obliczeń i magazynu
(3/15/2019 12:12:51 AM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standardowa_F1s | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 1 | 1 | 1.9 | 14 552 | 504 | 3,46% | 350 |
| Standardowa_F1s | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 1 | 1 | 1.9 | 14 784 | 858 | 5,80% | 357 |
| Standardowa_F2s | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 2 | 1 | 3.9 | 28 664 | 895 | 3,12% | 245 |
| Standardowa_F2s | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 2 | 1 | 3.9 | 29 188 | 1 228 | 4,21% | 455 |
| Standardowa_F4s | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 4 | 1 | 7,8 | 57 192 | 1 700 | 2,97% | 259 |
| Standardowa_F4s | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 4 | 1 | 7,8 | 57 412 | 2 215 | 3,86% | 448 |
| Standardowa_F8s | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 8 | 1 | 15,7 | 117 008 | 1 139 | 0,97% | 259 |
| Standardowa_F8s | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 8 | 1 | 15,7 | 112 610 | 1 595 | 1,42% | 441 |
| Standardowa_F16s | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 16 | 1 | 31,4 | 225 444 | 2 328 | 1,03% | 210 |
| Standardowa_F16s | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 16 | 2 | 31,4 | 228 919 | 3 380 | 1,48% | 28 |
| Standardowa_F16s | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 16 | 1 | 31,4 | 227 015 | 1 543 | 0,68% | 462 |

## <a name="f---compute-optimized"></a>F — Optymalizacja obliczeń
(3/12/2019 6:53:59 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standardowa_F1 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 1 | 1 | 1.9 | 14 937 | 593 | 3,97% | 350 |
| Standardowa_F1 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 1 | 1 | 1.9 | 15 460 | 1 326 | 8,58% | 350 |
| Standardowa_F2 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 2 | 1 | 3.9 | 29 324 | 1 196 | 4,08% | 343 |
| Standardowa_F2 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 2 | 1 | 3.9 | 29 299 | 1 908 | 6,51% | 364 |
| Standardowa_F4 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 4 | 1 | 7,8 | 58 314 | 1 245 | 2,14% | 364 |
| Standardowa_F4 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 4 | 1 | 7,8 | 58 280 | 3 581 | 6,14% | 336 |
| Standardowa_F8 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 8 | 1 | 15,7 | 117 516 | 1 460 | 1,24% | 308 |
| Standardowa_F8 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 8 | 1 | 15,7 | 114 361 | 3 868 | 3,38% | 399 |
| Standardowa_F16 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 16 | 1 | 31,4 | 226 487 | 4 140 | 1,83% | 154 |
| Standardowa_F16 | Procesor Intel (R) Xeon (R) E5-2673 v3 @ 2.40 GHz | 16 | 2 | 31,4 | 226 683 | 4 723 | 2,08% | 133 |
| Standardowa_F16 | Procesor Intel (R) Xeon (R) E5-2673 v4 @ 2.30 GHz | 16 | 1 | 31,4 | 228 592 | 2 371 | 1,04% | 392 |

## <a name="gs---storage-optimized"></a>GS — zoptymalizowane pod kątem magazynu
(3/12/2019 10:22:33 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standardowa_GS1 | Procesor Intel (R) Xeon (R) E5-2698B v3 @ 2,00 GHz | 2 | 1 | 27,5 | 28 835 | 2 222 | 7,71% | 287 |
| Standardowa_GS2 | Procesor Intel (R) Xeon (R) E5-2698B v3 @ 2,00 GHz | 4 | 1 | 55,0 | 55 568 | 3 139 | 5,65% | 287 |
| Standardowa_GS3 | Procesor Intel (R) Xeon (R) E5-2698B v3 @ 2,00 GHz | 8 | 1 | 110,2 | 106 567 | 2 188 | 2,05% | 287 |
| Standardowa_GS4 | Procesor Intel (R) Xeon (R) E5-2698B v3 @ 2,00 GHz | 16 | 1 | 220,4 | 210 586 | 4 130 | 1,96% | 287 |
| Standard_GS4-4 | Procesor Intel (R) Xeon (R) E5-2698B v3 @ 2,00 GHz | 4 | 1 | 220,4 | 58 598 | 2 670 | 4,56% | 287 |
| Standard_GS4-8 | Procesor Intel (R) Xeon (R) E5-2698B v3 @ 2,00 GHz | 8 | 1 | 220,4 | 108 234 | 2 392 | 2,21% | 287 |
| Standardowa_GS5 | Procesor Intel (R) Xeon (R) E5-2698B v3 @ 2,00 GHz | 32 | 2 | 440,9 | 399 835 | 8 694 | 2,17% | 287 |
| Standardowa_GS5-8 | Procesor Intel (R) Xeon (R) E5-2698B v3 @ 2,00 GHz | 8 | 2 | 440,9 | 116 643 | 2 354 | 2,02% | 287 |
| Standard_GS5-16 | Procesor Intel (R) Xeon (R) E5-2698B v3 @ 2,00 GHz | 16 | 2 | 440,9 | 210 984 | 2 995 | 1,42% | 287 |

## <a name="g---compute-optimized"></a>G — Optymalizacja obliczeń
(3/12/2019 10:23:51 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standardowa_G1 | Procesor Intel (R) Xeon (R) E5-2698B v3 @ 2,00 GHz | 2 | 1 | 27,5 | 32 808 | 2 679 | 8,17% | 287 |
| Standardowa_G2 | Procesor Intel (R) Xeon (R) E5-2698B v3 @ 2,00 GHz | 4 | 1 | 55,0 | 62 907 | 4 465 | 7,10% | 287 |
| Standardowa_G3 | Procesor Intel (R) Xeon (R) E5-2698B v3 @ 2,00 GHz | 8 | 1 | 110,2 | 113 471 | 4 346 | 3,83% | 287 |
| Standardowa_G4 | Procesor Intel (R) Xeon (R) E5-2698B v3 @ 2,00 GHz | 16 | 1 | 220,4 | 212 092 | 2 857 | 1,35% | 287 |
| Standard_G5 | Procesor Intel (R) Xeon (R) E5-2698B v3 @ 2,00 GHz | 32 | 2 | 440,9 | 403 315 | 6 947 | 1,72% | 273 |

## <a name="h---high-performance-compute-hpc"></a>Obliczenia o wysokiej wydajności (HPC)
(3/12/2019 10:50:51 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standardowa_H8 | Procesor Intel (R) Xeon (R) E5-2667 V3 @ 3.20 GHz | 8 | 1 | 55,0 | 149 859 | 734 | 0,49% | 175 |
| Standardowa_H8m | Procesor Intel (R) Xeon (R) E5-2667 V3 @ 3.20 GHz | 8 | 1 | 110,2 | 149 931 | 657 | 0,44% | 147 |
| Standardowa_H16 | Procesor Intel (R) Xeon (R) E5-2667 V3 @ 3.20 GHz | 16 | 2 | 110,2 | 282 083 | 6 738 | 2,39% | 84 |
| Standardowa_H16m | Procesor Intel (R) Xeon (R) E5-2667 V3 @ 3.20 GHz | 16 | 2 | 220,4 | 282 106 | 7 013 | 2,49% | 84 |
| Standard_H16mr | Procesor Intel (R) Xeon (R) E5-2667 V3 @ 3.20 GHz | 16 | 2 | 220,4 | 282 167 | 6 889 | 2,44% | 84 |
| Standard_H16r | Procesor Intel (R) Xeon (R) E5-2667 V3 @ 3.20 GHz | 16 | 2 | 110,2 | 280 837 | 6 587 | 2,35% | 84 |

## <a name="lv2---storage-optimized"></a>Lv2 — zoptymalizowane pod kątem magazynu
(3/14/2019 5:49:04 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standard_L8s_v2 | AMD EPYC 7551 32 — procesor Core | 8 | 1 | 62,9 | 80 528 | 404 | 0,50% | 119 |
| Standard_L16s_v2 | AMD EPYC 7551 32 — procesor Core | 16 | 2 | 125,9 | 154 829 | 3 708 | 2,40% | 119 |
| Standard_L32s_v2 | AMD EPYC 7551 32 — procesor Core | 32 | 4 | 251,9 | 310 811 | 7 751 | 2,49% | 119 |
| Standard_L64s_v2 | AMD EPYC 7551 32 — procesor Core | 64 | 8 | 503,9 | 595 140 | 14 572 | 2,45% | 112 |
| Standard_L80s_v2 | AMD EPYC 7551 32 — procesor Core | 80 | 10 | 629,9 | 773 171 | 19 559 | 2,53% | 119 |

## <a name="ls---storage-optimized"></a>LS — magazyn zoptymalizowany pod kątem
(3/12/2019 10:22:29 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standardowa_L4s | Procesor Intel (R) Xeon (R) E5-2698B v3 @ 2,00 GHz | 4 | 1 | 31,4 | 56 488 | 2 916 | 5,16% | 287 |
| Standardowa_L8s | Procesor Intel (R) Xeon (R) E5-2698B v3 @ 2,00 GHz | 8 | 1 | 62,9 | 107 017 | 2 323 | 2,17% | 287 |
| Standardowa_L16s | Procesor Intel (R) Xeon (R) E5-2698B v3 @ 2,00 GHz | 16 | 1 | 125,9 | 210 865 | 3 653 | 1,73% | 280 |
| Standardowa_L32s | Procesor Intel (R) Xeon (R) E5-2698B v3 @ 2,00 GHz | 32 | 2 | 251,9 | 399 963 | 9 254 | 2,31% | 287 |

## <a name="m---memory-optimized"></a>M — zoptymalizowane pod kątem pamięci
(4/11/2019 7:30:39 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standard_M8 — 2 MS | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 2 | 1 | 215,2 | 22 605 | 29 | 0,13% | 42 |
| Standard_M8 — 4 MS | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 4 | 1 | 215,2 | 44 488 | 183 | 0,41% | 42 |
| Standard_M16 — 4 MS | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 4 | 1 | 430,6 | 44 451 | 269 | 0,61% | 42 |
| Standard_M16 — 8ms | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 8 | 1 | 430,6 | 88 238 | 1 243 | 1,41% | 42 |
| Standard_M32 — 8ms | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 8 | 1 | 861,2 | 88 521 | 1 353 | 1,53% | 42 |
| Standard_M32 — 16ms | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 16 | 1 | 861,2 | 174 674 | 3 104 | 1,78% | 42 |
| Standard_M64 | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 64 | 2 | 1 007,9 | 683 022 | 11 929 | 1,75% | 42 |
| Standard_M64 — 16ms | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 16 | 2 | 1 763,9 | 169 386 | 4 737 | 2,80% | 42 |
| Standard_M64 — 32ms | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 32 | 2 | 1 763,9 | 337 599 | 4 738 | 1,40% | 42 |
| Standard_M64m | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 64 | 2 | 1 763,9 | 677 466 | 14 478 | 2,14% | 42 |
| Standardowa_M64ms | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 64 | 2 | 1 763,9 | 675 342 | 16 577 | 2,45% | 42 |
| Standard_M64s | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 64 | 2 | 1 007,9 | 674 785 | 15 983 | 2,37% | 42 |
| Standard_M128 | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 128 | 4 | 2 015,9 | 1 334 218 | 21 126 | 1,58% | 42 |
| Standard_M128 — 32ms | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 32 | 4 | 3 831,1 | 334 873 | 5 005 | 1,49% | 42 |
| Standard_M128 — 64ms | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 64 | 4 | 3 831,1 | 667 808 | 18 145 | 2,72% | 42 |
| Standard_M128m | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 128 | 4 | 3 831,1 | 1 335 873 | 19 642 | 1,47% | 42 |
| Standard_M128ms | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 128 | 4 | 3 831,1 | 1 329 151 | 24 295 | 1,83% | 42 |
| Standard_M128s | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 128 | 4 | 2 015,9 | 1 329 923 | 20 117 | 1,51% | 42 |
| Standard_M16ms | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 16 | 1 | 430,6 | 174 686 | 2 704 | 1,55% | 35 |
| Standard_M32ls | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 32 | 1 | 251,9 | 344 069 | 3 372 | 0,98% | 42 |
| Standard_M32ms | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 32 | 1 | 861,2 | 343 226 | 4 884 | 1,42% | 84 |
| Standard_M32ms | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 32 | 2 | 861,2 | 336 526 | 4 396 | 1,31% | 7 |
| Standard_M32ts | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 32 | 1 | 188,9 | 341 112 | 5 491 | 1,61% | 35 |
| Standard_M64ls | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 64 | 2 | 503,9 | 676 026 | 18 078 | 2,67% | 42 |
| Standard_M8ms | Procesor Intel (R) Xeon (R) E7-8890 v3 @ 2.50 GHz | 8 | 1 | 215,2 | 88 066 | 1 391 | 1,58% | 42 |

## <a name="ncsv3---gpu-enabled"></a>NCSv3 — procesor GPU włączony
(3/21/2019 5:48:37 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standard_NC6s_v3 | Procesor Intel (R) Xeon (R) E5-2690 v4 @ 2.60 GHz | 6 | 1 | 110,2 | 106 929 | 353 | 0,33% | 49 |
| Standard_NC12s_v3 | Procesor Intel (R) Xeon (R) E5-2690 v4 @ 2.60 GHz | 12 | 1 | 220,4 | 213 585 | 875 | 0,41% | 42 |
| Standard_NC24rs_v3 | Procesor Intel (R) Xeon (R) E5-2690 v4 @ 2.60 GHz | 24 | 2 | 440,9 | 403 554 | 6 705 | 1,66% | 42 |
| Standard_NC24s_v3 | Procesor Intel (R) Xeon (R) E5-2690 v4 @ 2.60 GHz | 24 | 2 | 440,9 | 403 874 | 7 603 | 1,88% | 42 |

## <a name="ncsv2---gpu-enabled"></a>NCSv2 — procesor GPU włączony
(3/12/2019 11:19:19 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standard_NC6s_v2 | Procesor Intel (R) Xeon (R) E5-2690 v4 @ 2.60 GHz | 6 | 1 | 110,2 | 107 115 | 321 | 0,30% | 63 |
| Standard_NC12s_v2 | Procesor Intel (R) Xeon (R) E5-2690 v4 @ 2.60 GHz | 12 | 1 | 220,4 | 213 814 | 656 | 0,31% | 63 |
| Standard_NC24rs_v2 | Procesor Intel (R) Xeon (R) E5-2690 v4 @ 2.60 GHz | 24 | 2 | 440,9 | 401 728 | 6 995 | 1,74% | 63 |
| Standard_NC24s_v2 | Procesor Intel (R) Xeon (R) E5-2690 v4 @ 2.60 GHz | 24 | 2 | 440,9 | 402 808 | 7 923 | 1,97% | 63 |

## <a name="nc---gpu-enabled"></a>NC — procesor GPU włączony
(3/12/2019 11:08:03 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standardowa_NC6 | Procesor Intel (R) Xeon (R) E5-2690 v3 @ 2.60 GHz | 6 | 1 | 55,0 | 102 211 | 658 | 0,64% | 259 |
| Standardowa_NC12 | Procesor Intel (R) Xeon (R) E5-2690 v3 @ 2.60 GHz | 12 | 1 | 110,2 | 203 523 | 2 293 | 1,13% | 259 |
| Standardowa_NC24 | Procesor Intel (R) Xeon (R) E5-2690 v3 @ 2.60 GHz | 24 | 2 | 220,4 | 382 897 | 8 712 | 2,28% | 259 |
| Standard_NC24r | Procesor Intel (R) Xeon (R) E5-2690 v3 @ 2.60 GHz | 24 | 2 | 220,4 | 383 171 | 9 166 | 2,39% | 259 |

## <a name="nds--gpu-enabled"></a>NDs — włączono procesor GPU
(3/12/2019 11:19:10 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standard_ND6s | Procesor Intel (R) Xeon (R) E5-2690 v4 @ 2.60 GHz | 6 | 1 | 110,2 | 107 095 | 353 | 0,33% | 63 |
| Standard_ND12s | Procesor Intel (R) Xeon (R) E5-2690 v4 @ 2.60 GHz | 12 | 1 | 220,4 | 212 298 | 3 457 | 1,63% | 63 |
| Standard_ND24rs | Procesor Intel (R) Xeon (R) E5-2690 v4 @ 2.60 GHz | 24 | 2 | 440,9 | 402 749 | 7 838 | 1,95% | 56 |
| Standard_ND24s | Procesor Intel (R) Xeon (R) E5-2690 v4 @ 2.60 GHz | 24 | 2 | 440,9 | 401 822 | 7 776 | 1,94% | 63 |

## <a name="nv---gpu-enabled"></a>NV — procesor GPU włączony
(3/12/2019 11:08:13 PM PBI 3897709)

| Rozmiar maszyny wirtualnej | Procesor CPU | Procesory wirtualne | Węzły NUMA | Pamięć (GiB) | Średni wynik | Odchylenie standardowe | Odchylenie standardowe% | #Runs |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Standardowa_NV6 | Procesor Intel (R) Xeon (R) E5-2690 v3 @ 2.60 GHz | 6 | 1 | 55,0 | 101 728 | 2 094 | 2,06% | 259 |
| Standardowa_NV12 | Procesor Intel (R) Xeon (R) E5-2690 v3 @ 2.60 GHz | 12 | 1 | 110,2 | 203 903 | 1 724 | 0,85% | 252 |
| Standardowa_NV24 | Procesor Intel (R) Xeon (R) E5-2690 v3 @ 2.60 GHz | 24 | 2 | 220,4 | 379 879 | 8 737 | 2,30% | 259 |


## <a name="about-coremark"></a>Informacje o poduwagi
Numery systemu Linux zostały obliczone przez uruchomienie [w systemie Ubuntu](https://www.eembc.org/coremark/faq.php) . Dla opcji inuwaga została skonfigurowana liczba wątków ustawionych na liczbę wirtualnych procesorów CPU, a współbieżność ustawiona na PThreads. Docelowa liczba iteracji została skorygowana na podstawie oczekiwanej wydajności, aby zapewnić środowisko uruchomieniowe co najmniej 20 sekund (zwykle znacznie dłużej). Końcowy wynik przedstawia liczbę iteracji zakończonych podziałem przez liczbę sekund trwania testu. Każdy test był uruchamiany co najmniej siedem razy na każdej maszynie wirtualnej. Pokazane powyżej daty przebiegu testu. Testy są uruchamiane na wielu maszynach wirtualnych w publicznych regionach platformy Azure, a maszyna wirtualna była obsługiwana w dniu uruchomienia. Seria podstawowa A i B (z możliwością szeregowania) nie jest wyświetlana, ponieważ wydajność jest zmienna. Seria N nie jest pokazywana, ponieważ są skoncentrowane na procesorach GPU i nie mierzy wydajności procesora GPU.

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać informacje na temat pojemności magazynu, szczegółów dysku i dodatkowych zagadnień związanych z wybieraniem rozmiarów maszyn wirtualnych, zobacz [rozmiary maszyny wirtualnej](../sizes.md).
* Aby móc uruchamiać skrypty programu do uwagi na maszynach wirtualnych z systemem Linux, Pobierz [pakiet skryptów](https://download.microsoft.com/download/3/0/5/305A3707-4D3A-4599-9670-AAEB423B4663/AzureCoreMarkScriptPack.zip)programu.