---
title: Nowości w platformie Azure — Wskaźnikowanie
description: W tym artykule opisano nowe funkcje na platformie Azure — od ostatnich kilku miesięcy.
services: sentinel
author: batamig
ms.author: bagol
ms.service: azure-sentinel
ms.subservice: azure-sentinel
ms.topic: conceptual
ms.date: 03/08/2021
ms.openlocfilehash: 88ac8bb1bc804604b96d5c90025b8325a6ce4962
ms.sourcegitcommit: 15d27661c1c03bf84d3974a675c7bd11a0e086e6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/09/2021
ms.locfileid: "102503128"
---
# <a name="whats-new-in-azure-sentinel"></a>Nowości w platformie Azure — Wskaźnikowanie

W tym artykule wymieniono najnowsze funkcje, które zostały dodane do usługi Azure, oraz nowe funkcje usług pokrewnych, które zapewniają Ulepszone środowisko użytkownika na platformie Azure.

Aby uzyskać informacje o wcześniejszych funkcjach, zobacz nasze [Blogi społeczności Tech](https://techcommunity.microsoft.com/t5/azure-sentinel/bg-p/AzureSentinelBlog/label-name/What's%20New).

Notowane funkcje są obecnie dostępne w wersji zapoznawczej. [Postanowienia uzupełniające dotyczące platformy Azure w wersji zapoznawczej](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) zawierają dodatkowe postanowienia prawne dotyczące funkcji systemu Azure, które są w wersji beta, wersji zapoznawczej lub w inny sposób nie zostały jeszcze udostępnione.


> [!TIP]
> Nasze zespoły zajmujące się łowiectwem zagrożeń w ramach zapytań, elementy PlayBook, skoroszytów i notesów programu Microsoft, w tym określonych [zapytań polowających](https://github.com/Azure/Azure-Sentinel) [, które](https://github.com/Azure/Azure-Sentinel)zespoły mogą dostosowywać i stosować. 
>
> Możesz również współtworzyć. Dołącz do nas w [społeczności usługi GitHub](https://github.com/Azure/Azure-Sentinel/wiki).
> 

## <a name="march-2021"></a>Marzec 2021

- [Integracja zdarzeń Microsoft 365 Defender](#microsoft-365-defender-incident-integration) (publiczna wersja zapoznawcza)
- [Nowe łączniki usługi firmy Microsoft korzystające z Azure Policy](#new-microsoft-service-connectors-using-azure-policy)

### <a name="microsoft-365-defender-incident-integration"></a>Integracja zdarzeń Microsoft 365 Defender

Integracja zdarzeń Microsoft 365 usługi Azure wskaźnikowej [(M365D)](/microsoft-365/security/mtp/microsoft-threat-protection) to usługa, która umożliwia przesyłanie strumieniowe wszystkich zdarzeń M365D do usługi Azure wskaźnikowej i utrzymywanie synchronizacji między obydwoma portalami. Zdarzenia z usługi M365D (dawniej znany jako Microsoft Threat Protection lub MTP) obejmują wszystkie skojarzone alerty, jednostki i istotne informacje, dzięki czemu można wykonać Klasyfikacja i wstępną badanie na platformie Azure. Gdy dane są wskazywane przez program, Zdarzenia nadal będą dwukierunkowe zsynchronizowane z usługą M365D, co pozwala korzystać z zalet obu portali w badaniu zdarzeń.

Jednoczesne korzystanie z platformy Azure i usługi Microsoft 365 Defender zapewnia najlepsze rozwiązanie obu tych rozwiązań. Uzyskasz szeroki wgląd w to, że SIEM udostępnia użytkownikowi cały zakres zasobów informacyjnych w organizacji, a także głębokość dostosowanej i dopasowanej mocy dochodzeniowej, którą XDR oferuje do ochrony zasobów Microsoft 365, zarówno w przypadku skoordynowanego, jak i zsynchronizowanego działania, które można bezproblemowo SOC.

Aby uzyskać więcej informacji, zobacz [integracja z usługą Microsoft 365 Defender z platformą Azure — wskaźnikiem](microsoft-365-defender-sentinel-integration.md).

### <a name="new-microsoft-service-connectors-using-azure-policy"></a>Nowe łączniki usługi firmy Microsoft korzystające z Azure Policy

[Azure Policy](../governance/policy/overview.md) to usługa platformy Azure, która umożliwia korzystanie z zasad w celu wymuszania i kontrolowania właściwości zasobu. Korzystanie z zasad zapewnia, że zasoby pozostają zgodne ze standardami zarządzania IT.

Wśród właściwości zasobów, które mogą być kontrolowane przez zasady, jest tworzenie i obsługa dzienników diagnostycznych i inspekcji. Wskaźnik na platformie Azure używa teraz Azure Policy, aby umożliwić stosowanie wspólnego zestawu ustawień dzienników diagnostycznych do wszystkich (bieżących i przyszłych) zasobów określonego typu, których dzienników chcesz pozyskać na platformie Azure. Dziękujemy za Azure Policy, nie trzeba już ustawiać zasobów ustawień dzienników diagnostycznych według zasobu.

Łączniki oparte na Azure Policy są teraz dostępne dla następujących usług platformy Azure:
- [Azure Key Vault](connect-azure-key-vault.md) (publiczna wersja zapoznawcza)
- [Usługa Azure Kubernetes](connect-azure-kubernetes-service.md) (publiczna wersja zapoznawcza)
- Bazy danych i serwery usługi Azure SQL Database (wersja ogólnie dostępna)

Klienci nadal będą mogli ręcznie wysyłać dzienniki dla określonych wystąpień i nie muszą używać aparatu zasad.

## <a name="february-2021"></a>Luty 2021 r.

- [Skoroszyt cyberbezpieczeństwa (CMMC) z modelem zapadalności](#cybersecurity-maturity-model-certification-cmmc-workbook)
- [Łączniki danych innych firm](#third-party-data-connectors)
- [UEBA szczegółowych informacji na stronie jednostki](#ueba-insights-in-the-entity-page)
- [Ulepszone wyszukiwanie zdarzeń](#improved-incident-search)

### <a name="cybersecurity-maturity-model-certification-cmmc-workbook"></a>Skoroszyt cyberbezpieczeństwa (CMMC) z modelem zapadalności

Skoroszyt CMMC na platformie Azure obejmuje mechanizm wyświetlania zapytań dzienników wyrównanych do kontrolek CMMC w portfolio firmy Microsoft, w tym ofert zabezpieczeń firmy Microsoft, pakietu Office 365, zespołów, usługi Intune, pulpitu wirtualnego systemu Windows i wielu innych.

Skoroszyt CMMC umożliwia architektom zabezpieczeń, inżynierom, analitykom operacji zabezpieczeń, menedżerom i specjalistom IT uzyskanie widoczności w zakresie bezpieczeństwa stan obciążeń w chmurze. Istnieją również zalecenia dotyczące wyboru, projektowania, wdrażania i konfigurowania ofert firmy Microsoft do wyrównania z odpowiednimi wymaganiami i praktyką CMMC.

Nawet jeśli nie jest wymagana zgodność z programem CMMC, skoroszyt CMMC jest przydatny podczas tworzenia centrów zabezpieczeń, tworzenia alertów, wizualizacji zagrożeń i zapewnienia świadomości w zakresie obciążeń.

Dostęp do skoroszytu CMMC w obszarze **skoroszyty** wskaźnikowego platformy Azure. Wybierz pozycję **szablon**, a następnie wyszukaj ciąg **CMMC**.

:::image type="content" source="media/whats-new/cmmc-guide-toggle.gif" alt-text="Włącz i Wyłącz Przewodnik po skoroszycie CMMC" lightbox="media/whats-new/cmmc-guide-toggle.gif":::


Aby uzyskać więcej informacji, zobacz:

- [Skoroszyt cyberbezpieczeństwa (CMMC) na platformie Azure — wskaźnik zapadalności](https://techcommunity.microsoft.com/t5/public-sector-blog/azure-sentinel-cybersecurity-maturity-model-certification-cmmc/ba-p/2110524)
- [Samouczek: wizualizowanie i monitorowanie danych](tutorial-monitor-your-data.md)


### <a name="third-party-data-connectors"></a>Łączniki danych innych firm

Nasza kolekcja integracji innych firm nadal rośnie, a w ciągu ostatnich dwóch miesięcy zostanie dodana trzydzieści łączników. Oto lista:

- [Agari phishing i ochrona przed markami](connect-agari-phishing-defense.md)
- [Zdarzenia zabezpieczeń Akamai](connect-akamai-security-events.md)
- [Alsid Active Directory](connect-alsid-active-directory.md)
- [Serwer Apache HTTP](connect-apache-http-server.md)
- [Aruba ClearPass](connect-aruba-clearpass.md)
- [BlackBerry CylancePROTECT](connect-data-sources.md)
- [Funkcja DLP firmy Symantec](connect-broadcom-symantec-dlp.md)
- [Cisco Firepower eStreamer](connect-data-sources.md)
- [Cisco Meraki](connect-cisco-meraki.md)
- [Cisco Umbrella](connect-cisco-umbrella.md)
- [Cisco Unified Computing System (UCS)](connect-cisco-ucs.md)
- [ESET Enterprise Inspector](connect-data-sources.md)
- [Centrum zarządzania zabezpieczeniami ESET](connect-data-sources.md)
- [Obszar roboczy Google (dawniej: zestaw G Suite)](connect-google-workspace.md)
- [Imperva WAF Gateway](connect-imperva-waf-gateway.md)
- [Juniper SRX](connect-juniper-srx.md)
- [Netskope](connect-data-sources.md)
- [NXLog dzienników DNS](connect-nxlog-dns.md)
- [NXLog systemu Linux](connect-nxlog-linuxaudit.md)
- [Platforma Onapsis](connect-data-sources.md)
- [Bezpieczeństwo poczty E-mail na żądanie Proofpoint (POD)](connect-proofpoint-pod.md)
- [Baza wiedzy zarządzania lukami w Qualys](connect-data-sources.md)
- [Salesforce Service Cloud](connect-salesforce-service-cloud.md)
- [Zapora SonicWall](connect-data-sources.md)
- [Sophos Cloud OPTIX](connect-sophos-cloud-optix.md)
- [Squid Proxy](connect-squid-proxy.md)
- [Endpoint Protection firmy Symantec](connect-data-sources.md)
- [Thycotic Secret Server](connect-thycotic-secret-server.md)
- [Trend Micro XDR](connect-data-sources.md)
- [VMware ESXi](connect-vmware-esxi.md)

### <a name="ueba-insights-in-the-entity-page"></a>UEBA szczegółowych informacji na stronie jednostki

Strony szczegółów jednostki wskaźnikowej platformy Azure udostępniają [okienko Insights](identify-threats-with-entity-behavior-analytics.md#entity-insights), w którym są wyświetlane szczegółowe informacje o działaniu jednostki i pomoc w szybkim wykrywaniu anomalii i zagrożeń bezpieczeństwa.

Jeśli masz [UEBA włączony](ueba-enrichments.md)i wybrałeś okres z przedziału czasu wynoszący co najmniej cztery dni, to okienko szczegółowych informacji będzie zawierać również następujące nowe sekcje dla usługi UEBA Insights:

|Sekcja  |Opis  |
|---------|---------|
|**UEBA Insights**     | Podsumowuje nietypowe działania użytkowników: <br>— Między lokalizacjami geograficznymi, urządzeniami i środowiskami<br>— W Horizons czasu i częstotliwości w porównaniu z własną historią użytkownika <br>— W porównaniu z zachowaniem elementów równorzędnych <br>— W porównaniu z zachowaniem organizacji     |
|**Elementy równorzędne użytkowników na podstawie przynależności do grupy zabezpieczeń**     |   Wyświetla listę elementów równorzędnych użytkownika w oparciu o członkostwo w grupach zabezpieczeń usługi Azure AD, dostarczając zespoły operacji zabezpieczeń z listą innych użytkowników, którzy mają podobne uprawnienia.  |
|**Uprawnienia dostępu użytkowników do subskrypcji platformy Azure**     |     Wyświetla uprawnienia dostępu użytkownika do subskrypcji platformy Azure dostępnych bezpośrednio lub za pośrednictwem grup/jednostek usługi Azure AD.   |
|**Wskaźniki zagrożeń powiązane z użytkownikiem**     |  Wyświetla listę znanych zagrożeń odnoszących się do adresów IP reprezentowanych w działaniach użytkownika. Zagrożenia są wymienione według typu i rodziny zagrożeń i są wzbogacane przez usługę analizy zagrożeń firmy Microsoft.       |
|     |         |

### <a name="improved-incident-search"></a>Ulepszone wyszukiwanie zdarzeń

Ulepszono środowisko wyszukiwania zdarzeń na platformie Azure, co pozwala na szybsze nawigowanie po zdarzeniach podczas badania określonego zagrożenia.

Podczas wyszukiwania zdarzeń na platformie Azure wskaźnikowej jest teraz możliwe wyszukiwanie według następujących szczegółów zdarzenia:

- ID (Identyfikator)
- Tytuł
- Produkt
- Właściciel
- Tag

## <a name="january-2021"></a>Styczeń 2021 r.

- [Kreator reguł analizy: Ulepszone środowisko edytowania zapytań (publiczna wersja zapoznawcza)](#analytics-rule-wizard-improved-query-editing-experience-public-preview)
- [AZ. SecurityInsights PowerShell — moduł (publiczna wersja zapoznawcza)](#azsecurityinsights-powershell-module-public-preview)
- [Łącznik bazy danych SQL](#sql-database-connector)
- [Łącznik systemu Dynamics 365](#dynamics-365-connector)
- [Ulepszone komentarze dotyczące zdarzeń](#improved-incident-comments)
- [Dedykowane klastry Log Analytics](#dedicated-log-analytics-clusters)
- [Tożsamości zarządzane przez aplikacje logiki](#logic-apps-managed-identities)
- [Ulepszone dostrajanie reguł przy użyciu wykresów z podglądem reguł analizy](#improved-rule-tuning-with-the-analytics-rule-preview-graphs-public-preview)


### <a name="analytics-rule-wizard-improved-query-editing-experience-public-preview"></a>Kreator reguł analizy: Ulepszone środowisko edytowania zapytań (publiczna wersja zapoznawcza)

Kreator zaplanowanej reguły analizy wskaźnikowej platformy Azure obejmuje teraz następujące udoskonalenia dotyczące pisania i edytowania zapytań:

-   Rozwijane okno edycji, które zapewnia więcej miejsca na ekranie, aby wyświetlić zapytanie.
-   Wyróżnianie kluczowych wyrazów w kodzie zapytania.
-   Rozszerzona obsługa autouzupełniania.
-   Walidacje zapytań w czasie rzeczywistym. Błędy w zapytaniu są teraz wyświetlane jako czerwony blok na pasku przewijania i jako czerwona kropka w nazwie karty **logiki zestawu reguł** . Ponadto nie można zapisać zapytania z błędami.

Aby uzyskać więcej informacji, zobacz [Samouczek: Tworzenie niestandardowych reguł analizy w celu wykrywania zagrożeń](tutorial-detect-threats-custom.md).
### <a name="azsecurityinsights-powershell-module-public-preview"></a>AZ. SecurityInsights PowerShell — moduł (publiczna wersja zapoznawcza)

Usługa Azure SecurityInsights obsługuje teraz nowy moduł [AZ.](https://www.powershellgallery.com/packages/Az.SecurityInsights/) PowerShell.

Moduł **AZ. SecurityInsights** obsługuje typowe przypadki użycia platformy Azure, takie jak manipulowanie zdarzeniami w celu zmiany Statues, ważności, właściciela i tak dalej, dodawania komentarzy i etykiet do zdarzeń oraz tworzenia zakładek.

Chociaż zalecamy używanie szablonów [Azure Resource Manager (ARM)](../azure-resource-manager/templates/index.yml) dla potoku ciągłej integracji/ciągłego wdrażania, moduł **AZ. SecurityInsights** jest przydatny do wykonywania zadań po wdrożeniu i jest przeznaczony dla automatyzacji SOC.  Na przykład Automatyzacja SOC może obejmować kroki konfigurowania łączników danych, tworzenia reguł analizy lub dodawania akcji automatyzacji do reguł analizy.

Aby uzyskać więcej informacji, w tym pełną listę i opis dostępnych poleceń cmdlet, opisów parametrów i przykładów, zobacz [AZ. SecurityInsights PowerShell — dokumentacja](/powershell/module/az.securityinsights/).

### <a name="sql-database-connector"></a>Łącznik bazy danych SQL

Wskaźnik na platformie Azure przedstawia teraz łącznik usługi Azure SQL Database, który umożliwia przesyłanie strumieniowe dzienników inspekcji i diagnostyki baz danych do usługi Azure wskaźnikowej i ciągłego monitorowania aktywności we wszystkich wystąpieniach.

Azure SQL to w pełni zarządzany aparat bazy danych platformy jako usługi (PaaS), który obsługuje większość funkcji zarządzania bazami danych, takich jak uaktualnianie, stosowanie poprawek, tworzenie kopii zapasowych i monitorowanie, bez zaangażowania użytkowników.

Aby uzyskać więcej informacji, zobacz [łączenie dzienników diagnostyki i inspekcji usługi Azure SQL Database](connect-azure-sql-logs.md).

### <a name="dynamics-365-connector"></a>Łącznik systemu Dynamics 365

Centrum danych platformy Azure udostępnia teraz łącznik dla systemu Microsoft Dynamics 365, który umożliwia gromadzenie dzienników aktywności użytkowników, administratorów i pomocy technicznej usługi Dynamics 365 na platformie Azure. Za pomocą tych danych można przeprowadzić inspekcję całości operacji przetwarzania danych i analizować ją pod kątem potencjalnych naruszeń zabezpieczeń.

Aby uzyskać więcej informacji, zobacz temat [łączenie dzienników aktywności Dynamics 365 z platformą Azure](connect-dynamics-365.md).

### <a name="improved-incident-comments"></a>Ulepszone komentarze dotyczące zdarzeń

Analitycy wykorzystują Komentarze do zdarzeń do współpracy nad zdarzeniami, dokumentowania procesów i kroków ręcznie lub w ramach element PlayBook. 

Nasze Ulepszone środowisko komentowania zdarzeń umożliwia formatowanie komentarzy i edytowanie lub usuwanie istniejących komentarzy.

Aby uzyskać więcej informacji, zobacz [Automatyczne tworzenie zdarzeń z alertów zabezpieczeń firmy Microsoft](create-incidents-from-alerts.md).
### <a name="dedicated-log-analytics-clusters"></a>Dedykowane klastry Log Analytics

Na platformie Azure jest teraz obsługiwane dedykowane klastry Log Analytics jako opcja wdrożenia. Zalecamy rozważenie dedykowanego klastra, jeśli:

- Zyskaj **ponad 1 TB** dziennie do obszaru roboczego wskaźnikowego platformy Azure
- **Posiadanie wielu obszarów roboczych usługi Azure** — Rejestracja na platformie Azure

Dedykowane klastry umożliwiają korzystanie z takich funkcji, jak klucze zarządzane przez klienta, skrytka, podwójne szyfrowanie i szybsze zapytania między obszarami roboczymi, gdy istnieje wiele obszarów roboczych w tym samym klastrze.

Aby uzyskać więcej informacji, zobacz [Azure monitor dzienniki dedykowanych klastrów](../azure-monitor/logs/logs-dedicated-clusters.md).

### <a name="logic-apps-managed-identities"></a>Tożsamości zarządzane przez aplikacje logiki

Usługa Azure element PlayBook obsługuje teraz zarządzane tożsamości dla łącznika Logic Apps wskaźnikowego platformy Azure, dzięki czemu można przyznać uprawnienia bezpośrednio do konkretnej do działania na platformie Azure, zamiast tworzyć dodatkowe tożsamości.

- **Bez tożsamości zarządzanej** łącznik Logic Apps wymaga oddzielnej tożsamości z rolą RBAC kontroli dostępu Azure Osobną tożsamością może być użytkownik usługi Azure AD lub nazwa główna usługi, na przykład zarejestrowana aplikacja usługi Azure AD.

- **Włączenie obsługi tożsamości zarządzanej w aplikacji logiki** spowoduje zarejestrowanie aplikacji logiki w usłudze Azure AD i podaje identyfikator obiektu. Użyj identyfikatora obiektu w wskaźniku kontroli platformy Azure, aby przypisać aplikację logiki z rolą RBAC platformy Azure w obszarze roboczym Azure wskaźnikowym. 

Aby uzyskać więcej informacji, zobacz:

- [Uwierzytelnianie za pomocą tożsamości zarządzanej w Azure Logic Apps](../logic-apps/create-managed-service-identity.md)
- [Dokumentacja dotycząca łącznika Logic Apps Azure wskaźnikowego](/connectors/azuresentinel) 

### <a name="improved-rule-tuning-with-the-analytics-rule-preview-graphs-public-preview"></a>Ulepszone dostrajanie reguł przy użyciu wykresów z podglądem reguł analizy (publiczna wersja zapoznawcza)

Na platformie Azure jest teraz pomocne lepsze dostosowanie reguł analitycznych, co pomaga zwiększyć ich dokładność i zmniejszyć szum.

Po przeprowadzeniu edycji reguły analizy na karcie **Ustawianie logiki reguły** Znajdź obszar **symulacja wyników** po prawej stronie. 

Wybierz pozycję **Testuj z bieżącymi danymi** , aby usługa Azure wskaźnikowa uruchomiła symulację ostatnich 50ych uruchomień reguły analizy. Generowany jest wykres przedstawiający średnią liczbę alertów wygenerowanych przez regułę na podstawie danych nieprzetworzonych zdarzeń. 

Aby uzyskać więcej informacji, zobacz [Definiowanie logiki zapytania reguły i Konfigurowanie ustawień](tutorial-detect-threats-custom.md#define-the-rule-query-logic-and-configure-settings).

## <a name="december-2020"></a>Grudzień 2020 r.

- [80 nowe wbudowane zapytania polowające](#80-new-built-in-hunting-queries)
- [Udoskonalenia agenta Log Analytics](#log-analytics-agent-improvements)

### <a name="80-new-built-in-hunting-queries"></a>80 nowe wbudowane zapytania polowające
 
Wbudowane zapytania polowające na platformie Azure sprawdzają analityków SOC, aby ograniczyć przerwy w bieżącym pokryciu wykrywania i powodować zapłon nowych potencjalnych klientów.

Ta aktualizacja dla systemu Azure wskaźnikowego obejmuje nowe zapytania polowające, które zapewniają pokrycie w macierzy MITRE ATT&

- **Kolekcja**
- **Polecenie i kontrola**
- **Dostęp do poświadczeń**
- **Odnajdywanie**
- **Działania**
- **Eksfiltracji**
- **Wpływ**
- **Dostęp wstępny**
- **Trwałość**
- **Eskalacja uprawnień**

Dodane zapytania dotyczące polowań zaprojektowano w celu ułatwienia znalezienia podejrzanych działań w Twoim środowisku. Chociaż mogą zwrócić wiarygodną aktywność i potencjalnie złośliwe działanie, mogą one być przydatne w przypadku wypróbowania Twojego polowania. 

Jeśli po uruchomieniu tych zapytań masz pewność, że możesz chcieć przekonwertować je na reguły analizy lub dodać wyniki polowania do istniejących lub nowych zdarzeń.

Wszystkie dodane zapytania są dostępne za pośrednictwem strony łowiectwa wskaźnikowego platformy Azure. Aby uzyskać więcej informacji, zobacz artykuł [w przypadku zagrożeń związanych z platformą Azure — wskaźnikiem](hunting.md).

### <a name="log-analytics-agent-improvements"></a>Udoskonalenia agenta Log Analytics

Użytkownicy usługi Azure wskaźnikowego korzystają z następujących usprawnień Log Analytics Agent:

- **Obsługa większej liczby systemów operacyjnych**, w tym CentOS 8, RedHat 8 i SUSE Linux 15.
- **Obsługa języka Python 3** oprócz języka Python 2

Usługa Azure CEF używa agenta Log Analytics do wysyłania zdarzeń do obszaru roboczego, w tym zdarzeń zabezpieczeń systemu Windows, zdarzeń dziennika systemowego, dzienników i innych.

> [!NOTE]
> Agent Log Analytics jest czasami określany jako agent pakietu OMS lub Microsoft Monitoring Agent (MMA). 
> 

Aby uzyskać więcej informacji, zobacz [dokumentację log Analytics](../azure-monitor/agents/log-analytics-agent.md) i informacje o [wersji agenta log Analytics](https://github.com/microsoft/OMS-Agent-for-Linux/releases).
## <a name="november-2020"></a>Listopad 2020 r.

- [Monitoruj kondycję elementy PlayBook na platformie Azure — wskaźnik](#monitor-your-playbooks-health-in-azure-sentinel)
- [Łącznik Microsoft 365 Defender (publiczna wersja zapoznawcza)](#microsoft-365-defender-connector-public-preview)

### <a name="monitor-your-playbooks-health-in-azure-sentinel"></a>Monitoruj kondycję elementy PlayBook na platformie Azure — wskaźnik

Usługa Azure wskaźnik elementy PlayBook opiera się na przepływach pracy utworzonych w usłudze [Azure log Apps](../logic-apps/index.yml), usłudze w chmurze, która pomaga zaplanować, zautomatyzować i zorganizować zadania, procesy biznesowe i przepływy pracy. Elementy PlayBook może być wywoływana automatycznie podczas tworzenia zdarzenia lub podczas segregowania i pracy z zdarzeniami. 

Aby uzyskać wgląd w kondycję, wydajność i użycie elementy PlayBook, dodaliśmy [skoroszyt](../azure-monitor/visualize/workbooks-overview.md) o nazwie **monitorowanie kondycji elementy PlayBook**. 

Użyj skoroszytu **monitorowania kondycji programu elementy PlayBook** , aby monitorować kondycję elementy PlayBook, lub poszukać anomalii w ilości pomyślnych lub nieudanych uruchomień. 

Skoroszyt **monitorowania kondycji elementy PlayBook** jest teraz dostępny w galerii szablonów wskaźnikowych platformy Azure:

:::image type="content" source="media/whats-new/playbook-monitoring-workbook.gif" alt-text="Przykładowy skoroszyt monitorowania kondycji elementy PlayBook":::

Aby uzyskać więcej informacji, zobacz:

- [Dokumentacja Logic Apps](../logic-apps/monitor-logic-apps-log-analytics.md#set-up-azure-monitor-logs)

- [Dokumentacja usługi Azure Monitor](../azure-monitor/essentials/activity-log.md#send-to-log-analytics-workspace)

### <a name="microsoft-365-defender-connector-public-preview"></a>Łącznik Microsoft 365 Defender (publiczna wersja zapoznawcza)
 
Łącznik usługi Microsoft 365 Defender dla platformy Azure (wskaźnik produkcji) umożliwia przesyłanie strumieniowe zaawansowanych dzienników łowiectwa (typu nieprzetworzonych danych zdarzeń) z Microsoft 365 Defender do platformy Azure. 

Dzięki integracji usługi [Microsoft Defender dla punktów końcowych (MDATP)](/windows/security/threat-protection/) na parasol zabezpieczeń programu [Microsoft 365 Defender](/microsoft-365/security/mtp/microsoft-threat-protection) można teraz zbierać zaawansowane zdarzenia polowania usługi Microsoft Defender for Endpoint przy użyciu łącznika Microsoft 365 Defender i przesyłać je bezpośrednio do nowych, wbudowanych tabel w obszarze roboczym wskaźnikowego platformy Azure. 

Tabele wskaźnikowe platformy Azure są oparte na tym samym schemacie, który jest używany w portalu Microsoft 365 Defender, i zapewnia pełny dostęp do pełnego zestawu zaawansowanych dzienników łowiectwa. 

Aby uzyskać więcej informacji, zobacz [łączenie danych z programu Microsoft 365 Defender z platformą Azure — wskaźnikiem](connect-microsoft-365-defender.md).

> [!NOTE]
> Usługa Microsoft 365 Defender była znana wcześniej jako Microsoft Threat Protection lub MTP. Usługa Microsoft Defender dla punktu końcowego była znana wcześniej jako usługa Microsoft Defender Advanced Threat Protection lub MDATP.
> 

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
>[Tablica wskaźnikowa platformy Azure](quickstart-onboard.md)

> [!div class="nextstepaction"]
>[Uzyskiwanie wglądu w alerty](quickstart-get-visibility.md)
