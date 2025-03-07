---
title: Pytania dotyczące odnajdywania, oceny i analizy zależności w programie Azure Migrate
description: Uzyskaj odpowiedzi na często zadawane pytania dotyczące odnajdywania, oceny i analizy zależności w programie Azure Migrate.
author: vineetvikram
ms.author: vivikram
ms.manager: abhemraj
ms.topic: conceptual
ms.date: 06/09/2020
ms.openlocfilehash: 6c4dfed27a105fad951ae12ca053b6d86772717a
ms.sourcegitcommit: f3ec73fb5f8de72fe483995bd4bbad9b74a9cc9f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/04/2021
ms.locfileid: "102032572"
---
# <a name="discovery-assessment-and-dependency-analysis---common-questions"></a>Wykrywanie, Ocena i analiza zależności — typowe pytania

W tym artykule znajdują się odpowiedzi na często zadawane pytania dotyczące odnajdywania, oceny i analizy zależności w programie Azure Migrate. Jeśli masz inne pytania, zapoznaj się z następującymi zasobami:

- [Ogólne pytania](resources-faq.md) dotyczące Azure Migrate
- Pytania dotyczące [urządzenia Azure Migrate](common-questions-appliance.md)
- Pytania dotyczące [migracji serwera](common-questions-server-migration.md)
- Uzyskaj odpowiedzi na pytania na [forum Azure Migrate](https://aka.ms/AzureMigrateForum)


## <a name="what-geographies-are-supported-for-discovery-and-assessment-with-azure-migrate"></a>Jakie lokalizacje geograficzne są obsługiwane na potrzeby odnajdywania i oceny przy użyciu Azure Migrate?

Przejrzyj obsługiwane lokalizacje geograficzne [chmur publicznych](migrate-support-matrix.md#supported-geographies-public-cloud) i [chmur dla instytucji rządowych](migrate-support-matrix.md#supported-geographies-azure-government).


## <a name="how-many-vms-can-i-discover-with-an-appliance"></a>Ile maszyn wirtualnych można odnajdywać za pomocą urządzenia?

Możesz odkryć do 10 000 maszyn wirtualnych VMware, do 5 000 maszyn wirtualnych funkcji Hyper-V, a nawet do 1000 serwery fizyczne przy użyciu jednego urządzenia. Jeśli masz więcej maszyn, zapoznaj się [z tematem skalowanie oceny funkcji Hyper-V](scale-hyper-v-assessment.md), [skalowanie oceny oprogramowania VMware](scale-vmware-assessment.md)lub [skalowanie oceny serwera fizycznego](scale-physical-assessment.md).

## <a name="how-do-i-choose-the-assessment-type"></a>Jak wybrać typ oceny?

- Korzystając z **ocen maszyn wirtualnych platformy Azure** , można ocenić lokalne [maszyny wirtualne programu VMware](how-to-set-up-appliance-vmware.md), [maszyny wirtualne funkcji Hyper-V](how-to-set-up-appliance-hyper-v.md)i [serwery fizyczne](how-to-set-up-appliance-physical.md) do migracji na maszyny wirtualne platformy Azure. [Więcej informacji](concepts-assessment-calculation.md)

- Użyj typu oceny **Azure SQL** , jeśli chcesz ocenić SQL Server lokalny ze środowiska VMware w celu migracji do Azure SQL Database lub wystąpienia zarządzanego Azure SQL. [Więcej informacji](concepts-assessment-calculation.md)

    > [!Note]
    > Odnajdywanie i Ocena SQL Server wystąpień i baz danych działających w środowisku VMware jest teraz w wersji zapoznawczej. Aby wypróbować tę funkcję, użyj [**tego linku**](https://aka.ms/AzureMigrate/SQL) , aby utworzyć projekt w regionie **Australia Wschodnia** . Jeśli masz już projekt w Australii wschodniej i chcesz wypróbować tę funkcję, upewnij się, że zostały spełnione [**wymagania wstępne**](how-to-discover-sql-existing-project.md) w portalu.

- Korzystając z funkcji oceny **rozwiązań VMware firmy Azure (Automatyczna synchronizacja)** , możesz ocenić swoje lokalne [maszyny wirtualne VMware](how-to-set-up-appliance-vmware.md) na potrzeby migracji do [rozwiązania Azure VMware (Automatyczna synchronizacja)](../azure-vmware/introduction.md) przy użyciu tego typu oceny. [Dowiedz się więcej](concepts-azure-vmware-solution-assessment-calculation.md)

- Grupy wspólnej można używać z maszynami VMware tylko do uruchamiania obu typów ocen. Jeśli używasz ocen usługi AVS w usłudze Azure Migrate po raz pierwszy, zaleca się utworzenie nowej grupy maszyn VMware.
 

## <a name="why-is-performance-data-missing-for-someall-servers-in-my-azure-vm-andor-avs-assessment-report"></a>Dlaczego brakuje danych dotyczących wydajności dla niektórych/wszystkich serwerów w raporcie na maszynie wirtualnej platformy Azure i/lub w ramach oceny automatycznej synchronizacji?

W przypadku oceny „Na podstawie wydajności” eksport raportu oceny zawiera ciąg „PercentageOfCoresUtilizedMissing” lub „PercentageOfMemoryUtilizedMissing”, gdy urządzenie usługi Azure Migrate nie może zebrać danych wydajności lokalnych maszyn wirtualnych. Sprawdź następujące kwestie:

- Czy maszyny wirtualne są włączone przez czas trwania, dla którego tworzysz ocenę
- Jeśli brakuje tylko liczników pamięci i próbujesz ocenić maszyny wirtualne funkcji Hyper-V. W tym scenariuszu należy włączyć pamięć dynamiczną na maszynach wirtualnych i "ponownie Oblicz" ocenę, aby odzwierciedlić najnowsze zmiany. Urządzenie może zbierać wartości wykorzystania pamięci dla maszyn wirtualnych funkcji Hyper-V tylko wtedy, gdy maszyna wirtualna ma włączoną pamięć dynamiczną.

- Jeśli brakuje wszystkich liczników wydajności, upewnij się, że połączenia wychodzące na portach 443 (HTTPS) są dozwolone.

    > [!Note]
    > Jeśli brakuje któregokolwiek z liczników wydajności, Azure Migrate: Ocena serwera powraca do przyznanych rdzeni/pamięci lokalnie i zaleca odpowiednio rozmiar maszyny wirtualnej.


## <a name="why-is-performance-data-missing-for-someall-sql-instancesdatabases-in-my-azure-sql-assessment"></a>Dlaczego brakuje danych dotyczących wydajności dla niektórych/wszystkich wystąpień lub baz danych SQL w ramach oceny usługi Azure SQL?

Aby zapewnić zbieranie danych dotyczących wydajności, należy sprawdzić:

- Jeśli serwery SQL są włączone na czas trwania tworzenia oceny
- Jeśli stan połączenia agenta programu SQL Server w Azure Migrate to "Connected" i sprawdź ostatni puls 
- Jeśli Azure Migrate stan połączenia dla wszystkich wystąpień SQL ma wartość "Połączono" w bloku odnalezionego wystąpienia programu SQL
- Jeśli brakuje wszystkich liczników wydajności, upewnij się, że połączenia wychodzące na portach 443 (HTTPS) są dozwolone

Jeśli brakuje któregokolwiek z liczników wydajności, usługa Azure SQL Assessment zaleca najmniejszą konfigurację usługi Azure SQL dla tego wystąpienia/bazy danych.

## <a name="why-is-the-confidence-rating-of-my-assessment-low"></a>Dlaczego ocena ufności mojej oceny jest niska?

Ocena ufności dla ocen „Na podstawie wydajności” jest obliczana w oparciu o wartość procentową [dostępnych punktów danych](./concepts-assessment-calculation.md#ratings) potrzebnych do obliczenia oceny. Poniżej przedstawiono przyczyny, z powodu których ocena ufności może być niska:

- Nie profilujesz swojego środowiska przez czas trwania, dla którego tworzysz ocenę. Jeśli na przykład tworzysz ocenę z czasem trwania wydajności ustawionym na jeden tydzień, musisz poczekać co najmniej tydzień po uruchomieniu odnajdywania, aby zebrać wszystkie punkty danych. Jeśli nie można czekać na czas trwania, należy zmienić czas trwania wydajności na mniejszy okres i **ponownie obliczyć** ocenę.
 
- Ocena nie jest w stanie zebrać danych wydajności dla niektórych lub wszystkich serwerów w okresie oceny. W celu uzyskania oceny o wysokiej pewności upewnij się, że: 
    - Serwery są zasilane na czas trwania oceny
    - Połączenia wychodzące na portach 443 są dozwolone
    - W przypadku pamięci dynamicznej na serwerach funkcji Hyper-V jest włączona 
    - Stan połączenia agentów w Azure Migrate to "Połączono" i sprawdź ostatni puls
    - W przypadku usługi Azure SQL Assessment Azure Migrate stan połączenia dla wszystkich wystąpień SQL ma wartość "Połączono" w bloku odnalezionego wystąpienia programu SQL

    **Oblicz ponownie** ocenę, aby odzwierciedlić najnowsze zmiany w klasyfikacji zaufania.

- W przypadku maszyn wirtualnych platformy Azure i ocen dotyczących automatycznej wersji programu po rozpoczęciu odnajdywania zostały utworzone kilka serwerów. Na przykład jeśli tworzysz ocenę dla historii wydajności dla ostatniego miesiąca, ale kilka serwerów zostało utworzonych w środowisku tylko tydzień temu. W takim przypadku dane wydajności dla nowych serwerów nie będą dostępne przez cały czas, a Ocena zaufania byłaby niska. [Dowiedz się więcej](./concepts-assessment-calculation.md#confidence-ratings-performance-based)

- W przypadku ocen usługi Azure SQL utworzono kilka wystąpień SQL lub baz danych po rozpoczęciu odnajdywania. Na przykład jeśli tworzysz ocenę dla historii wydajności dla ostatniego miesiąca, ale kilka wystąpień SQL lub baz danych zostało utworzonych w środowisku tylko tydzień temu. W takim przypadku dane wydajności dla nowych serwerów nie będą dostępne przez cały czas, a Ocena zaufania byłaby niska. [Dowiedz się więcej](./concepts-azure-sql-assessment-calculation.md#confidence-ratings)

## <a name="i-want-to-try-out-the-new-azure-sql-assessment-feature-in-azure-migrate"></a>Chcę wypróbować nową funkcję oceny usługi Azure SQL w Azure Migrate
Aby wypróbować tę funkcję, użyj [tego linku](https://go.microsoft.com/fwlink/?linkid=2155668L) , aby utworzyć projekt w regionie **Australia Wschodnia** .
- Aby rozpocząć, zapoznaj się z samouczkami [odnajdywania](https://docs.microsoft.com/azure/migrate/tutorial-discover-vmware) i [oceny](https://docs.microsoft.com/azure/migrate/tutorial-assess-sql) .
- Należy pamiętać, że odnajdywanie i Ocena wystąpień SQL Server i baz danych działających w środowisku programu VMware jest obecnie dostępna w wersji zapoznawczej.

## <a name="i-cant-see-some-servers-when-i-am-creating-an-azure-sql-assessment"></a>Nie widzę niektórych serwerów podczas tworzenia oceny usługi Azure SQL

- Ocenę usługi Azure SQL można wykonać tylko na serwerach, na których wykryto wystąpienia SQL. Jeśli nie widzisz serwerów i wystąpień programu SQL, które chcesz ocenić, poczekaj chwilę na ukończenie odnajdywania, a następnie utwórz ocenę. 
- Jeśli nie widzisz wcześniej utworzonej grupy podczas tworzenia oceny, Usuń wszystkie serwery inne niż VMware lub dowolny serwer bez wystąpienia SQL z grupy.
- Jeśli korzystasz z funkcji oceny usługi Azure SQL w Azure Migrate po raz pierwszy, zaleca się utworzenie nowej grupy serwerów.

## <a name="i-want-to-understand-how-was-the-readiness-for-my-instance-computed"></a>Chcę zrozumieć, jak była przewidziana gotowość mojego wystąpienia?
Gotowość wystąpień programu SQL została obliczona po sprawdzeniu zgodności funkcji z dodanym typem wdrożenia usługi Azure SQL (Azure SQL Database lub wystąpieniem zarządzanym usługi Azure SQL). [Dowiedz się więcej](./concepts-azure-sql-assessment-calculation.md#calculate-readiness)

## <a name="why-is-the-readiness-for-all-my-sql-instances-marked-as-unknown"></a>Dlaczego gotowość wszystkich wystąpień programu SQL oznaczono jako nieznana?
Jeśli odnajdywanie zostało uruchomione niedawno i nadal trwa, może zostać wyświetlona gotowość dla niektórych lub wszystkich wystąpień SQL jako nieznane. Zalecamy poczekanie przez jakiś czas na przeprofilowanie środowiska przez urządzenie, a następnie ponowne obliczenie oceny.
Funkcja odnajdywania SQL jest przeprowadzana co 24 godziny. może być konieczne odczekanie na dzień, aż najnowsze zmiany konfiguracji zostaną odzwierciedlone. 

## <a name="why-is-the-readiness-for-some-of-my-sql-instances-marked-as-unknown"></a>Dlaczego gotowość dla niektórych wystąpień SQL jest oznaczona jako nieznana?
Może się tak zdarzyć, jeśli: 
- Odnajdywanie jest nadal w toku. Zalecamy poczekanie przez jakiś czas na przeprofilowanie środowiska przez urządzenie, a następnie ponowne obliczenie oceny.
- Istnieją problemy z odnajdywaniem, które należy naprawić w bloku błędy i powiadomienia.

Funkcja odnajdywania SQL jest przeprowadzana co 24 godziny. może być konieczne odczekanie na dzień, aż najnowsze zmiany konfiguracji zostaną odzwierciedlone.

## <a name="my-assessment-is-in-outdated-state"></a>Moja ocena jest w stanie nieaktualnym

### <a name="azure-vmavs-assessment"></a>Ocena maszyn wirtualnych/automatycznej wersji platformy Azure
Jeśli istnieją lokalne zmiany w maszynach wirtualnych, które znajdują się w grupie, która została oceniona, ocena jest oznaczona jako nieaktualna. Ocenę można oznaczyć jako "nieaktualne" z powodu co najmniej jednej zmiany w poniższych właściwościach:
- Liczba rdzeni procesora
- Przydzieloną pamięć
- Typ rozruchu lub oprogramowanie układowe
- Nazwa, wersja i architektura systemu operacyjnego
- Liczba dysków
- Liczba kart sieciowych
- Zmiana rozmiaru dysku (przydzielono GB)
- Aktualizacja właściwości karty sieciowej. Przykład: zmiany adresów MAC, Dodawanie adresów IP itp.

**Oblicz ponownie** ocenę, aby odzwierciedlić najnowsze zmiany w ocenie.

### <a name="azure-sql-assessment"></a>Ocena usługi Azure SQL
Jeśli istnieją zmiany w lokalnych wystąpieniach SQL i bazach danych, które znajdują się w grupie, która została oceniona, ocena jest oznaczona jako **nieaktualna**:
- Wystąpienie SQL zostało dodane lub usunięte z serwera
- Baza danych SQL została dodana lub usunięta z wystąpienia programu SQL Server
- Łączny rozmiar bazy danych w wystąpieniu serwera SQL został zmieniony o ponad 20%
- Zmień liczbę rdzeni procesora i/lub przydzieloną pamięć

**Oblicz ponownie** ocenę, aby odzwierciedlić najnowsze zmiany w ocenie.

## <a name="why-was-i-recommended-a-particular-target-deployment-type"></a>Dlaczego został zalecany określony docelowy typ wdrożenia?
Azure Migrate zaleca określony typ wdrożenia usługi Azure SQL, który jest zgodny z wystąpieniem serwera SQL. Migrowanie do zalecanego elementu docelowego firmy Microsoft zmniejsza ogólny nakład pracy związany z migracją. Ta konfiguracja usługi Azure SQL (SKU) została zalecana po uwzględnieniu charakterystyki wydajności wystąpienia programu SQL i baz danych, którymi zarządza. Jeśli kwalifikują się wiele konfiguracji usługi Azure SQL, zalecamy korzystanie z nich, co jest najbardziej opłacalne. [Dowiedz się więcej](./concepts-azure-sql-assessment-calculation.md#calculate-sizing)

## <a name="what-deployment-target-should-i-choose-if-my-sql-instance-is-ready-for-azure-sql-db-and-azure-sql-mi"></a>Jakiego celu wdrożenia należy wybrać, jeśli moje wystąpienie SQL jest gotowe do używania w usłudze Azure SQL DB i Azure SQL MI? 
Jeśli wystąpienie jest gotowe zarówno do usługi Azure SQL DB, jak i Azure SQL, zalecamy docelowy typ wdrożenia, dla którego jest niższy szacowany koszt konfiguracji usługi Azure SQL.

## <a name="why-is-my-instance-marked-as-potentially-ready-for-azure-vm-in-my-azure-sql-assessment"></a>Dlaczego moje wystąpienie jest oznaczone jako potencjalnie gotowe dla maszyny wirtualnej platformy Azure w ramach oceny usługi Azure SQL?
Może się tak zdarzyć, gdy docelowy typ wdrożenia wybrany we właściwościach oceny jest **zalecany** i wystąpienie programu SQL Server nie jest gotowe do Azure SQL Database i wystąpienia zarządzanego Azure SQL. Aby określić, czy serwer, na którym uruchomiono wystąpienie, jest gotowy do migracji na maszynę wirtualną platformy Azure, zaleca się utworzenie oceny migracji platformy Azure z typem oceny jako **maszyny wirtualnej platformy** Azure.
Zaleca się utworzenie oceny w Azure Migrate z typem oceny jako **maszyną wirtualną platformy Azure** w celu ustalenia, czy serwer, na którym uruchomiono wystąpienie, jest gotowy do migracji na maszynę wirtualną platformy Azure:
- Oceny maszyn wirtualnych platformy Azure w Azure Migrate są obecnie zniesione i przenoszone i nie uwzględniają określonych metryk wydajności związanych z uruchamianiem wystąpień SQL i baz danych na maszynie wirtualnej platformy Azure. 
- Po uruchomieniu oceny maszyny wirtualnej platformy Azure na serwerze zalecany rozmiar i szacunkowy koszt będą dotyczyć wszystkich wystąpień uruchomionych na serwerze i można je migrować na maszynę wirtualną platformy Azure przy użyciu narzędzia do migracji serwera. Przed [przeprowadzeniem migracji zapoznaj się z zaleceniami](https://docs.microsoft.com/azure/azure-sql/virtual-machines/windows/performance-guidelines-best-practices) dotyczącymi wydajności SQL Server w usłudze Azure Virtual Machines.

## <a name="i-cant-see-some-databases-in-my-assessment-even-though-the-instance-is-part-of-the-assessment"></a>Nie widzę niektórych baz danych w mojej ocenie, mimo że wystąpienie jest częścią oceny

Ocena usługi Azure SQL obejmuje tylko bazy danych znajdujące się w stanie online. W przypadku, gdy baza danych znajduje się w innym stanie, ocena jest ignorowana pod kątem gotowości, wielkości i obliczeń kosztów dla takich baz danych. Jeśli chcesz ocenić te bazy danych, Zmień stan bazy danych i ponownie Oblicz ocenę w pewnym czasie.

## <a name="i-want-to-compare-costs-for-running-my-sql-instances-on-azure-vm-vs-azure-sql-databaseazure-sql-managed-instance"></a>Chcę porównać koszty uruchamiania wystąpień programu SQL na maszynie wirtualnej platformy Azure a Azure SQL Database/wystąpienia zarządzanego Azure SQL

Można utworzyć ocenę przy użyciu typu **maszyny wirtualnej platformy Azure** w tej samej grupie, która została użyta w ramach oceny **usługi Azure SQL** . Następnie można porównać te dwa raporty obok siebie. Mimo że oceny maszyn wirtualnych platformy Azure w Azure Migrate są obecnie przyłączone i przenoszone i nie będzie uwzględniać określonych metryk wydajności dotyczących uruchamiania wystąpień SQL i baz danych na maszynie wirtualnej platformy Azure. Po uruchomieniu oceny maszyny wirtualnej platformy Azure na serwerze zalecany rozmiar i szacunkowy koszt będą dotyczyć wszystkich wystąpień uruchomionych na serwerze i można je migrować na maszynę wirtualną platformy Azure przy użyciu narzędzia do migracji serwera. Przed [przeprowadzeniem migracji zapoznaj się z zaleceniami](https://docs.microsoft.com/azure/azure-sql/virtual-machines/windows/performance-guidelines-best-practices) dotyczącymi wydajności SQL Server w usłudze Azure Virtual Machines.

## <a name="the-storage-cost-in-my-azure-sql-assessment-is-zero"></a>Koszt magazynu w ramach oceny usługi Azure SQL jest równy zero
W przypadku wystąpienia zarządzanego usługi Azure SQL nie dodaliśmy kosztu magazynu dla pierwszego magazynu 32 GB/wystąpienia/miesiąca, a dodatkowy koszt magazynu jest dodawany do magazynu w przyrostach 32 GB. [Więcej informacji](https://azure.microsoft.com/pricing/details/azure-sql/sql-managed-instance/single/)

## <a name="i-cant-see-some-groups-when-i-am-creating-an-azure-vmware-solution-avs-assessment"></a>Nie widzę niektórych grup podczas tworzenia rozwiązania Azure VMware (Automatyczna synchronizacja)

- Ocenę usługi AVS można przeprowadzić w grupach, które mają tylko maszyny VMware. Jeśli zamierzasz przeprowadzić ocenę usługi AVS, usuń z grupy wszystkie maszyny inne niż VMware.
- Jeśli używasz ocen usługi AVS w usłudze Azure Migrate po raz pierwszy, zaleca się utworzenie nowej grupy maszyn VMware.

## <a name="i-cant-see-some-vm-types-in-azure-government"></a>Nie widzę niektórych typów maszyn wirtualnych w Azure Government

Typy maszyn wirtualnych obsługiwane na potrzeby oceny i migracji zależą od dostępności w Azure Government lokalizacji. Możesz [przejrzeć i porównać](https://azure.microsoft.com/global-infrastructure/services/?regions=usgov-non-regional,us-dod-central,us-dod-east,usgov-arizona,usgov-iowa,usgov-texas,usgov-virginia&products=virtual-machines) typy maszyn wirtualnych w Azure Government.

## <a name="the-size-of-my-vm-changed-can-i-run-an-assessment-again"></a>Zmieniono rozmiar maszyny wirtualnej. Czy mogę ponownie uruchomić ocenę?

Urządzenie Azure Migrate ciągle zbiera informacje o środowisku lokalnym.  Ocena to migawka lokalnych maszyn wirtualnych do określonego momentu. Jeśli zmienisz ustawienia na maszynie wirtualnej, która ma zostać oceniona, użyj opcji Oblicz ponownie, aby zaktualizować ocenę przy użyciu najnowszych zmian.

## <a name="how-do-i-discover-vms-in-a-multitenant-environment"></a>Jak mogę odnajdywania maszyn wirtualnych w środowisku wielodostępnym?

- **VMware**: Jeśli środowisko jest współużytkowane przez dzierżawców i nie chcesz odnajdywać maszyn wirtualnych dzierżawy w ramach subskrypcji innej dzierżawy, Utwórz VMware vCenter Server poświadczenia, które mogą uzyskiwać dostęp tylko do maszyn wirtualnych, które chcesz odnajdywać. Następnie użyj tych poświadczeń po rozpoczęciu odnajdywania na urządzeniu Azure Migrate.
- **Funkcja Hyper-v**: odnajdywanie używa poświadczeń hosta funkcji Hyper-v. Jeśli maszyny wirtualne korzystają z tego samego hosta funkcji Hyper-V, nie ma możliwości oddzielenia odnajdywania.  

## <a name="do-i-need-vcenter-server"></a>Czy potrzebuję vCenter Server?

Tak, Azure Migrate wymaga vCenter Server w środowisku VMware w celu przeprowadzenia odnajdywania. Azure Migrate nie obsługuje odnajdywania hostów ESXi, które nie są zarządzane przez vCenter Server.

## <a name="what-are-the-sizing-options-in-an-azure-vm-assessment"></a>Jakie są opcje ustalania wielkości w ocenie maszyny wirtualnej platformy Azure?

W przypadku ustalania rozmiarów lokalnych Azure Migrate nie uwzględnia danych wydajności maszyny wirtualnej w celu oceny. Azure Migrate ocenia rozmiary maszyn wirtualnych na podstawie konfiguracji lokalnej. W przypadku ustalania rozmiarów na podstawie wydajności rozmiar jest oparty na danych użycia.

Na przykład jeśli lokalna maszyna wirtualna ma cztery rdzenie i 8 GB pamięci na 50% użycia procesora CPU i 50% wykorzystania pamięci:
- Ustalanie rozmiarów lokalnych będzie zalecane dla jednostki SKU maszyny wirtualnej platformy Azure, która ma cztery rdzenie i 8 GB pamięci.
- Ustalanie wielkości na podstawie wydajności spowoduje zalecanie jednostki SKU maszyny wirtualnej, która ma dwa rdzenie i 4 GB pamięci, ponieważ jest brana pod uwagę procent użycia.

Podobnie rozmiary dysku są zależne od kryteriów ustalania rozmiarów i typu magazynu:
- Jeśli kryteria ustalania wielkości są oparte na wydajności i typ magazynu jest automatyczny, Azure Migrate pobiera wartości IOPS i przepływności dysku do konta, gdy identyfikuje docelowy typ dysku (standardowa lub Premium).
- Jeśli kryterium ustalania rozmiaru jest oparte na wydajności, a typ magazynu to Premium, Azure Migrate zaleca SKU dysku w warstwie Premium na podstawie rozmiaru dysku lokalnego. Ta sama logika jest stosowana do wielkości dysku, gdy wielkość liter jest jako lokalna, a typ magazynu to standardowa lub Premium.

## <a name="does-performance-history-and-utilization-affect-sizing-in-an-azure-vm-assessment"></a>Czy historia wydajności i wykorzystanie wpływają na zmianę rozmiarów w ramach oceny maszyny wirtualnej platformy Azure?

Tak, historia wydajności i wykorzystanie wpływają na rozmiar w ocenie maszyny wirtualnej platformy Azure.

### <a name="performance-history"></a>Historia wydajności

W przypadku tylko ustalania rozmiaru na podstawie wydajności Azure Migrate zbiera historię wydajności maszyn lokalnych, a następnie używa jej w celu zaproponowania rozmiaru maszyny wirtualnej i typu dysku na platformie Azure:

1. Urządzenie nieustannie profiluje środowisko lokalne, aby gromadzić dane dotyczące użycia w czasie rzeczywistym co 20 sekund.
2. Urządzenie zbiera zebrane 20-sekundowe próbki i używa ich do tworzenia jednego punktu danych co 15 minut.
3. Aby utworzyć punkt danych, urządzenie wybiera wartość szczytu ze wszystkich próbek 20-sekund.
4. Urządzenie wysyła punkt danych do platformy Azure.

### <a name="utilization"></a>Wykorzystanie

Po utworzeniu oceny na platformie Azure, w zależności od czasu trwania wydajności i wartości percentylu historii wydajności, która jest ustawiona, Azure Migrate oblicza wartość efektywnego wykorzystania, a następnie używa jej do ustalania rozmiarów.

Na przykład jeśli ustawisz czas trwania wydajności na jeden dzień i wartość percentylu na używany 95. percentyl, Azure Migrate sortuje 15-minutowe punkty próbkowania wysyłane przez moduł zbierający dla ostatniego dnia w kolejności rosnącej. Wybiera wartość percentylu używany 95. jako efektywne wykorzystanie.

Użycie wartości percentylu używany 95. gwarantuje, że elementy odstające są ignorowane. Elementy odstające mogą być dołączane, jeśli Azure Migrate używa percentylu 99. Aby wybrać szczytowe użycie dla tego okresu bez braku żadnych wartości odstających, ustaw Azure Migrate na użycie 99 percentyl.


## <a name="how-are-import-based-assessments-different-from-assessments-with-discovery-source-as-appliance"></a>Jak są oceniane oceny oparte na imporcie, które różnią się od ocen ze źródłem odnajdywania jako urządzenie?

Oparte na imporcie oceny maszyn wirtualnych platformy Azure są ocenami utworzonymi w przypadku maszyn zaimportowanych do Azure Migrate przy użyciu pliku CSV. Tylko cztery pola są wymagane do zaimportowania: Nazwa serwera, rdzenie, pamięć i system operacyjny. Poniżej przedstawiono kilka kwestii, które należy zwrócić uwagę: 
 - Kryteria gotowości są mniej rygorystyczne w przypadku ocen opartych na imporcie w parametrze typu rozruchu. Jeśli typ rozruchu nie zostanie podany, zakłada się, że maszyna ma typ rozruchu w systemie BIOS, a maszyna nie jest oznaczona jako **warunkowo gotowa**. W obszarze oceny ze źródłem odnajdywania jako urządzenie gotowość jest oznaczona jako **warunkowo gotowa** , jeśli brakuje typu rozruchu. Różnica w obliczaniu gotowości wynika z faktu, że użytkownicy mogą nie mieć wszystkich informacji na maszynach na wczesnych etapach planowania migracji w przypadku wykonywania ocen opartych na imporcie. 
 - Oceny importowe oparte na wydajności używają wartości wykorzystania dostarczonej przez użytkownika do obliczeń o odpowiednim wymiarze. Ponieważ wartość użycia jest dostarczana przez użytkownika, w oknie właściwości oceny są wyłączone opcje **historia wydajności** i **użycie percentylu** . W obszarze oceny ze źródłem odnajdywania jako urządzenie wybrana wartość percentylu jest wybierana z danych wydajności zbieranych przez urządzenie.

## <a name="why-is-the-suggested-migration-tool-in-import-based-avs-assessment-marked-as-unknown"></a>Dlaczego sugerowane narzędzie do migracji w ramach oceny automatycznej synchronizacji opartej na imporcie zostało oznaczone jako nieznane?

W przypadku maszyn zaimportowanych za pośrednictwem pliku CSV domyślne narzędzie do migracji jest nieznane. Mimo że w przypadku maszyn VMware zaleca się korzystanie z rozwiązania VMware hybryd Cloud Extension (HCX). [Dowiedz się więcej](../azure-vmware/tutorial-deploy-vmware-hcx.md).


## <a name="what-is-dependency-visualization"></a>Co to jest Wizualizacja zależności?

Wizualizacja zależności może pomóc ocenić grupy maszyn wirtualnych do migracji z większą pewnością. Wizualizacja między różnymi kontrolami zależności maszyn przed uruchomieniem oceny. Pozwala to zagwarantować, że nic nie pozostanie w tle i pomaga uniknąć nieoczekiwanego przestoju podczas migracji na platformę Azure. Azure Migrate używa rozwiązania Service Map w Azure Monitor, aby włączyć wizualizację zależności. [Dowiedz się więcej](concepts-dependency-visualization.md).

> [!NOTE]
> Analiza zależności oparta na agentach nie jest dostępna w Azure Government. Można użyć analizy zależności bez agenta

## <a name="whats-the-difference-between-agent-based-and-agentless"></a>Jaka jest różnica między opartymi na agentach i bez wykorzystania agentów?

Różnice między wizualizacją bez agenta i wizualizacją opartą na agentach zostały podsumowane w tabeli.

**Wymaganie** | **Bez agenta** | **Na podstawie agenta**
--- | --- | ---
Pomoc techniczna | Ta opcja jest obecnie w wersji zapoznawczej i jest dostępna tylko dla maszyn wirtualnych VMware. [Przejrzyj](migrate-support-matrix-vmware.md#dependency-analysis-requirements-agentless) obsługiwane systemy operacyjne. | Ogólnie dostępna.
Agent | Nie trzeba instalować agentów na maszynach, które mają być sprawdzane krzyżowo. | Agenci do zainstalowania na każdej maszynie lokalnej, którą chcesz analizować: [program Microsoft Monitoring Agent (MMA)](../azure-monitor/agents/agent-windows.md)i [Agent zależności](../azure-monitor/agents/agents-overview.md#dependency-agent). 
Wymagania wstępne | [Zapoznaj](concepts-dependency-visualization.md#agentless-analysis) się z wymaganiami dotyczącymi wymagań wstępnych i wdrażania. | [Zapoznaj](concepts-dependency-visualization.md#agent-based-analysis) się z wymaganiami dotyczącymi wymagań wstępnych i wdrażania.
Log Analytics | Niewymagane. | Azure Migrate używa rozwiązania [Service map](../azure-monitor/vm/service-map.md) w [dziennikach Azure monitor](../azure-monitor/logs/log-query-overview.md) na potrzeby wizualizacji zależności. [Dowiedz się więcej](concepts-dependency-visualization.md#agent-based-analysis).
Jak to działa | Przechwytuje dane połączenia TCP na maszynach z włączoną funkcją wizualizacji zależności. Po odnajdywaniu dane są zbierane w odstępach pięciu minut. | Service Map agenci zainstalowani na komputerze zbierają dane dotyczące procesów TCP oraz połączeń przychodzących/wychodzących dla każdego procesu.
Dane | Nazwa serwera źródłowego, proces, nazwa aplikacji.<br/><br/> Nazwa serwera maszyny docelowej, proces, nazwa aplikacji i port. | Nazwa serwera źródłowego, proces, nazwa aplikacji.<br/><br/> Nazwa serwera maszyny docelowej, proces, nazwa aplikacji i port.<br/><br/> Liczba połączeń, opóźnień i informacji o przesyłaniu danych jest zbieranych i dostępnych dla zapytań Log Analytics. 
Wizualizacja | Mapę zależności pojedynczego serwera można wyświetlać w czasie trwania z przedziału od godziny do 30 dni. | Mapa zależności pojedynczego serwera.<br/><br/> Mapę można wyświetlać tylko w ciągu godziny.<br/><br/> Mapa zależności grupy serwerów.<br/><br/> Dodawanie i usuwanie serwerów w grupie z widoku mapy.
Eksport danych | Dane z ostatnich 30 dni można pobrać w formacie CSV. | Dane można badać przy użyciu Log Analytics.


## <a name="do-i-need-to-deploy-the-appliance-for-agentless-dependency-analysis"></a>Czy muszę wdrożyć urządzenie na potrzeby analizy zależności bez agentów?

Tak, należy wdrożyć [urządzenie Azure Migrate](migrate-appliance.md) .

## <a name="do-i-pay-for-dependency-visualization"></a>Czy płacisz za wizualizację zależności?

Nie. Dowiedz się więcej o [cenach Azure Migrate](https://azure.microsoft.com/pricing/details/azure-migrate/).

## <a name="what-do-i-install-for-agent-based-dependency-visualization"></a>Co należy zainstalować dla wizualizacji zależności opartej na agentach?

Aby użyć wizualizacji zależności opartej na agentach, Pobierz i zainstaluj agentów na każdej maszynie lokalnej, którą chcesz oszacować:

- [Microsoft Monitoring Agent (MMA)](../azure-monitor/agents/agent-windows.md)
- [Agent zależności](../azure-monitor/agents/agents-overview.md#dependency-agent)
- Jeśli masz maszyny, które nie mają łączności z Internetem, Pobierz i zainstaluj na nich bramę Log Analytics.

Te agenci są potrzebne tylko wtedy, gdy jest używana Wizualizacja zależności oparta na agentach.

## <a name="can-i-use-an-existing-workspace"></a>Czy mogę użyć istniejącego obszaru roboczego?

Tak, w przypadku wizualizacji zależności opartej na agentach można dołączyć istniejący obszar roboczy do projektu migracji i użyć go do wizualizacji zależności. 

## <a name="can-i-export-the-dependency-visualization-report"></a>Czy można wyeksportować raport wizualizacji zależności?

Nie, nie można wyeksportować raportu wizualizacji zależności w wizualizacji opartej na agentach. Jednak Azure Migrate używa Service Map i można użyć [interfejsu API REST Service map](/rest/api/servicemap/machines/listconnections) do pobrania zależności w formacie JSON.

## <a name="can-i-automate-agent-installation"></a>Czy można zautomatyzować instalację agenta?

Dla wizualizacji zależności opartej na agentach:

- [Zainstaluj agenta zależności](../azure-monitor/vm/vminsights-enable-hybrid.md#dependency-agent)przy użyciu skryptu.
- W przypadku MMA należy [użyć wiersza polecenia lub automatyzacji](../azure-monitor/agents/log-analytics-agent.md#installation-options)lub użyć [skryptu](https://gallery.technet.microsoft.com/scriptcenter/Install-OMS-Agent-with-2c9c99ab).
- Oprócz skryptów można użyć narzędzi wdrażania, takich jak Microsoft Endpoint Configuration Manager i [Intigua](https://www.intigua.com/intigua-for-azure-migration) , aby wdrożyć agentów.

## <a name="what-operating-systems-does-mma-support"></a>Jakie systemy operacyjne są obsługiwane przez MMA?

- Zapoznaj się z listą [systemów operacyjnych Windows obsługiwanych przez program MMA](../azure-monitor/agents/log-analytics-agent.md#installation-options).
- Zapoznaj się z listą [systemów operacyjnych Linux obsługiwanych przez program MMA](../azure-monitor/agents/log-analytics-agent.md#installation-options).

## <a name="can-i-visualize-dependencies-for-more-than-one-hour"></a>Czy mogę wizualizować zależności przez więcej niż godzinę?

W przypadku wizualizacji opartej na agentach można wizualizować zależności przez maksymalnie jedną godzinę. Można wrócić o jeden miesiąc do określonej daty w historii, ale maksymalny czas trwania wizualizacji wynosi godzinę. Na przykład można użyć czasu trwania w mapie zależności, aby wyświetlić zależności dla wczoraj, ale można wyświetlić zależności tylko dla jednogodzinnego okna. Można jednak użyć dzienników Azure Monitor do [wykonywania zapytań o dane zależności](./how-to-create-group-machine-dependencies.md) przez dłuższy czas.

W przypadku wizualizacji bez wykorzystania agentów można wyświetlić mapę zależności pojedynczego serwera od czasu trwania z przedziału od 1 godziny do 30 dni.

## <a name="can-i-visualize-dependencies-for-groups-of-more-than-10-vms"></a>Czy mogę wizualizować zależności dla grup o więcej niż 10 maszynach wirtualnych?

Możesz [wizualizować zależności](./how-to-create-a-group.md#refine-a-group-with-dependency-mapping) dla grup, które mają maksymalnie 10 maszyn wirtualnych. Jeśli masz grupę, która ma więcej niż 10 maszyn wirtualnych, zalecamy podział grupy do mniejszych grup, a następnie wizualizację zależności.

## <a name="next-steps"></a>Następne kroki

Zapoznaj się z [omówieniem Azure Migrate](migrate-services-overview.md).