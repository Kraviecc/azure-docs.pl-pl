---
title: Wymagania dotyczące wspólnych transakcji | Portal Azure Marketplace
description: Dowiedz się więcej o wymaganiach oferta oferowana przez firmę Microsoft komercyjnej witryny Marketplace, aby zakwalifikować się do korzystania z zachęcani sprzedaży gotowej lub do sprzedaży.
ms.service: marketplace
ms.subservice: partnercenter-marketplace-publisher
ms.topic: how-to
author: vamahtan
ms.author: vamahtan
ms.date: 3/12/2021
ms.openlocfilehash: fa8f2b5e952ddd188f99d130c2154d4602191c2b
ms.sourcegitcommit: 94c3c1be6bc17403adbb2bab6bbaf4a717a66009
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/12/2021
ms.locfileid: "103225068"
---
# <a name="co-sell-requirements"></a>Wymagania dotyczące wspólnych transakcji

Ten artykuł zawiera wymagania dotyczące różnych poziomów współsprzedażowych. Aby uzyskać najnowszą listę typów ofert, które obsługują wspólną sprzedaż, zobacz  [Konfigurowanie współsprzedaży dla komercyjnej oferty portalu Marketplace](commercial-marketplace-co-sell.md). Aby zapoznać się z omówieniem współpracy, zobacz artykuł [współpraca z zespołami sprzedaży firmy Microsoft i partnerami](marketplace-co-sell.md).

W tej tabeli przedstawiono wszystkie możliwe stany współsprzedażowe:

| Stan | Komentarz |
| ------------ | ------------- |
| Nie Współpracuj gotowy | Nie spełniono minimalnych [wymagań dotyczących stanu gotowości do współsprzedażu](#requirements-for-co-sell-ready-status) . |
| Gotowe do rozłożenia | Wszystkie [wymagania dotyczące stanu gotowości do współsprzedażu](#requirements-for-co-sell-ready-status) zostały spełnione. |
| Usługa Azure IP zachęcani — sprzedawanie | Oprócz [tych dodatkowych wymagań](#requirements-for-azure-ip-co-sell-incentivized-status)zostały spełnione wymagania dotyczące wspólnych transakcji. |
| BIZ Apps ISV Connect Premium  | Ten stan ma zastosowanie do oferty Dynamics 365 i usługi dla aplikacji zaawansowanych i wskazuje, że spełniono wszystkie [wymagania dotyczące tego stanu](#requirements-for-biz-apps-isv-connect-premium-incentive-status) . |
|||

## <a name="requirements-for-co-sell-ready-status"></a>Wymagania w zakresie przygotowania do współdziałania

Aby uzyskać ofertę osiągnięcia stanu gotowości do sprzedaży, musisz spełnić następujące wymagania:

**Wszyscy partnerzy**:

- Mieć identyfikator MPN i aktywne [komercyjne konto portalu Marketplace w centrum partnerskim](./partner-center-portal/create-account.md).
- Upewnij się, że masz pełny [profil biznesowy](/partner-center/create-a-marketing-profile) w centrum partnerskim. Jako uprawniony partner firmy Microsoft Twój profil biznesowy pomaga klientom, którzy poszukują Twoich unikatowych rozwiązań i wiedzą, w zakresie zaspokajania potrzeb firmy, co wynika z [odwołań](/partner-center/referrals).
- Ukończ **sprzedawanie z kartami firmy Microsoft** i Opublikuj ofertę na komercyjnym rynku.
- Podaj kontakt sprzedaży dla każdej sprzedawanej lokalizacji geograficznej i wymaganego zestawienia materiałów)

**Partnerzy usług**:

- W przypadku ofert typu _rozwiązanie usługi_ należy mieć aktywną kompetencję Gold w dowolnym obszarze kompetencji.
 
**Business Applications niezależnych dostawców oprogramowania**:

- Dynamics 365 Customer Engagement & PowerApps i Dynamics 365 finanse & Ops (z wyjątkiem Dynamics 365 Business Central), a rozwiązania PowerApps wymagają rejestracji niezależnego dostawcy oprogramowania.

### <a name="complete-the-co-sell-with-microsoft-tab"></a>Ukończ sprzedawanie z kartami firmy Microsoft

Podczas publikowania lub aktualizowania oferty Podaj wszystkie wymagane informacje na karcie **współsprzedaż z firmą Microsoft** , zgodnie z opisem w temacie [Konfigurowanie współsprzedaży dla komercyjnej oferty portalu Marketplace](commercial-marketplace-co-sell.md). Obejmuje to następujące dokumenty:

- Rozwiązanie/oferowanie jednego modułu stronicowania
- Pokład rozwiązania/skoku oferty

Udostępniamy szablony ułatwiające tworzenie tych dokumentów. Aby uzyskać więcej informacji na temat informacji wymaganych i opcjonalnych dla karty współsprzedaży z firmą Microsoft, zobacz sekcję [Konfigurowanie współsprzedaży dla komercyjnej oferty portalu Marketplace](commercial-marketplace-co-sell.md).

### <a name="publish-your-offer-live"></a>Publikuj swoją ofertę na żywo

Aby można było zakwalifikować się do sprzedaży w stanie gotowości, oferta lub rozwiązanie musi zostać opublikowane na żywo co najmniej jednego sklepu online Marketplace: Azure Marketplace lub Microsoft AppSource. Aby uzyskać informacje o publikowaniu ofert do komercyjnej witryny Marketplace, zobacz [Publikowanie przewodnika według typu oferty](publisher-guide-by-offer-type.md). Jeśli jeszcze nie opublikowano oferty w komercyjnej witrynie Marketplace, upewnij się, że masz [komercyjne konto w portalu Marketplace](./partner-center-portal/create-account.md).

## <a name="requirements-for-azure-ip-co-sell-incentivized-status"></a>Wymagania dotyczące usługi Azure IP zachęcani

Stan zachęcani współsprzedaży platformy Azure w ramach adresu IP dotyczący następujących typów ofert:

- Azure Application
- Kontener platformy Azure
- Maszyna wirtualna platformy Azure
- Moduł IoT Edge
- Oprogramowanie jako usługa (SaaS)

Po osiągnięciu stanu gotowości do sprzedawania należy spełnić trzy dodatkowe wymagania, aby uzyskać stan zachęcani współsprzedażowej usługi Azure IP:

Wymaganie 1 — osiąganie następujących danych:

- Na _poziomie organizacji_ Wygeneruj co najmniej $100 000 USD wartości progowej przychodu z platformy Azure w ciągu końcowych 12-miesięcznego okresu. Można to uzyskać za pomocą kombinacji rozwiązań platformy Azure. Jeśli oferta jest transakcyjna w komercyjnej witrynie Marketplace, można spełnić to wymaganie, korzystając z progu przychodu wynoszącego $100 000 USD.

Wymaganie 2 — Przekaż weryfikację techniczną firmy Microsoft do rozwiązania opartego na platformie Azure:
- Weryfikacja techniczna musi potwierdzić, że ponad 50% infrastruktury oferty używa powtarzalny kod IP na platformie Azure. Należy zauważyć, że transakcyjne maszyny wirtualne platformy Azure i rozwiązania aplikacji platformy Azure na rynku komercyjnym będą spełniać te wymagania domyślnie.

Wymaganie 3 — udostępnianie diagramu architektury referencyjnej:
- Zapoznaj się z diagramem architektury referencyjnej zawierającym dokumenty towarzyszące w centrum partnerskim do przeglądu. Aby uzyskać wskazówki dotyczące tworzenia tego diagramu, zobacz [diagram architektury referencyjnej](reference-architecture-diagram.md). Aby uzyskać informacje o przekazywaniu diagramu, zobacz sekcję [Konfigurowanie współsprzedaży dla komercyjnej oferty portalu Marketplace](commercial-marketplace-co-sell.md).

## <a name="requirements-for-biz-apps-isv-connect-premium-incentive-status"></a>Wymagania dotyczące usługi BIZ Apps ISV Połącz stan zachęty Premium

Ten stan dotyczy rozwiązań opartych na protokole IP, aplikacji i usług wbudowanych w Dynamics 365 lub aplikacjach zaawansowanych.

Nie musisz osiągać stanu gotowości do zakupu (wymienionego powyżej), aby uzyskać BIZ aplikacje dostawcy niezależnego oprogramowania do nawiązywania połączenia. Jednak po osiągnięciu przez aplikację stanu gotowości do realizacji należy wziąć pod uwagę, że aplikacje BIZ Apps ISV łączą się ze stanem oferty Premium w oparciu o ubiegłe 12 miesięcy udział w udziale i wyniki współsprzedażowych/progów.

Wymaganie — wymagana jest aktywna Rejestracja w warstwie Premium programu [ISV Connect](business-applications-isv-program.md) .

## <a name="next-steps"></a>Następne kroki

- [Konfigurowanie współsprzedaży dla komercyjnej oferty portalu Marketplace](commercial-marketplace-co-sell.md)
