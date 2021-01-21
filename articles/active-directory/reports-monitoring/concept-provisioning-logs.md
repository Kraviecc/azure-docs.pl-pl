---
title: Dzienniki aprowizacji w portalu Azure Active Directory (wersja zapoznawcza) | Microsoft Docs
description: Wprowadzenie do raportów dotyczących aprowizacji dzienników w portalu Azure Active Directory
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: daveba
editor: ''
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.subservice: report-monitor
ms.date: 1/19/2021
ms.author: markvi
ms.reviewer: arvinh
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4c7d02b48d30fa558f8fd12f92705046dab74057
ms.sourcegitcommit: a0c1d0d0906585f5fdb2aaabe6f202acf2e22cfc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/21/2021
ms.locfileid: "98624239"
---
# <a name="provisioning-reports-in-the-azure-active-directory-portal-preview"></a>Raporty dotyczące aprowizacji w portalu Azure Active Directory (wersja zapoznawcza)

Architektura raportowania w Azure Active Directory (Azure AD) składa się z następujących składników:

- **Działanie** 
    - **Logowania** — informacje o użyciu aplikacji zarządzanych oraz działania związane z logowaniem użytkowników.
    - **Dzienniki inspekcji**  -  [Dzienniki inspekcji](concept-audit-logs.md) zapewniają informacje o aktywności systemu dotyczące zarządzania użytkownikami i grupami, zarządzanych aplikacji i działań związanych z katalogiem.
    - **Dzienniki aprowizacji** — zapewniają działania systemowe dotyczące użytkowników, grup i ról, które są obsługiwane przez usługę aprowizacji usługi Azure AD. 

- **Bezpieczeństwo** 
    - **Ryzykowne logowania** — [ryzykowne logowanie](../identity-protection/overview-identity-protection.md) jest wskaźnikiem próby logowania, które mogło zostać wykonane przez kogoś, kto nie jest uprawnionym właścicielem konta użytkownika.
    - **Użytkownicy oflagowani do ryzyka** — [ryzykowny użytkownik](../identity-protection/overview-identity-protection.md) jest wskaźnikiem konta użytkownika, które mogło zostać naruszone.

Ten temat zawiera omówienie dzienników aprowizacji. Zapewniają odpowiedzi na pytania, takie jak: 

* Które grupy zostały pomyślnie utworzone w usługi ServiceNow?
* Jakie użytkowników zostało pomyślnie usuniętych z firmy Adobe?
* Co użytkownicy z produktu Workday zostały pomyślnie utworzone w Active Directory? 

## <a name="prerequisites"></a>Wymagania wstępne

### <a name="who-can-access-the-data"></a>Kto może uzyskać dostęp do danych?
* Właściciele aplikacji mogą wyświetlać dzienniki dla aplikacji, których są właścicielami
* Użytkownicy w rolach administrator zabezpieczeń, czytelnik zabezpieczeń, czytelnik raportu, administrator aplikacji i administrator aplikacji w chmurze
* Użytkownicy w roli niestandardowej z [uprawnieniem provisioningLogs](https://docs.microsoft.com/azure/active-directory/roles/custom-enterprise-app-permissions#full-list-of-permissions)
* Administratorzy globalni


### <a name="what-azure-ad-license-do-you-need-to-access-provisioning-activities"></a>Jaka licencja usługi Azure AD jest wymagana w celu uzyskania dostępu do działań aprowizacji?

Dzierżawca musi mieć skojarzoną licencję Azure AD — wersja Premium, aby wyświetlić raport dotyczący całej aktywności aprowizacji. Aby uaktualnić swoją wersję usługi Azure Active Directory, zobacz [Wprowadzenie do usługi Azure Active Directory w wersji Premium](../fundamentals/active-directory-get-started-premium.md). 


## <a name="ways-of-interacting-with-the-provisioning-logs"></a>Sposoby współpracy z dziennikami aprowizacji 
Klienci mają cztery metody współdziałania z dziennikami aprowizacji:

1. Uzyskiwanie dostępu do dzienników z Azure Portal zgodnie z poniższym opisem.
1. Przesyłanie strumieniowe dzienników aprowizacji do [Azure monitor](https://docs.microsoft.com/azure/active-directory/app-provisioning/application-provisioning-log-analytics), co pozwala na Rozszerzone przechowywanie danych, tworzenie niestandardowych pulpitów nawigacyjnych, alertów i zapytań.
1. Wykonywanie zapytania dotyczącego [interfejsu API Microsoft Graph](https://docs.microsoft.com/graph/api/resources/provisioningobjectsummary?view=graph-rest-beta) dla dzienników aprowizacji.
1. Pobieranie dzienników aprowizacji jako pliku CSV lub JSON.

## <a name="access-the-logs-from-the-azure-portal"></a>Uzyskaj dostęp do dzienników z Azure Portal
Dostęp do dzienników aprowizacji można uzyskać, wybierając pozycję **dzienniki aprowizacji** w sekcji **monitorowanie** w bloku **Azure Active Directory** w [Azure Portal](https://portal.azure.com). W przypadku niektórych rekordów aprowizacji w portalu może upłynąć do dwóch godzin.

![Dzienniki aprowizowania](./media/concept-provisioning-logs/access-provisioning-logs.png "Dzienniki aprowizowania")


Dziennik aprowizacji zawiera domyślny widok listy, który pokazuje:

- Tożsamość
- Akcja
- System źródłowy
- System docelowy
- Stan
- Data


![Kolumny domyślne](./media/concept-provisioning-logs/default-columns.png "Kolumny domyślne")

Możesz dostosować widok listy, klikając pozycję **Kolumny** na pasku narzędzi.

![Wybór kolumn](./media/concept-provisioning-logs/column-chooser.png "Wybór kolumn")

Dzięki temu możesz wyświetlić dodatkowe pola lub usunąć pola, które są już wyświetlane.

![Dostępne kolumny](./media/concept-provisioning-logs/available-columns.png "Dostępne kolumny")

Wybierz element w widoku listy, aby uzyskać bardziej szczegółowe informacje.

![Szczegółowe informacje](./media/concept-provisioning-logs/steps.png "Filtr")


## <a name="filter-provisioning-activities"></a>Filtrowanie działań aprowizacji

Możesz filtrować dane aprowizacji. Niektóre wartości filtru są dynamicznie wypełniane na podstawie dzierżawy. Jeśli na przykład nie masz żadnych zdarzeń tworzenia w dzierżawie, nie będzie dostępna opcja filtru dla operacji tworzenia.
W widoku domyślnym można wybrać następujące filtry:

- Tożsamość
- Date
- Stan
- Akcja


![Dodaj filtry](./media/concept-provisioning-logs/default-filter.png "Filtr")

Filtr **tożsamości** umożliwia określenie nazwy lub tożsamości, o której Cię interesują. Ta tożsamość może być użytkownikiem, grupą, rolą lub innym obiektem. Można wyszukiwać według nazwy lub identyfikatora obiektu. Identyfikator różni się w zależności od scenariusza. Na przykład podczas aprowizacji obiektu z usługi Azure AD do usług SalesForce identyfikator źródłowy jest IDENTYFIKATORem obiektu użytkownika w usłudze Azure AD, a TargetID jest IDENTYFIKATORem użytkownika w usłudze Salesforce. Po zainicjowaniu obsługi administracyjnej od dnia roboczego do Active Directory identyfikator źródła to identyfikator pracownika procesu roboczego programu Workday. Należy zauważyć, że nazwa użytkownika może nie zawsze występować w kolumnie tożsamość. Zawsze będzie istnieć jeden identyfikator. 


Filtr **Data** umożliwia zdefiniowanie przedziału czasu dla zwracanych danych.  
Możliwe wartości:

- 1 miesiąc
- 7 dni
- 30 dni
- 24 godziny
- Niestandardowy zakres czasu

Po wybraniu niestandardowego przedziału czasu można skonfigurować datę początkową i datę końcową.


Filtr **stanu** umożliwia wybranie:

- Wszystko
- Powodzenie
- Niepowodzenie
- Pominięto



Filtr **akcji** umożliwia filtrowanie:

- Utwórz 
- Aktualizacja
- Usuń
- Wyłącz
- Inne

Dodatkowo, do filtrów widoku domyślnego, można również ustawić następujące filtry:

- Identyfikator zadania
- Identyfikator cyklu
- Identyfikator zmiany
- Identyfikator źródła
- Identyfikator docelowy
- Aplikacja


![Wybierz pole](./media/concept-provisioning-logs/add-filter.png "Wybierz pole")


- **Identyfikator zadania** — unikatowy identyfikator zadania jest skojarzony z każdą aplikacją, dla której włączono obsługę administracyjną.   

- **Identyfikator cyklu** — jednoznacznie identyfikuje cykl aprowizacji. Ten identyfikator można udostępnić do obsługi, aby wyszukać cykl, w którym wystąpiło zdarzenie.

- **Zmień identyfikator** — unikatowy identyfikator dla zdarzenia aprowizacji. Ten identyfikator można udostępnić do obsługi wyszukania zdarzenia aprowizacji.   


- **System źródłowy** — umożliwia określenie lokalizacji, z której jest inicjowana tożsamość. Na przykład podczas aprowizacji obiektu z usługi Azure AD do usługi ServiceNow, system źródłowy to Azure AD. 

- **System docelowy** — umożliwia określenie lokalizacji, w której ma zostać zainicjowana tożsamość. Na przykład podczas aprowizacji obiektu z usługi Azure AD do usługi ServiceNow system docelowy to usługi ServiceNow. 

- **Aplikacja** — umożliwia wyświetlanie tylko rekordów aplikacji o nazwie wyświetlanej zawierającej określony ciąg.

 

## <a name="provisioning-details"></a>Szczegóły aprowizacji 

Po wybraniu elementu w widoku listy aprowizacji uzyskasz więcej szczegółowych informacji na temat tego elementu.
Szczegóły są pogrupowane w oparciu o następujące kategorie:

- Kroki

- Rozwiązywanie problemów i zalecenia

- Zmodyfikowane właściwości

- Podsumowanie


![Szczegóły aprowizacji](./media/concept-provisioning-logs/provisioning-tabs.png "Karty")



### <a name="steps"></a>Kroki

Na karcie **kroki** przedstawiono kroki, które należy wykonać w celu aprowizacji obiektu. Inicjowanie obsługi obiektu może składać się z czterech kroków: 

- Importuj obiekt
- Określanie, czy obiekt jest w zakresie
- Dopasuj obiekt między źródłem i elementem docelowym
- Inicjowanie obiektu (podejmowanie akcji — może to być tworzenie, aktualizowanie, usuwanie lub wyłączanie)



![Zrzut ekranu przedstawia kartę kroki, która zawiera kroki inicjowania obsługi.](./media/concept-provisioning-logs/steps.png "Filtr")


### <a name="troubleshoot-and-recommendations"></a>Rozwiązywanie problemów i zalecenia


Karta **Rozwiązywanie problemów i zalecenia** zawiera kod błędu i przyczynę. Informacje o błędzie są dostępne tylko w przypadku awarii. 


### <a name="modified-properties"></a>Zmodyfikowane właściwości

**Zmodyfikowane właściwości** pokazuje starą wartość i nową wartość. W przypadku braku starej wartości kolumna stara wartość jest pusta. 

### <a name="summary"></a>Podsumowanie

Karta **Podsumowanie** zawiera przegląd informacji o tym, co się stało i identyfikatory dla obiektu w systemie źródłowym i docelowym. 

## <a name="download-logs-as-csv-or-json"></a>Pobierz dzienniki jako plik CSV lub JSON

Dzienniki aprowizacji można pobrać do użycia później, przechodząc do dzienników w Azure Portal a następnie klikając pozycję Pobierz. Plik zostanie przefiltrowany na podstawie wybranych kryteriów filtrowania. Można sprawić, aby filtry były możliwie jak najbardziej określone, aby skrócić czas pobierania i rozmiar pobieranych plików. Pobieranie woluminu CSV zostało podzielone na trzy pliki:

* ProvisioningLogs: Pobiera wszystkie dzienniki, z wyjątkiem kroków aprowizacji i zmodyfikowanych właściwości.
* ProvisioningLogs_ProvisioningSteps: zawiera kroki inicjowania obsługi administracyjnej i identyfikator zmiany. Identyfikator zmiany może służyć do sprzęgania zdarzenia z innymi dwoma plikami.
* ProvisioningLogs_ModifiedProperties: zawiera atrybuty, które zostały zmienione wraz z IDENTYFIKATORem zmiany. Identyfikator zmiany może służyć do sprzęgania zdarzenia z innymi dwoma plikami.

#### <a name="opening-the-json-file"></a>Otwieranie pliku JSON
Aby otworzyć plik JSON, użyj edytora tekstów, takiego jak [kod Microsoft Visual Studio](https://aka.ms/vscode). Visual Studio Code ułatwia ich odczytywanie, zapewniając wyróżnianie składni. Plik JSON można także otworzyć przy użyciu przeglądarek w nieedytowalnym formacie, np. [Microsoft Edge](https://aka.ms/msedge) 

#### <a name="prettifying-the-json-file"></a>Prettifying plik JSON
Plik JSON zostanie pobrany w formacie zminimalizowanego, aby zmniejszyć rozmiar pobierania. To z kolei może utrudnić odczytywanie ładunku. Zapoznaj się z dwoma opcjami, aby Prettify plik:

1. Użyj Visual Studio Code, aby sformatować kod JSON

Postępuj zgodnie z instrukcjami zdefiniowanymi [tutaj](https://code.visualstudio.com/docs/languages/json#_formatting) , aby sformatować plik JSON przy użyciu Visual Studio Code.

2. Formatowanie kodu JSON przy użyciu programu PowerShell

Ten skrypt będzie wyprowadzał dane JSON w formacie prettified z kartami i spacjami. 

` $JSONContent = Get-Content -Path "<PATH TO THE PROVISIONING LOGS FILE>" | ConvertFrom-JSON`

`$JSONContent | ConvertTo-Json > <PATH TO OUTPUT THE JSON FILE>`

#### <a name="parsing-the-json-file"></a>Analizowanie pliku JSON

Oto kilka przykładowych poleceń do pracy z plikiem JSON przy użyciu programu PowerShell. Możesz użyć dowolnego języka programowania, z którym masz doświadczenie.  

Najpierw [Przeczytaj plik JSON](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/convertfrom-json?view=powershell-7.1) , uruchamiając polecenie:

` $JSONContent = Get-Content -Path "<PATH TO THE PROVISIONING LOGS FILE>" | ConvertFrom-JSON`

Teraz można analizować dane w danym scenariuszu. Oto kilka przykładów: 

1. Wyprowadź wszystkie jobIDs w JsonFile

`foreach ($provitem in $JSONContent) { $provitem.jobId }`

2. Wyprowadź wszystkie changeIds dla zdarzeń, w których akcja była "Create"

`foreach ($provitem in $JSONContent) { `
`   if ($provItem.action -eq 'Create') {`
`       $provitem.changeId `
`   }`
`}`

## <a name="what-you-should-know"></a>Co należy wiedzieć

- W Azure Portal są przechowywane zgłoszone dane aprowizacji przez 30 dni, jeśli masz wersję Premium i 7 dni, jeśli masz bezpłatną wersję. Dzienniki aprowizacji można publikować w usłudze [log Analytics](../app-provisioning/application-provisioning-log-analytics.md) w celu przechowywania danych przez okres dłuższy niż 30 dni. 

- Można użyć atrybutu identyfikatora zmiany jako unikatowego identyfikatora. Jest to przydatne na przykład podczas współdziałania z pomocą techniczną produktu.

- W przypadku użytkowników, którzy nie znajdują się w zakresie, mogą zostać wyświetlone pominięte zdarzenia. Jest to oczekiwane, szczególnie w przypadku, gdy zakres synchronizacji jest ustawiony na wszystkich użytkowników i grupy. Nasza usługa oceni wszystkie obiekty w dzierżawie, nawet te, które znajdują się poza zakresem. 

- Dzienniki aprowizacji są obecnie niedostępne w chmurze dla instytucji rządowych. Jeśli nie możesz uzyskać dostępu do dzienników aprowizacji, użyj dzienników inspekcji jako tymczasowego obejścia. 

- Dzienniki aprowizacji nie wyświetlają importów ról (dotyczy to AWS, SalesForce i systemu Zendesk). Dzienniki dla importowanych ról można znaleźć w dziennikach inspekcji. 

## <a name="error-codes"></a>Kody błędów

Skorzystaj z poniższej tabeli, aby lepiej zrozumieć, jak rozwiązywać błędy, które można znaleźć w dziennikach aprowizacji. W przypadku brakujących kodów błędów Prześlij opinię przy użyciu linku w dolnej części tej strony. 

|Kod błędu|Opis|
|---|---|
|Konflikt, EntryConflict|Popraw wartości atrybutów powodujących konflikt w usłudze Azure AD lub aplikacji albo sprawdź zgodną konfigurację atrybutów, jeśli powodujące konflikt konto użytkownika ma zostać dopasowane i przejęte. Zapoznaj się z poniższą [dokumentacją](../app-provisioning/customize-application-attributes.md) , aby uzyskać więcej informacji na temat konfigurowania pasujących atrybutów.|
|TooManyRequests|Aplikacja docelowa odrzuciła próbę zaktualizowania użytkownika, ponieważ jest przeciążona i otrzymuje zbyt wiele żądań. Nie ma nic do zrobienia. Ta próba zostanie automatycznie wycofana. Firma Microsoft otrzymała również powiadomienie o tym problemie.|
|InternalServerError |Aplikacja docelowa zwróciła nieoczekiwany błąd. Może wystąpić problem z usługą w aplikacji docelowej, która uniemożliwia wykonanie tej pracy. Ta próba zostanie automatycznie wycofana w ciągu 40 minut.|
|InsufficientRights, MethodNotAllowed, NotPermitted, nieautoryzowane| Usługa Azure AD mogła uwierzytelnić się w aplikacji docelowej, ale nie ma autoryzacji do wykonania tej aktualizacji. Przejrzyj wszelkie instrukcje dostarczone przez aplikację docelową oraz odpowiedni [samouczek](../saas-apps/tutorial-list.md)aplikacji.|
|UnprocessableEntity|Aplikacja docelowa zwróciła nieoczekiwaną odpowiedź. Konfiguracja aplikacji docelowej może być niepoprawna lub wystąpił problem z aplikacją docelową, która uniemożliwia wykonywanie tego działania.|
|WebExceptionProtocolError |Wystąpił błąd protokołu HTTP podczas nawiązywania połączenia z aplikacją docelową. Nie ma nic do zrobienia. Ta próba zostanie automatycznie wycofana w ciągu 40 minut.|
|InvalidAnchor|Użytkownik, który został wcześniej utworzony lub dopasowany przez usługę aprowizacji, już nie istnieje. Sprawdź, czy użytkownik istnieje. Aby wymusić ponowne dopasowanie wszystkich użytkowników, należy [ponownie uruchomić zadanie](/graph/api/synchronization-synchronizationjob-restart?tabs=http&view=graph-rest-beta)przy użyciu programu MS interfejs API programu Graph. Ponowne uruchomienie aprowizacji wyzwoli cykl początkowy, który może zająć trochę czasu. Powoduje również usunięcie pamięci podręcznej używanej przez usługę aprowizacji do działania, co oznacza, że wszyscy użytkownicy i grupy w dzierżawie będą musieli ponownie ocenić i można porzucić pewne zdarzenia aprowizacji.|
|Nie zaimplementowano | Aplikacja docelowa zwróciła nieoczekiwaną odpowiedź. Konfiguracja aplikacji może być niepoprawna lub wystąpił problem z usługą dla aplikacji docelowej, która uniemożliwia wykonanie tej pracy. Przejrzyj wszelkie instrukcje dostarczone przez aplikację docelową i odpowiedni [samouczek](../saas-apps/tutorial-list.md)aplikacji. |
|MandatoryFieldsMissing, MissingValues |Nie można utworzyć użytkownika, ponieważ brakuje wymaganych wartości. Popraw brakujące wartości atrybutów w rekordzie źródłowym lub przejrzyj zgodną konfigurację atrybutów, aby upewnić się, że wymagane pola nie zostały pominięte. [Dowiedz się więcej](../app-provisioning/customize-application-attributes.md) o konfigurowaniu pasujących atrybutów.|
|SchemaAttributeNotFound |Nie można wykonać operacji, ponieważ określono atrybut, który nie istnieje w aplikacji docelowej. Zapoznaj się z [dokumentacją](../app-provisioning/customize-application-attributes.md) dotyczącą dostosowywania atrybutów i upewnij się, że konfiguracja jest poprawna.|
|InternalError |Wystąpił wewnętrzny błąd usługi w usłudze Azure AD Provisioning. Nie ma nic do zrobienia. Ta próba zostanie ponowiona automatycznie w ciągu 40 minut.|
|InvalidDomain |Nie można wykonać operacji z powodu wartości atrybutu zawierającej nieprawidłową nazwę domeny. Zaktualizuj nazwę domeny użytkownika lub Dodaj ją do listy dozwolonych w aplikacji docelowej. |
|Limit czasu |Nie można ukończyć operacji, ponieważ aplikacja docelowa zbyt długo nie odpowiadała. Nie ma nic do zrobienia. Ta próba zostanie ponowiona automatycznie w ciągu 40 minut.|
|LicenseLimitExceeded|Nie można utworzyć użytkownika w aplikacji docelowej, ponieważ nie ma żadnych dostępnych licencji dla tego użytkownika. Uzyskaj więcej licencji dla aplikacji docelowej lub przejrzyj przypisania użytkowników i konfigurację mapowania atrybutów, aby upewnić się, że poprawni użytkownicy są przypisani przy użyciu poprawnych atrybutów.|
|DuplicateTargetEntries  |Nie można ukończyć operacji, ponieważ znaleziono więcej niż jednego użytkownika w aplikacji docelowej ze skonfigurowanymi pasującymi atrybutami. Usuń zduplikowanego użytkownika z aplikacji docelowej lub ponownie skonfiguruj mapowania atrybutów zgodnie z opisem w [tym miejscu](../app-provisioning/customize-application-attributes.md).|
|DuplicateSourceEntries | Nie można ukończyć operacji, ponieważ znaleziono więcej niż jednego użytkownika ze skonfigurowanymi pasującymi atrybutami. Usuń zduplikowanego użytkownika lub Zmień konfigurację mapowań atrybutów zgodnie z opisem w [tym miejscu](../app-provisioning/customize-application-attributes.md).|
|ImportSkipped | Podczas oceniania każdego użytkownika podjęto próbę zaimportowania użytkownika z systemu źródłowego. Ten błąd występuje często, gdy importowany użytkownik nie ma pasującej właściwości zdefiniowanej w mapowaniu atrybutów. Bez wartości znajdującej się w obiekcie użytkownika dla pasującego atrybutu nie można obliczyć zakresu, dopasowywania ani eksportowania zmian. Należy zauważyć, że obecność tego błędu nie wskazuje, że użytkownik należy do zakresu, ponieważ nie oceniamy jeszcze zakresu dla użytkownika.|
|EntrySynchronizationSkipped | Usługa aprowizacji pomyślnie zbadał system źródłowy i zidentyfikował użytkownika. Nie wykonano żadnych dalszych akcji dla użytkownika i zostały one pominięte. Pominięcie mogą być spowodowane brakiem zakresu lub użytkownikiem już istniejącym w systemie docelowym bez konieczności wprowadzania dalszych zmian.|
|SystemForCrossDomainIdentityManagementMultipleEntriesInResponse| Podczas wykonywania żądania GET w celu pobrania użytkownika lub grupy w odpowiedzi otrzymano wielu użytkowników lub grupy. Oczekujemy, że w odpowiedzi otrzymasz tylko jednego użytkownika lub grupę. Jeśli [na przykład](../app-provisioning/use-scim-to-provision-users-and-groups.md#get-group)wyślemy żądanie pobrania grupy i udostępnienia filtru do wykluczania elementów członkowskich, a punkt końcowy Standard scim zwraca członków, zgłosi ten błąd.|

## <a name="next-steps"></a>Następne kroki

* [Sprawdź stan aprowizacji użytkowników](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user.md)
* [Wystąpił problem podczas konfigurowania aprowizacji użytkowników w aplikacji z galerii usługi Azure AD](../app-provisioning/application-provisioning-config-problem.md)
* [Interfejs API grafu obsługi dzienników aprowizacji](/graph/api/resources/provisioningobjectsummary?view=graph-rest-beta)
