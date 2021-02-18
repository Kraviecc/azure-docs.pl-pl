---
title: Uaktualnianie do usługi Azure Defender — Azure Security Center
description: W tym przewodniku szybki start przedstawiono, jak przeprowadzić uaktualnienie do usługi Azure Defender Security Center, aby uzyskać dodatkowe zabezpieczenia.
services: security-center
documentationcenter: na
author: memildin
manager: rkarlin
ms.assetid: 61e95a87-39c5-48f5-aee6-6f90ddcd336e
ms.service: security-center
ms.devlang: na
ms.topic: quickstart
ms.custom: mvc
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/17/2021
ms.author: memildin
ms.openlocfilehash: 5e39093e0472705111907e72b70446db53770012
ms.sourcegitcommit: 58ff80474cd8b3b30b0e29be78b8bf559ab0caa1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/17/2021
ms.locfileid: "100634496"
---
# <a name="quickstart-set-up-azure-security-center"></a>Szybki Start: Konfigurowanie Azure Security Center

Usługa Azure Security Center zapewnia ujednolicone zarządzanie zabezpieczeniami i ochronę przed zagrożeniami na potrzeby różnych obciążeń chmury hybrydowej. Chociaż bezpłatne funkcje oferują ograniczone zabezpieczenia tylko dla zasobów platformy Azure, włączenie usługi Azure Defender rozszerza te możliwości do lokalnych i innych chmur. Usługa Azure Defender ułatwia znajdowanie i rozwiązywanie luk w zabezpieczeniach, stosowanie kontroli dostępu i aplikacji w celu blokowania złośliwych działań, wykrywanie zagrożeń przy użyciu analiz i analiz oraz szybkie reagowanie na ataki. Możesz bezpłatnie wypróbować usługę Azure Defender. Aby dowiedzieć się więcej, zobacz [stronę z cennikiem](https://azure.microsoft.com/pricing/details/security-center/).

Ten przewodnik Szybki Start przeprowadzi Cię przez włączenie usługi Azure Defender pod kątem dodatkowych zabezpieczeń i zainstalowanie agenta Log Analytics na maszynach w celu monitorowania luk w zabezpieczeniach i zagrożeń.

Wykonaj następujące czynności:

> [!div class="checklist"]
> * Włączanie Security Center w ramach subskrypcji platformy Azure
> * Włączanie usługi Azure Defender w ramach subskrypcji platformy Azure
> * Włącz automatyczne zbieranie danych

## <a name="prerequisites"></a>Wymagania wstępne
Do rozpoczęcia korzystania z usługi Security Center wymagana jest subskrypcja usługi Microsoft Azure. Jeśli nie masz subskrypcji, możesz zarejestrować się, aby uzyskać dostęp do [bezpłatnego konta](https://azure.microsoft.com/pricing/free-trial/).

Aby włączyć usługę Azure Defender w ramach subskrypcji, musisz mieć przypisaną rolę właściciela subskrypcji, współautora subskrypcji lub administratora zabezpieczeń.


## <a name="enable-security-center-on-your-azure-subscription"></a>Włączanie Security Center w ramach subskrypcji platformy Azure

1. Zaloguj się do [Azure Portal](https://azure.microsoft.com/features/azure-portal/).

1. Z menu portalu wybierz pozycję **Security Center**. 

    Zostanie otwarta strona przeglądu Security Center.

    :::image type="content" source="./media/security-center-get-started/overview.png" alt-text="Pulpit nawigacyjny przeglądu Security Center" lightbox="./media/security-center-get-started/overview.png":::

Okno **Security Center — Przegląd** zapewnia ujednolicony wgląd w stan zabezpieczeń obciążeń chmury hybrydowej, dzięki czemu możesz odnajdywać i oceniać zabezpieczenia obciążeń oraz identyfikować i ograniczać ryzyko. Security Center automatycznie, bez żadnych kosztów, umożliwia korzystanie z subskrypcji platformy Azure, które nie zostały wcześniej dołączone przez Ciebie lub innego użytkownika subskrypcji.

Możesz wyświetlić i filtrować listę subskrypcji, wybierając element menu **subskrypcje** . Security Center dostosowuje wyświetlanie, aby odzwierciedlały stan zabezpieczeń wybranych subskrypcji. 

W ciągu kilku minut od uruchomienia Security Center po raz pierwszy zobaczysz:

- **Zalecenia** dotyczące sposobów zwiększania bezpieczeństwa połączonych zasobów.
- Spis zasobów, które są teraz oceniane przez Security Center, wraz z stan zabezpieczeń każdego z nich.

Aby w pełni wykorzystać Security Center, należy wykonać poniższe kroki, aby włączyć usługę Azure Defender i zainstalować agenta Log Analytics.

> [!TIP]
> Aby włączyć Security Center we wszystkich subskrypcjach w grupie zarządzania, zobacz [włączanie Security Center w wielu subskrypcjach platformy Azure](onboard-management-group.md).

## <a name="enable-azure-defender"></a>Włączanie usługi Azure Defender

Na potrzeby przewodników Szybki Start i samouczków Security Center należy włączyć usługę Azure Defender. Dostępna jest bezpłatna 30-dniowa wersja próbna. Aby dowiedzieć się więcej, zobacz [stronę z cennikiem](https://azure.microsoft.com/pricing/details/security-center/). 

1. Na pasku bocznym Security Center wybierz opcję **wprowadzenie**.

    :::image type="content" source="./media/security-center-get-started/get-started-upgrade-tab.png" alt-text="Karta Uaktualnij na stronie Wprowadzenie"::: 

    Karta **Uaktualnij** zawiera listę subskrypcji i obszarów roboczych kwalifikujących się do dołączenia.

1. Z listy **Wybierz obszary robocze, aby włączyć usługę Azure Defender na** liście Wybierz obszary robocze do uaktualnienia.
   - Jeśli wybierzesz subskrypcje i obszary robocze, które nie są uprawnione do korzystania z wersji próbnej, następnym krokiem spowoduje ich uaktualnienie, a opłaty zostaną naliczone.
   - W przypadku wybrania obszaru roboczego, który kwalifikuje się do korzystania z bezpłatnej wersji próbnej, następnym krokiem będzie rozpoczęcie korzystania z wersji próbnej.
1. Wybierz pozycję **Uaktualnij** , aby włączyć usługę Azure Defender.

## <a name="enable-automatic-data-collection"></a>Włącz automatyczne zbieranie danych
Security Center zbiera dane z maszyn do monitorowania pod kątem luk w zabezpieczeniach i zagrożeń. Dane są zbierane przy użyciu agenta Log Analytics, który odczytuje różne konfiguracje związane z zabezpieczeniami i dzienniki zdarzeń z komputera i kopiuje dane do obszaru roboczego w celu przeprowadzenia analizy. Domyślnie usługa Security Center utworzy nowy obszar roboczy.

W przypadku włączenia automatycznej obsługi administracyjnej program Security Center instaluje agenta Log Analytics na wszystkich obsługiwanych maszynach i utworzonych nowych. Używanie automatycznej aprowizacji jest zdecydowanie zalecane.

Aby włączyć automatyczną obsługę administracyjną agenta Log Analytics:

1. W menu Security Center wybierz pozycję **cennik & ustawienia**.
1. Wybierz odpowiednią subskrypcję.
1. Na stronie **autozastrzeganie** dla **agenta log Analytics dla maszyn wirtualnych platformy Azure** Ustaw stan na **włączone**.
1. Wybierz pozycję **Zapisz**.

    :::image type="content" source="./media/security-center-enable-data-collection/enable-automatic-provisioning.png" alt-text="Włączanie obsługi administracyjnej agenta Log Analytics":::

>[!TIP]
> Jeśli konieczne jest zainicjowanie obszaru roboczego, Instalacja agenta może trwać do 25 minut.

Dzięki agentowi wdrożonemu na maszynach Security Center mogą zapewnić dodatkowe zalecenia dotyczące stanu aktualizacji systemu, konfiguracji zabezpieczeń systemu operacyjnego, programu Endpoint Protection, a także generować dodatkowe alerty zabezpieczeń.

>[!NOTE]
> Ustawienie opcji autozastrzeganie na **wyłączone** nie powoduje usunięcia agenta log Analytics z maszyn wirtualnych platformy Azure, w przypadku których Agent został już zainicjowany. Wyłączenie automatycznej aprowizacji powoduje ograniczenie monitorowania zabezpieczeń dla zasobów.



## <a name="next-steps"></a>Następne kroki
W tym przewodniku szybki start włączono usługę Azure Defender i Zainicjowano obsługę agenta Log Analytics w celu zapewnienia ujednoliconego zarządzania zabezpieczeniami i ochrony przed zagrożeniami w ramach obciążeń chmury hybrydowej. Aby dowiedzieć się więcej na temat korzystania z usługi Security Center, przejdź do przewodnika Szybki start dotyczącego dołączania komputerów z systemem Windows znajdujących się w środowisku lokalnym i w innych chmurach.

> [!div class="nextstepaction"]
> [Szybki Start: dołączanie maszyn nienależących do platformy Azure](quickstart-onboard-machines.md)

Chcesz zoptymalizować i zapisać wydatki na chmurę?

> [!div class="nextstepaction"]
> [Rozpocznij analizowanie kosztów za pomocą Cost Management](../cost-management-billing/costs/quick-acm-cost-analysis.md?WT.mc_id=costmanagementcontent_docsacmhorizontal_-inproduct-learn)

<!--Image references-->
[2]: ./media/security-center-get-started/overview.png
[4]: ./media/security-center-get-started/get-started.png
[5]: ./media/security-center-get-started/pricing.png
[7]: ./media/security-center-get-started/security-alerts.png
[8]: ./media/security-center-get-started/recommendations.png
[9]: ./media/security-center-get-started/select-subscription.png