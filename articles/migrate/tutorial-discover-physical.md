---
title: Odnajdywanie serwerów fizycznych za pomocą oceny serwera Azure Migrate
description: Dowiedz się, jak odnajdywać lokalne serwery fizyczne przy użyciu oceny serwera Azure Migrate.
author: vineetvikram
ms.author: vivikram
ms.manager: abhemraj
ms.topic: tutorial
ms.date: 09/14/2020
ms.custom: mvc
ms.openlocfilehash: 1263bc3ffe18aa951b3e5b61747c889d36acbab1
ms.sourcegitcommit: ea551dad8d870ddcc0fee4423026f51bf4532e19
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/07/2020
ms.locfileid: "96752817"
---
# <a name="tutorial-discover-physical-servers-with-server-assessment"></a>Samouczek: odnajdywanie serwerów fizycznych za pomocą oceny serwera

W ramach przeprowadzonej migracji na platformę Azure można odnaleźć serwery do oceny i migracji.

W tym samouczku pokazano, jak odnajdywać lokalne serwery fizyczne przy użyciu Azure Migrate: narzędzia do oceny serwera za pomocą urządzenia uproszczonego Azure Migrate. Urządzenie jest wdrażane jako serwer fizyczny w celu ciągłego odnajdywania metadanych maszyn i wydajności.

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Skonfiguruj konto platformy Azure.
> * Przygotuj serwery fizyczne do odnajdowania.
> * Tworzenie projektu w usłudze Azure Migrate.
> * Skonfiguruj urządzenie Azure Migrate.
> * Rozpocznij odnajdowanie ciągłe.

> [!NOTE]
> Samouczki pokazują najszybszą ścieżkę w celu wypróbowania scenariusza i używają opcji domyślnych.  

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem tego samouczka zapoznaj się z wymaganiami wstępnymi.

**Wymaganie** | **Szczegóły**
--- | ---
**Wprowadzony** | Potrzebna jest maszyna, na której będzie uruchamiane urządzenie Azure Migrate. Maszyna powinna mieć następujące:<br/><br/> — Zainstalowano system Windows Server 2016. _(Obecnie wdrożenie urządzenia jest obsługiwane tylko w systemie Windows Server 2016)._<br/><br/> -16 GB pamięci RAM, 8 procesorów wirtualnych vCPU, około 80 GB miejsca na dysku<br/><br/> — Statyczny lub dynamiczny adres IP, z dostępem do Internetu, bezpośrednio lub za pomocą serwera proxy.
**Serwery z systemem Windows** | Zezwalaj na połączenia przychodzące na porcie WinRM 5985 (HTTP), aby urządzenie mogły ściągnąć konfigurację i metadane wydajności.
**Serwery z systemem Linux** | Zezwalaj na połączenia przychodzące na porcie 22 (TCP).

## <a name="prepare-an-azure-user-account"></a>Przygotowywanie konta użytkownika platformy Azure

Aby utworzyć projekt Azure Migrate i zarejestrować urządzenie Azure Migrate, musisz mieć konto z:
- Uprawnienia współautora lub właściciela w ramach subskrypcji platformy Azure.
- Uprawnienia do rejestrowania aplikacji Azure Active Directory.

Jeśli bezpłatne konto platformy Azure zostało właśnie utworzone, jesteś właścicielem subskrypcji. Jeśli nie jesteś właścicielem subskrypcji, Pracuj z właścicielem, aby przypisać uprawnienia w następujący sposób:

1. W Azure Portal Wyszukaj "subskrypcje", a w obszarze **usługi** wybierz pozycję **subskrypcje**.

    ![Wyszukaj w polu wyszukiwania subskrypcję platformy Azure](./media/tutorial-discover-physical/search-subscription.png)

2. Na stronie **subskrypcje** wybierz subskrypcję, w której chcesz utworzyć projekt Azure Migrate. 
3. W subskrypcji wybierz pozycję **Kontrola dostępu (IAM)**  >  **sprawdzanie dostępu**.
4. W obszarze **Sprawdź dostęp** Wyszukaj odpowiednie konto użytkownika.
5. W obszarze **Dodaj przypisanie roli** kliknij pozycję **Dodaj**.

    ![Wyszukaj konto użytkownika, aby sprawdzić dostęp i przypisać rolę](./media/tutorial-discover-physical/azure-account-access.png)

6. W obszarze **Dodaj przypisanie roli** wybierz rolę współautor lub właściciela, a następnie wybierz konto (azmigrateuser w naszym przykładzie). Następnie kliknij przycisk **Zapisz**.

    ![Otwiera stronę Dodawanie przypisania roli w celu przypisania roli do konta](./media/tutorial-discover-physical/assign-role.png)

7. W portalu Wyszukaj użytkowników, a w obszarze **usługi** wybierz pozycję **Użytkownicy**.
8. W obszarze **Ustawienia użytkownika** Sprawdź, czy użytkownicy usługi Azure AD mogą rejestrować aplikacje (domyślnie ustawione na **wartość tak** ).

    ![Sprawdź ustawienia użytkownika, które użytkownicy mogą rejestrować Active Directory aplikacje](./media/tutorial-discover-physical/register-apps.png)

9. Alternatywnie, dzierżawa/Administrator globalny może przypisać rolę **dewelopera aplikacji** do konta, aby umożliwić rejestrację aplikacji usługi AAD. [Dowiedz się więcej](../active-directory/fundamentals/active-directory-users-assign-role-azure-portal.md).

## <a name="prepare-physical-servers"></a>Przygotuj serwery fizyczne

Skonfiguruj konto, za pomocą którego urządzenie może uzyskać dostęp do serwerów fizycznych.

- W przypadku serwerów z systemem Windows należy użyć konta domeny dla komputerów przyłączonych do domeny oraz konta lokalnego dla maszyn, które nie są przyłączone do domeny. Konto użytkownika należy dodać do tych grup: Użytkownicy zarządzania zdalnego, użytkownicy monitora wydajności i Użytkownicy dzienników wydajności.
- W przypadku serwerów systemu Linux potrzebujesz konta głównego na serwerach systemu Linux, które mają być odnajdywane. Alternatywnie można ustawić konto inne niż główne z wymaganymi możliwościami przy użyciu następujących poleceń:

**Polecenie** | **Cel**
--- | --- |
setcap CAP_DAC_READ_SEARCH + EIP/usr/sbin/fdisk <br></br> setcap CAP_DAC_READ_SEARCH + EIP/sbin/fdisk _(jeśli/usr/sbin/fdisk nie istnieje)_ | Aby zebrać dane konfiguracji dysku
setcap cap_dac_override, cap_dac_read_search, cap_fowner, cap_fsetid, cap_setuid,<br>cap_setpcap, cap_net_bind_service, cap_net_admin, cap_sys_chroot, cap_sys_admin,<br>cap_sys_resource, cap_audit_control, cap_setfcap = + EIP "/sbin/LVM | Aby zebrać dane o wydajności dysku
setcap CAP_DAC_READ_SEARCH + EIP/usr/sbin/dmidecode | Aby zebrać numer seryjny systemu BIOS
chmod a + r/sys/Class/DMI/ID/product_uuid | Aby zebrać identyfikator GUID systemu BIOS


## <a name="set-up-a-project"></a>Konfigurowanie projektu

Skonfiguruj nowy projekt Azure Migrate.

1. W witrynie Azure Portal > **Wszystkie usługi** znajdź pozycję **Azure Migrate**.
2. W obszarze **Usługi** wybierz pozycję **Azure Migrate**.
3. W obszarze **Przegląd** wybierz pozycję **Utwórz projekt**.
5. W obszarze **Utwórz projekt** wybierz swoją subskrypcję platformy Azure i grupę zasobów. Utwórz grupę zasobów, jeśli jej nie masz.
6. W obszarze **szczegóły projektu** Określ nazwę projektu i geografię, w której chcesz utworzyć projekt. Przejrzyj obsługiwane lokalizacje geograficzne dla chmur [publicznych](migrate-support-matrix.md#supported-geographies-public-cloud) i [instytucji rządowych](migrate-support-matrix.md#supported-geographies-azure-government).

   ![Pola nazwy i regionu projektu](./media/tutorial-discover-physical/new-project.png)

7. Wybierz przycisk **Utwórz**.
8. Zaczekaj kilka minut, aż projekt usługi Azure Migrate zostanie wdrożony.

**Azure Migrate: Narzędzie do oceny serwera** jest domyślnie dodawane do nowego projektu.

![Zostanie wyświetlona strona narzędzia do oceny serwera, która jest domyślnie dodawana](./media/tutorial-discover-physical/added-tool.png)


## <a name="set-up-the-appliance"></a>Konfigurowanie urządzenia

Aby skonfigurować urządzenie:
- Podaj nazwę urządzenia i Wygeneruj klucz projektu Azure Migrate w portalu.
- Pobierz spakowany plik ze skryptem Instalatora Azure Migrate z Azure Portal.
- Wyodrębnij zawartość z pliku spakowanego. Uruchom konsolę programu PowerShell z uprawnieniami administracyjnymi.
- Wykonaj skrypt programu PowerShell, aby uruchomić aplikację sieci Web urządzenia.
- Skonfiguruj urządzenie po raz pierwszy i zarejestruj je w projekcie Azure Migrate przy użyciu klucza projektu Azure Migrate.

### <a name="generate-the-azure-migrate-project-key"></a>Generowanie klucza projektu Azure Migrate

1. W obszarze **Cele migracji** > **Serwery** > **Azure Migrate: Server Assessment** wybierz pozycję **Odnajdź**.
2. W obszarze **odnajdywanie** maszyn  >  **są zwirtualizowane maszyny?** wybierz pozycję **fizyczne lub inne (AWS, GCP, Xen itp.)**.
3. W obszarze **1: generowanie klucza projektu Azure Migrate** Podaj nazwę urządzenia Azure Migrate, które zostanie skonfigurowane do odnajdywania serwerów fizycznych lub wirtualnych. Nazwa powinna być alfanumeryczna z 14 znakami lub mniej.
1. Kliknij pozycję **Generuj klucz** , aby rozpocząć tworzenie wymaganych zasobów platformy Azure. Nie zamykaj strony odnajdywanie maszyn podczas tworzenia zasobów.
1. Po pomyślnym utworzeniu zasobów platformy Azure zostanie wygenerowany **klucz projektu Azure Migrate** .
1. Skopiuj klucz, ponieważ będzie on potrzebny do ukończenia rejestracji urządzenia podczas jego konfiguracji.

### <a name="download-the-installer-script"></a>Pobierz skrypt Instalatora

W **2: Pobierz urządzenie Azure Migrate**, kliknij pozycję **Pobierz**.


### <a name="verify-security"></a>Weryfikuj zabezpieczenia

Przed wdrożeniem należy sprawdzić, czy spakowany plik jest bezpieczny.

1. Na maszynie, na którą pobrano plik, otwórz okno wiersza polecenia administratora.
2. Uruchom następujące polecenie, aby wygenerować skrót dla pliku spakowanego:
    - ```C:\>CertUtil -HashFile <file_location> [Hashing Algorithm]```
    - Przykładowe użycie chmury publicznej: ```C:\>CertUtil -HashFile C:\Users\administrator\Desktop\AzureMigrateInstaller-Server-Public.zip SHA256 ```
    - Przykładowe użycie w chmurze dla instytucji rządowych: ```  C:\>CertUtil -HashFile C:\Users\administrator\Desktop\AzureMigrateInstaller-Server-USGov.zip SHA256 ```
3.  Sprawdź najnowsze wersje urządzeń i wartości skrótu:
    - W przypadku chmury publicznej:

        **Scenariusz** | **Pobierz** _ | _ *Wartość skrótu**
        --- | --- | ---
        Fizyczne (85,8 MB) | [Najnowsza wersja](https://go.microsoft.com/fwlink/?linkid=2140334) | ce5e6f0507936def8020eb7b3109173dad60fc51dd39c3bd23099bc9baaabe29

    - Dla Azure Government:

        **Scenariusz** | **Pobierz** _ | _ *Wartość skrótu**
        --- | --- | ---
        Fizyczne (85,8 MB) | [Najnowsza wersja](https://go.microsoft.com/fwlink/?linkid=2140338) | ae132ebc574caf231bf41886891040ffa7abbe150c8b50436818b69e58622276
 

### <a name="run-the-azure-migrate-installer-script"></a>Uruchom skrypt Instalatora Azure Migrate
Skrypt Instalatora wykonuje następujące czynności:

- Instaluje agentów i aplikację sieci Web na potrzeby odnajdywania i oceny serwera fizycznego.
- Zainstaluj role systemu Windows, w tym usługi aktywacji systemu Windows, usług IIS i programu PowerShell ISE.
- Pobierz i zainstaluj moduł, który ma zostać przezapisywalny usług IIS. [Dowiedz się więcej](https://www.microsoft.com/download/details.aspx?id=7435).
- Aktualizuje klucz rejestru (HKLM) z trwałymi ustawieniami ustawień dla Azure Migrate.
- Tworzy następujące pliki w ścieżce:
    - **Pliki konfiguracji**:%ProgramData%\Microsoft Azure\Config
    - **Pliki dziennika**:%ProgramData%\Microsoft Azure\Logs

Uruchom skrypt w następujący sposób:

1. Wyodrębnij spakowany plik do folderu na serwerze, który będzie hostować urządzenie.  Upewnij się, że skrypt nie jest uruchamiany na komputerze na istniejącym urządzeniu Azure Migrate.
2. Uruchom program PowerShell na powyższym serwerze z uprawnieniami administracyjnymi (z podwyższonym poziomem uprawnień).
3. Zmień katalog programu PowerShell do folderu, w którym zawartość została wyodrębniona z pobranego pliku spakowanego.
4. Uruchom skrypt o nazwie **AzureMigrateInstaller.ps1** , uruchamiając następujące polecenie:

    - W przypadku chmury publicznej: 
    
        ``` PS C:\Users\administrator\Desktop\AzureMigrateInstaller-Server-Public> .\AzureMigrateInstaller.ps1 ```
    - Dla Azure Government: 
    
        ``` PS C:\Users\Administrators\Desktop\AzureMigrateInstaller-Server-USGov>.\AzureMigrateInstaller.ps1 ```

    Po pomyślnym zakończeniu działania skryptu zostanie uruchomiona aplikacja sieci Web urządzenia.

Jeśli występują problemy, możesz uzyskać dostęp do dzienników skryptów w witrynie C:\ProgramData\Microsoft Azure\Logs\ AzureMigrateScenarioInstaller_<em>timestamp</em>. log w celu rozwiązywania problemów.



### <a name="verify-appliance-access-to-azure"></a>Weryfikowanie dostępu urządzenia do platformy Azure

Upewnij się, że maszyna wirtualna urządzenia może połączyć się z adresami URL platformy Azure dla chmur [publicznych](migrate-appliance.md#public-cloud-urls) i dla [instytucji rządowych](migrate-appliance.md#government-cloud-urls) .

### <a name="configure-the-appliance"></a>Konfigurowanie urządzenia

Skonfiguruj urządzenie po raz pierwszy.

1. Otwórz przeglądarkę na dowolnym komputerze, który może nawiązać połączenie z urządzeniem, a następnie otwórz adres URL aplikacji sieci Web urządzenia: **https://*Nazwa urządzenia lub adres IP*: 44368**.

   Możesz też otworzyć aplikację z poziomu pulpitu, klikając skrót do aplikacji.
2. Zaakceptuj **postanowienia licencyjne** i przeczytaj informacje o innych firmach.
1. W aplikacji internetowej > **skonfigurować wymagania wstępne**, wykonaj następujące czynności:
    - **Łączność**: aplikacja sprawdza, czy serwer ma dostęp do Internetu. Jeśli serwer używa serwera proxy:
        - Kliknij pozycję **Skonfiguruj serwer proxy** , aby określić adres serwera proxy (w postaci http://ProxyIPAddress lub na http://ProxyFQDN) porcie nasłuchu.
        - Jeśli serwer proxy wymaga uwierzytelnienia, wprowadź poświadczenia.
        - Obsługiwane są tylko serwery proxy HTTP.
        - Jeśli dodano szczegóły serwera proxy lub wyłączono serwer proxy i/lub uwierzytelnianie, kliknij przycisk **Zapisz** , aby ponownie uruchomić sprawdzanie łączności.
    - **Synchronizacja czasu**: godzina została zweryfikowana. Czas na urządzeniu powinien być zsynchronizowany z czasem internetowym w celu poprawnego działania funkcji odnajdywania serwerów.
    - **Instalowanie aktualizacji**: ocena serwera Azure Migrate sprawdza, czy na urządzeniu zainstalowano najnowsze aktualizacje. Po zakończeniu sprawdzania można kliknąć pozycję **Wyświetl usługi urządzenia** , aby zobaczyć stan i wersje składników uruchomionych na urządzeniu.

### <a name="register-the-appliance-with-azure-migrate"></a>Zarejestruj urządzenie w Azure Migrate

1. Wklej **klucz projektu Azure Migrate** skopiowany z portalu. Jeśli nie masz klucza, przejdź do pozycji **Ocena serwera> odkryj> zarządzanie istniejącymi urządzeniami**, wybierz nazwę urządzenia podaną w momencie generowania klucza i skopiuj odpowiedni klucz.
1. Kliknij pozycję **Zaloguj się**. Spowoduje to otwarcie monitu logowania platformy Azure na nowej karcie przeglądarki. Jeśli ta wartość nie jest wyświetlana, upewnij się, że w przeglądarce wyłączono blokowanie wyskakujących okienek.
1. Na nowej karcie Zaloguj się przy użyciu nazwy użytkownika i hasła platformy Azure.
   
   Logowanie przy użyciu numeru PIN nie jest obsługiwane.
3. Po pomyślnym zalogowaniu Wróć do aplikacji sieci Web. 
4. Jeśli konto użytkownika platformy Azure używane do rejestrowania ma odpowiednie [uprawnienia]() do zasobów platformy Azure utworzonych podczas generowania klucza, Rejestracja urządzenia zostanie zainicjowana.
1. Po pomyślnym zarejestrowaniu urządzenia można wyświetlić szczegóły rejestracji, klikając pozycję **Wyświetl szczegóły**.


## <a name="start-continuous-discovery"></a>Uruchom odnajdywanie ciągłe

Teraz nawiąż połączenie z urządzeniem z serwerami fizycznymi, które mają zostać odnalezione, i Uruchom odnajdywanie.

1. W **kroku 1: podaj poświadczenia do odnajdywania serwerów fizycznych lub wirtualnych z systemami Windows i Linux**, kliknij pozycję **Dodaj poświadczenia** , aby określić przyjazną nazwę dla poświadczeń, Dodaj **nazwę użytkownika** i **hasło** dla serwera z systemem Windows lub Linux. Kliknij pozycję **Zapisz**.
1. Jeśli chcesz dodać jednocześnie wiele poświadczeń, kliknij pozycję **Dodaj więcej** , aby zapisać i dodać więcej poświadczeń. W przypadku odnajdywania serwerów fizycznych obsługiwane są wiele poświadczeń.
1. W **kroku 2: Podaj informacje o serwerze fizycznym lub wirtualnym**, kliknij pozycję **Dodaj źródło odnajdowania** , aby określić **adres IP/nazwę FQDN** serwera i przyjazną nazwę dla poświadczeń do nawiązania połączenia z serwerem.
1. Możesz **dodać pojedynczy element** naraz lub **dodać wiele elementów** w jednym miejscu. Istnieje również możliwość zapewnienia informacji o serwerze za poorednictwem **importowania woluminu CSV**.


    - Jeśli wybierzesz opcję **Dodaj pojedynczy element**, możesz wybrać typ systemu operacyjnego, określić przyjazną nazwę dla poświadczeń, dodać **adres IP/nazwę FQDN** serwera i kliknąć przycisk **Zapisz**.
    - W przypadku wybrania opcji **Dodaj wiele elementów** można dodać wiele rekordów jednocześnie, określając **adres IP/nazwę FQDN** serwera z przyjazną nazwą poświadczenia w polu tekstowym. **Sprawdź** dodane rekordy i kliknij pozycję **Zapisz**.
    - W przypadku wybrania opcji **Importuj woluminy CSV** _(wybrane domyślnie)_ można pobrać plik szablonu CSV, wypełnić plik **adresem IP serwera/nazwą FQDN** i przyjazną nazwą poświadczenia. Następnie zaimportuj plik do urządzenia, **Sprawdź** rekordy w pliku i kliknij przycisk **Zapisz**.

1. Po kliknięciu przycisku Zapisz Urządzenie spróbuje sprawdzić poprawność połączenia z dodanymi serwerami i wyświetlić **stan sprawdzania poprawności** w tabeli na każdym serwerze.
    - Jeśli walidacja nie powiedzie się dla serwera, przejrzyj błąd, klikając opcję **Walidacja nie powiodła się** w kolumnie Stan tabeli. Usuń problem i ponownie sprawdź poprawność.
    - Aby usunąć serwer, kliknij przycisk **Usuń**.
1. Możesz ponownie **sprawdzić poprawność** łączności z serwerami w dowolnym momencie przed rozpoczęciem odnajdywania.
1. Kliknij przycisk **Rozpocznij odnajdywanie**, aby uruchomić odnajdywanie pomyślnie zweryfikowanych serwerów. Po pomyślnym zainicjowaniu odnajdywania można sprawdzić stan odnajdywania dla każdego serwera w tabeli.


Spowoduje to uruchomienie odnajdywania. Aby metadane wykrytego serwera pojawiły się w Azure Portal, zajmie około 2 minut na serwer.

## <a name="verify-servers-in-the-portal"></a>Weryfikowanie serwerów w portalu

Po zakończeniu odnajdywania możesz sprawdzić, czy serwery są wyświetlane w portalu.

1. Otwórz pulpit nawigacyjny usługi Azure Migrate.
2. W **Azure Migrate serwery**  >  **Azure Migrate: Strona Ocena serwera** kliknij ikonę, która wyświetla liczbę **odnalezionych serwerów**.
## <a name="next-steps"></a>Następne kroki

- [Oceń serwery fizyczne](tutorial-assess-physical.md) do migracji na maszyny wirtualne platformy Azure.
- [Przejrzyj dane](migrate-appliance.md#collected-data---physical) zbierane przez urządzenie podczas odnajdywania.