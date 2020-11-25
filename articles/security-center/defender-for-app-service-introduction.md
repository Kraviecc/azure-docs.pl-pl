---
title: Usługa Azure Defender dla App Service — korzyści i funkcje
description: Dowiedz się więcej o zaletach i funkcjach usługi Azure Defender dla App Service.
author: memildin
ms.author: memildin
ms.date: 9/22/2020
ms.topic: overview
ms.service: security-center
manager: rkarlin
ms.openlocfilehash: bb0e073d5ccf73434d05c801b9a8727c1d19fa47
ms.sourcegitcommit: b8a175b6391cddd5a2c92575c311cc3e8c820018
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/25/2020
ms.locfileid: "96122235"
---
# <a name="introduction-to-azure-defender-for-app-service"></a>Wprowadzenie do usługi Azure Defender dla App Service

Azure App Service to w pełni zarządzana platforma do tworzenia i hostowania aplikacji i interfejsów API sieci Web bez obaw o zarządzanie infrastrukturą. Umożliwia zarządzanie, monitorowanie i wgląd w dane operacyjne w celu spełnienia wymagań dotyczących wydajności, zabezpieczeń i zgodności klasy korporacyjnej. Aby uzyskać więcej informacji, zobacz [Azure App Service](https://azure.microsoft.com/services/app-service/).

**Usługa Azure Defender dla App Service** używa skali chmury, aby identyfikować ataki ukierunkowane na aplikacje działające przez App Service. Osoby atakujące mogą wykrywać słabe i luki w zabezpieczeniach aplikacji sieci Web. Przed skierowaniem do określonych środowisk żądania do aplikacji uruchomionych na platformie Azure przechodzą przez kilka bram, gdzie są kontrolowane i rejestrowane. Te dane są następnie używane do identyfikowania luk w zabezpieczeniach i ataków oraz do uczenia się nowych wzorców, które będą używane później.

Korzystając z widoczności platformy Azure jako dostawcy chmury, Security Center analizuje App Service dzienników wewnętrznych w celu zidentyfikowania metodologii ataków na wiele obiektów docelowych. Na przykład metodologia obejmuje szerokie skanowanie i rozproszone ataki. Ten typ ataku zwykle pochodzi z małego podzbioru adresów IP i pokazuje wzorce przeszukiwania do podobnych punktów końcowych na wielu hostach. Ataki są wyszukiwaniem zagrożonej strony lub wtyczki i nie mogą być zidentyfikowane z punktu widzenia jednego hosta.


## <a name="availability"></a>Dostępność

|Aspekt|Szczegóły|
|----|:----|
|Stan wydania:|Ogólnie dostępna (GA)|
|Wpisaną|[Usługa Azure Defender dla App Service](azure-defender.md) jest rozliczana zgodnie z opisem na [stronie cennika](security-center-pricing.md)|
|Obsługiwane App Service plany:|![Tak — ](./media/icons/yes-icon.png) podstawowa, standardowa, Premium, izolowany lub Linux<br>![Brak ](./media/icons/no-icon.png) wolnego, współdzielonego lub zużycia<br>[Dowiedz się więcej o planach App Service](https://azure.microsoft.com/pricing/details/app-service/plans/)|
|Połączeń|![Tak](./media/icons/yes-icon.png) Chmury komercyjne<br>![Nie](./media/icons/no-icon.png) National/suwerenne (US Gov, Chiny gov, inne gov)|
|||

## <a name="what-does-azure-defender-for-app-service-protect"></a>Co to jest usługa Azure Defender dla App Service ochrony?

Po włączeniu planu App Service Security Center ocenia zasoby objęte planem App Service i generuje zalecenia dotyczące zabezpieczeń na podstawie ich wyników. Security Center chroni wystąpienie maszyny wirtualnej, w której jest uruchomiony App Service i interfejs zarządzania. Monitoruje również żądania i odpowiedzi wysyłane do i z aplikacji uruchamianych w App Service.

Jeśli używasz planu App Service opartego na systemie Windows, Security Center również ma dostęp do podstawowych piaskownic i maszyn wirtualnych. Wraz z danymi dzienników wymienionymi powyżej infrastruktura może powiedzieć historię, od nowego ataku w przypadku komputerów klienckich. W związku z tym nawet jeśli Security Center zostanie wdrożona po wykorzystaniu aplikacji sieci Web, może być możliwe wykrycie trwających ataków.


## <a name="protect-your-azure-app-service-web-apps-and-apis"></a>Chronienie aplikacji internetowych i interfejsów API w usłudze Azure App Service
Aby chronić plan Azure App Service za pomocą usługi Azure Defender dla App Service:

- Upewnij się, że masz plan App Service, który jest skojarzony z dedykowanymi maszynami. Obsługiwane plany są wymienione powyżej w obszarze [dostępność](#availability).

- Włącz **usługę Azure Defender** w ramach subskrypcji (można opcjonalnie włączyć tylko **usługę azure Defender for App Service** plan) zgodnie z opisem w [cenniku Azure Security Center](security-center-pricing.md)

Security Center jest natywnie zintegrowana z App Service, eliminując konieczność wdrażania i dołączania — integracja jest niewidoczna.

>[!NOTE]
> Na stronie Cennik i ustawienia znajduje się lista wystąpień **zasobów**. Przedstawia ona łączną liczbę wystąpień obliczeniowych w ramach wszystkich App Service planów w ramach tej subskrypcji, uruchomionych w momencie otwarcia strony warstwy cenowej.
>
> Azure App Service oferuje różne plany. Plan App Service definiuje zestaw zasobów obliczeniowych dla aplikacji sieci Web do uruchomienia. Są one równoważne farmom serwerów w konwencjonalnym hostingu w sieci Web. Co najmniej jedna aplikacja może być skonfigurowana do uruchamiania w tych samych zasobach obliczeniowych (lub w tym samym planie App Service).
>
>Aby sprawdzić poprawność liczby, przejdź do obszaru "App Service plany" w witrynie Azure Portal, gdzie możesz zobaczyć liczbę wystąpień obliczeniowych używanych przez poszczególne plany. 



## <a name="next-steps"></a>Następne kroki

W tym artykule przedstawiono informacje o usłudze Azure Defender dla App Service. 

W przypadku pokrewnego materiału zapoznaj się z następującymi artykułami: 

- Czy alert jest generowany przez Security Center, czy odbierany przez Security Center z innego produktu zabezpieczeń, można go wyeksportować. Aby wyeksportować alerty do platformy Azure, wszelkich SIEM innych firm lub innych zewnętrznych narzędzi, postępuj zgodnie z instrukcjami zawartymi w [alertach przesyłania strumieniowego do Siem, o lub rozwiązania do zarządzania usługami IT](export-to-siem.md).
- Listę alertów Azure App Service można znaleźć w [tabeli referencyjnej alertów](alerts-reference.md#alerts-azureappserv).
- Aby uzyskać więcej informacji na temat planów App Service, zobacz [plany App Service](https://azure.microsoft.com/pricing/details/app-service/plans/).
- > [!div class="nextstepaction"]
    > [Włączanie usługi Azure Defender](security-center-pricing.md)