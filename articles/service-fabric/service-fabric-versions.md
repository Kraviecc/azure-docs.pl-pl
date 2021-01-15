---
title: Obsługiwane wersje klastra w usłudze Azure Service Fabric
description: Dowiedz się więcej o wersjach klastra w usłudze Azure Service Fabric, łącznie z linkiem do najnowszych wydań z blogu zespołu Service Fabric.
ms.topic: troubleshooting
ms.date: 06/15/2020
ms.openlocfilehash: c2ea2b53649cf148a19df46835c8936345aa20e5
ms.sourcegitcommit: c7153bb48ce003a158e83a1174e1ee7e4b1a5461
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/15/2021
ms.locfileid: "98234345"
---
# <a name="supported-service-fabric-versions"></a>Obsługiwane Service Fabric wersje

Upewnij się, że w klastrze jest zawsze uruchomiona obsługiwana wersja usługi Azure Service Fabric. Co najmniej 60 dni po opublikowaniu nowej wersji Service Fabric, obsługa poprzedniej wersji zostanie zakończona. Anonse nowych wydań znajdziesz na [blogu zespołu Service Fabric](https://azure.microsoft.com/updates/?product=service-fabric).

W przypadku danej wersji środowiska uruchomieniowego Service Fabric można użyć określonych lub starszych wersji pakietów SDK/NuGet. Nowsze wersje pakietów nie są obsługiwane i mogą mieć problemy związane ze starszymi klastrami, ponieważ mogą one mieć zmiany funkcji lub protokołu nieobsługiwane przez te środowiska.

Zapoznaj się z następującymi dokumentami, aby uzyskać szczegółowe informacje o tym, jak utrzymać klaster z obsługiwaną wersją Service Fabric:

- [Uaktualnianie klastra usługi Azure Service Fabric](service-fabric-cluster-upgrade.md)
- [Uaktualnij wersję Service Fabric działającą w autonomicznym klastrze systemu Windows Server](service-fabric-cluster-upgrade-windows-server.md)


## <a name="unsupported-versions"></a>Nieobsługiwane wersje

### <a name="upgrade-alert-for-versions-between-57-and-below-6363"></a>Zgłoś alert dla wersji z zakresu od 5,7 do 6.3.63. *
Aby zwiększyć bezpieczeństwo i dostępność, infrastruktura platformy Azure wprowadzi zmianę, która może mieć wpływ na Service Fabric klientów. **Wszystkie klastry Service Fabric w nieobsługiwanych wersjach od 5,7 do 6,3.** Rozadresowanie zmiany wymaga aktualizacji środowiska uruchomieniowego Service Fabric, która jest już dostępna dla wszystkich obsługiwanych Service Fabric wersji we wszystkich regionach.

Zalecamy i zalecamy podejmowanie działań w celu przeprowadzenia uaktualnienia do najnowszych obsługiwanych wersji do **19 stycznia 2021,** aby uniknąć przerw w świadczeniu usługi, jeśli masz plan pomocy technicznej i potrzebujesz pomoc techniczną, skontaktuj się z nami za pośrednictwem kanałów pomocy technicznej systemu Azure, otwierając żądanie pomocy technicznej dla usługi Azure Service Fabric i wspominając o tym kontekście w ramach biletu pomocy technicznej.

#### <a name="impact-if-not-upgraded-to-supported-versions"></a>Wpływ, jeśli nie zostanie uaktualniony do obsługiwanych wersji

**Klastry usługi Azure Service Fabric uruchamiane w nieobsługiwanych wersjach z 5,7 do 6.3.63. \* Program nie będzie mógł działać i będzie niedostępny** , jeśli nie uaktualniono do jednej z poniższych obsługiwanych wersji do 19 stycznia 2021.

#### <a name="required-action"></a>Wymagana akcja
Uaktualnij do Service Fabric obsługiwanych wersji wymienionych poniżej, aby zapobiec przestojom lub utracie funkcjonalności związanej z tą zmianą. Upewnij się, że w klastrach działają co najmniej te wersje, aby zapobiec problemom w danym środowisku.

  ###### <a name="supported-service-fabric-runtime-versions"></a>Obsługiwane Service Fabric wersje środowiska uruchomieniowego
   Jeśli nie znajdujesz się na poniższej liście obsługiwanych wersji Service Fabric, przeprowadź uaktualnienie do jednej z tych wersji, które zawierają już niezbędne zmiany, aby zapobiec przestojom w klastrze. **Uwaga:** Wszystkie wersje wydań 7,2 obejmują niezbędne zmiany.
  
  | System operacyjny | Bieżące środowisko uruchomieniowe Service Fabric w klastrze | Wydanie w wersji CU/patch  | 
  | --- | --- |--- | 
  | Windows | 7,0. * | 7.0.478.9590 |
  | Windows | 7,1. * | 7.1.503.9590 |
  | Windows | 7,2. * | 7,2. * |
  | Ubuntu 16 | 7,0. * | 7.0.472.1  |
  | Linux Ubuntu 16,04 | 7,1. * | 7.1.455.1  |
  | Linux Ubuntu 18,04 | 7,1. * | 7.1.455.1804 |
  | Linux Ubuntu 16,04 | 7,2. * | 7,2. * |
  | Linux Ubuntu 18,04 | 7,2. * | 7,2. * |
 
### <a name="upgrade-alert-for-versions-greater-than-63"></a>Zgłoś alert dla wersji większych niż 6,3 
Aby zwiększyć bezpieczeństwo i dostępność, infrastruktura platformy Azure wprowadzi zmianę, która może mieć wpływ na Service Fabric klientów. **Wszystkie klastry Service Fabric, które korzystają z [funkcji Otwórz sieć dla kontenerów](https://docs.microsoft.com/azure/service-fabric/service-fabric-networking-modes#set-up-open-networking-mode), działają w nieobsługiwanych wersjach większych niż 6,3 i niższych niż 7,0, ale mają wpływ na niezgodne wersje obsługiwane przez 7,0**. Rozadresowanie zmiany wymaga aktualizacji środowiska uruchomieniowego Service Fabric, która jest już dostępna dla wszystkich obsługiwanych Service Fabric wersji we wszystkich regionach.

 #### <a name="impact-if-not-upgraded-to-supported-versions"></a>Wpływ, jeśli nie zostanie uaktualniony do obsługiwanych wersji
  Klastry usługi Azure Service Fabric **używające funkcji [Otwórz funkcję sieci dla](https://docs.microsoft.com/azure/service-fabric/service-fabric-networking-modes#set-up-open-networking-mode) kontenerów dla kontenerów i działają w wersjach większych niż 6,3** , które nie obejmują zmian, spowodują utratę funkcjonalności lub przerw w działaniu usługi, jeśli nie zostaną uaktualnione do jednej z poniższych obsługiwanych wersji do **19 stycznia 2021**.
 
  - **W przypadku klastrów z uruchomioną wersją Service Fabric większą niż 6,3 nie korzystających z funkcji sieci**, klaster pozostanie Nieuruchomiony, jednak funkcja otwartej sieci dla klastrów kontenerów przestanie działać, co może spowodować zakłócenia usługi dla obciążeń.

 - **W przypadku klastrów z uruchomioną wersją Service Fabric większą niż 6,3 i używania [funkcji Otwórz sieć dla kontenerów](https://docs.microsoft.com/azure/service-fabric/service-fabric-networking-modes#set-up-open-networking-mode)** klaster może stać się niedostępny i przestanie działać, co może spowodować przerwanie działania usługi dla obciążeń.
  
#### <a name="required-action"></a>Wymagana akcja
Uaktualnij do Service Fabric obsługiwanych wersji wymienionych poniżej, aby zapobiec przestojom lub utracie funkcjonalności związanej z tą zmianą. Upewnij się, że w klastrach działają co najmniej te wersje, aby zapobiec problemom w danym środowisku. 
 
 ###### <a name="supported-service-fabric-runtime-versions"></a>Obsługiwane Service Fabric wersje środowiska uruchomieniowego
 Jeśli nie znajdujesz się na poniższej liście obsługiwanych wersji Service Fabric, przeprowadź uaktualnienie do jednej z tych wersji, które zawierają już niezbędne zmiany, aby zapobiec utracie funkcjonalności.  **Uwaga:** Wszystkie wersje wydań 7,2 obejmują niezbędne zmiany.
 
  | System operacyjny | Bieżące środowisko uruchomieniowe Service Fabric w klastrze | Wydanie w wersji CU/patch  | 
  | --- | --- |--- | 
  | Windows | 7,0. * | 7.0.478.9590 |
  | Windows | 7,1. * | 7.1.503.9590 |
  | Windows | 7,2. * | 7,2. * |
  | Linux Ubuntu 16,04 | 7,0. * | 7.0.472.1  |
  | Linux Ubuntu 16,04 | 7,1. * | 7.1.455.1  |
  | Linux Ubuntu 18,04 | 7,1. * | 7.1.455.1804 |
  | Linux Ubuntu 16,04 | 7,2. * | 7,2. * |
  | Linux Ubuntu 18,04 | 7,2. * | 7,2. * |

## <a name="supported-versions"></a>Obsługiwane wersje
W poniższej tabeli wymieniono wersje Service Fabric i ich daty końcowe pomocy technicznej.

| Service Fabric środowisko uruchomieniowe w klastrze | Można uaktualnić bezpośrednio z wersji klastra |Zgodna wersja zestawu SDK lub pakietu NuGet | Koniec wsparcia |
| --- | --- |--- | --- |
| Wszystkie wersje klastra przed 5.3.121 | 5.1.158.* |Mniejsze niż lub równe wersji 2,3 |20 stycznia 2017 |
| 5,3. * | 5.1.158.* |Mniejsze niż lub równe wersji 2,3 |24 lutego 2017 |
| 5,4. * | 5.1.158.* |Mniejsze niż lub równe wersji 2,4 |10 maja 2017       |
| 5,5. * | 5.4.164.* |Mniejsze niż lub równe wersji 2,5 |10 sierpnia 2017 r.    |
| 5,6. * | 5.4.164.* |Mniejsze niż lub równe wersji 2,6 |13 października 2017 r.   |
| 5,7. * | 5.4.164.* |Mniejsze niż lub równe wersji 2,7 |15 grudnia 2017 r.  |
| 6,0. * | 5.6.205.* |Mniejsze niż lub równe wersji 2,8 |30 marca 2018     |
| 6,1. * | 5.7.221.* |Mniejsze niż lub równe wersji 3,0 |15 lipca 2018      |
| 6,2. * | 6.0.232.* |Mniejsze niż lub równe wersji 3,1 |26 października 2018   |
| 6,3. * | 6.1.480.* |Mniejsze niż lub równe wersji 3,2 |31 marca 2019  |
| 6,4. * | 6.2.301.* |Mniejsze niż lub równe wersji 3,3 |15 września 2019 |
| 6,5. * | 6.4.617.* |Mniejsze niż lub równe wersji 3,4 |1 sierpnia 2020 |
| 7.0.466.* | 6.4.664.* |Mniejsze niż lub równe wersji 4,0|31 stycznia 2021  |
| 7.0.466.* | 6,5. * |Mniejsze niż lub równe wersji 4,0|31 stycznia 2021 |
| 7.0.470.* | 7.0.466.* |Mniejsze niż lub równe wersji 4,0 |31 stycznia 2021  |
| 7.0.472.* | 7.0.466.* |Mniejsze niż lub równe wersji 4,0 |31 stycznia 2021  |
| 7.0.478.* | 7.0.466.* |Mniejsze niż lub równe wersji 4,0 |31 stycznia 2021  |
| 7.1.409.* | 7.0.466.* |Mniejsze niż lub równe wersji 4,1 |31 marca 2021 |
| 7.1.417.* | 7.0.466.* |Mniejsze niż lub równe wersji 4,1 |31 marca 2021 |
| 7.1.428.* | 7.0.466.* |Mniejsze niż lub równe wersji 4,1 |31 marca 2021 |
| 7.1.456.* | 7.0.466.* |Mniejsze niż lub równe wersji 4,1 |31 marca 2021 |
| 7.1.458.* | 7.0.466.* |Mniejsze niż lub równe wersji 4,1 |31 marca 2021 |
| 7.1.459.* | 7.0.466.* |Mniejsze niż lub równe wersji 4,1 |31 marca 2021 |
| 7.1.503.* | 7.0.466.* |Mniejsze niż lub równe wersji 4,1 |31 marca 2021 |
| 7.2.413.* | 7.0.470.* |Mniejsze niż lub równe wersji 4,2 |Bieżąca wersja, dlatego bez daty zakończenia |
| 7.2.432.* | 7.0.470.* |Mniejsze niż lub równe wersji 4,2 |Bieżąca wersja, dlatego bez daty zakończenia |
| 7.2.433.* | 7.0.470.* |Mniejsze niż lub równe wersji 4,2 |Bieżąca wersja, dlatego bez daty zakończenia |
| 7.2.445.* | 7.0.470.* |Mniejsze niż lub równe wersji 4,2 |Bieżąca wersja, dlatego bez daty zakończenia |

## <a name="supported-operating-systems"></a>Obsługiwane systemy operacyjne

W poniższej tabeli wymieniono systemy operacyjne obsługiwane przez obsługiwane wersje Service Fabric.

| System operacyjny | Najwcześniejsza obsługiwana wersja Service Fabric |
| --- | --- |
| Windows Server 2012 z dodatkiem R2 | Wszystkie wersje |
| Windows Server 2016 | Wszystkie wersje |
| System Windows Server 1709 | 6.0 |
| System Windows Server 1803 | 6.4 |
| System Windows Server 1809 | 6.4.654.9590 |
| Windows Server 2019 | 6.4.654.9590 |
| Linux Ubuntu 16,04 | 6.0 |
| Linux Ubuntu 18,04 | 7.1 |

## <a name="supported-version-names"></a>Obsługiwane nazwy wersji

W poniższej tabeli wymieniono nazwy wersji Service Fabric i odpowiadające im numery wersji.

| Nazwa wersji | Numer wersji systemu Windows | Numer wersji systemu Linux |
| --- | --- | --- |
| 5,3 RTO | 5.3.121.9494 | Nie dotyczy |
| 5,3 CU1 | 5.3.204.9494 | Nie dotyczy |
| 5,3 ZASTOSUJESZ PAKIETU CU2 | 5.3.301.9590 | Nie dotyczy |
| 5,3 CU3 | 5.3.311.9590 | Nie dotyczy |
| 5,4 ZASTOSUJESZ PAKIETU CU2 | 5.4.164.9494 | Nie dotyczy |
| 5,5 CU1 | 5.5.216.0    | Nie dotyczy |
| 5,5 ZASTOSUJESZ PAKIETU CU2 | 5.5.219.0    | Nie dotyczy |
| 5,5 CU3 | 5.5.227.0    | Nie dotyczy |
| 5,5 CU4 | 5.5.232.0 | Nie dotyczy |
| 5,6 RTO | 5.6.204.9494 | Nie dotyczy |
| 5,6 ZASTOSUJESZ PAKIETU CU2 | 5.6.210.9494 | Nie dotyczy |
| 5,6 CU3 | 5.6.220.9494 | Nie dotyczy |
| 5,7 RTO | 5.7.198.9494 | Nie dotyczy |
| 5,7 CU4 | 5.7.221.9494 | Nie dotyczy |
| 6,0 RTO | 6.0.211.9494 | 6.0.120.1 |
| 6,0 CU1 | 6.0.219.9494 | 6.0.127.1 |
| 6,0 ZASTOSUJESZ PAKIETU CU2 | 6.0.232.9494 | 6.0.133.1 |
| 6,1 CU1 | 6.1.456.9494 | 6.1.183.1 |
| 6,1 ZASTOSUJESZ PAKIETU CU2 | 6.1.467.9494 | 6.1.185.1 |
| 6,1 CU3 | 6.1.472.9494 | Nie dotyczy |
| 6,1 CU4 | 6.1.480.9494 | 6.1.187.1 |
| 6,2 RTO | 6.2.269.9494 | 6.2.184.1 | 
| 6,2 CU1 | 6.2.274.9494 | 6.2.191.1 |
| 6,2 ZASTOSUJESZ PAKIETU CU2 | 6.2.283.9494 | 6.2.194.1 |
| 6,2 CU3 | 6.2.301.9494 | 6.2.199.1 |
| 6,3 RTO | 6.3.162.9494 | 6.3.119.1 |
| 6,3 CU1 | 6.3.176.9494 | 6.3.124.1 |
| 6,3 CU1 | 6.3.187.9494 | 6.3.129.1 |
| 6,4 RTO | 6.4.617.9590 | 6.4.625.1 |
| 6,4 ZASTOSUJESZ PAKIETU CU2 | 6.4.622.9590 | Nie dotyczy |
| 6,4 CU3 | 6.4.637.9590 | 6.4.634.1 |
| 6,4 CU4 | 6.4.644.9590 | 6.4.639.1 |
| 6,4 CU5 | 6.4.654.9590 | 6.4.649.1 |
| 6,4 CU6 | 6.4.658.9590 | Nie dotyczy |
| 6,4 CU7 | 6.4.664.9590 | 6.4.661.1 |
| 6,4 CU8 | 6.4.670.9590 | Nie dotyczy |
| 6,5 RTO | 6.5.639.9590 | 6.5.435.1 |
| 6,5 CU1 | 6.5.641.9590 | 6.5.454.1 |
| 6,5 ZASTOSUJESZ PAKIETU CU2 | 6.5.658.9590 | 6.5.460.1 |
| 6,5 CU3 | 6.5.664.9590 | 6.5.466.1 |
| 6,5 CU5 | 6.5.676.9590 | 6.5.467.1 |
| 7,0 RTO | 7.0.457.9590 | 7.0.457.1 |
| 7,0 ZASTOSUJESZ PAKIETU CU2 | 7.0.464.9590 | 7.0.464.1 |
| 7,0 CU3 | 7.0.466.9590 | 7.0.465.1 |
| 7,0 CU4 | 7.0.470.9590 | 7.0.469.1 |
| 7,0 CU6 | 7.0.472.9590 | 7.0.471.1 |
| 7,0 CU9 | 7.0.478.9590 | 7.0.472.1 |
| 7,1 RTO | 7.1.409.9590 | 7.1.410.1 |
| 7,1 CU1 | 7.1.417.9590 | 7.1.418.1 |
| 7,1 ZASTOSUJESZ PAKIETU CU2 | 7.1.428.9590 | 7.1.428.1 |
| 7,1 CU3 | 7.1.456.9590 | 7.1.452.1 |
| 7,1 CU5 | 7.1.458.9590 | 7.1.454.1 |
| 7,1 CU6 | 7.1.459.9590 | 7.1.455.1 |
| 7,1 CU8 | 7.1.503.9590 | 7.1.508.1 |
| 7,2 RTO | 7.2.413.9590 | Nie dotyczy |
| 7,2 ZASTOSUJESZ PAKIETU CU2 | 7.2.432.9590 | 7.2.431.1 |
| 7,2 CU3 | 7.2.433.9590 | Nie dotyczy |
| 7,2 CU4 | 7.2.445.9590 | 7.2.447.1 |

