---
title: Azure Defender for SQL — korzyści i funkcje
description: Dowiedz się więcej o zaletach i funkcjach usługi Azure Defender dla programu SQL Server.
author: memildin
ms.author: memildin
ms.date: 11/22/2020
ms.topic: overview
ms.service: security-center
ms.custom: references_regions
manager: rkarlin
ms.openlocfilehash: 102d4916caf9dcae577006b6b847979f98ab3673
ms.sourcegitcommit: d60976768dec91724d94430fb6fc9498fdc1db37
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/02/2020
ms.locfileid: "96499904"
---
# <a name="introduction-to-azure-defender-for-sql"></a>Wprowadzenie do usługi Azure Defender dla programu SQL

Usługa Azure Defender dla programu SQL obejmuje dwa plany usługi Azure Defender, które rozszerzają [pakiet zabezpieczeń danych](../azure-sql/database/azure-defender-for-sql.md) Azure Security Center, aby zabezpieczyć bazy danych i ich dane w dowolnym miejscu. 

## <a name="availability"></a>Dostępność

|Aspekt|Szczegóły|
|----|:----|
|Stan wydania:|**Usługa Azure Defender dla serwerów usługi Azure SQL Database** — ogólnie dostępna (ga)<br>**Usługa Azure Defender dla serwerów SQL na komputerach** — wersja zapoznawcza<br>[!INCLUDE [Legalese](../../includes/security-center-preview-legal-text.md)] |
|Wpisaną|Na [stronie cennika](security-center-pricing.md) są naliczane opłaty za dwa plany tworzące **usługę Azure Defender for SQL** .|
|Chronione wersje programu SQL:|SQL na maszynach wirtualnych platformy Azure — [systemy Windows](../azure-sql/virtual-machines/windows/sql-server-on-azure-vm-iaas-what-is-overview.md) i [Linux](../azure-sql/virtual-machines/linux/sql-server-on-linux-vm-what-is-iaas-overview.md)<br>[Serwery SQL z włączonym łukem](/sql/sql-server/azure-arc/overview) (w tym lokalne serwery SQL)<br>[Pojedyncze bazy danych](../azure-sql/database/single-database-overview.md) SQL Azure i [Pule elastyczne](../azure-sql/database/elastic-pool-overview.md)<br>[Wystąpienie zarządzane Azure SQL](../azure-sql/managed-instance/sql-managed-instance-paas-overview.md)<br>[Dedykowana Pula SQL usługi Azure Synapse Analytics](../synapse-analytics/sql-data-warehouse/sql-data-warehouse-overview-what-is.md)|
|Połączeń|![Tak](./media/icons/yes-icon.png) Chmury komercyjne<br>![Tak](./media/icons/yes-icon.png) US Gov<br>![Nie](./media/icons/no-icon.png) Chiny gov, inne gov|
|||

## <a name="what-does-azure-defender-for-sql-protect"></a>Co to jest usługa Azure Defender dla ochrony SQL?

**Usługa Azure Defender dla programu SQL** obejmuje dwa oddzielne plany usługi Azure Defender:

- **Usługa Azure Defender dla serwerów usługi Azure SQL Database** chroni:
  - [Azure SQL Database](../azure-sql/database/sql-database-paas-overview.md)
  - [Wystąpienie zarządzane Azure SQL](../azure-sql/managed-instance/sql-managed-instance-paas-overview.md)
  - [Dedykowana Pula SQL na platformie Azure Synapse](../synapse-analytics/sql-data-warehouse/sql-data-warehouse-overview-what-is.md)

- **Usługa Azure Defender dla serwerów SQL na maszynach (wersja zapoznawcza)** rozszerza ochronę natywnych serwerów SQL na platformie Azure w celu zapewnienia pełnej obsługi środowisk hybrydowych i ochrony serwerów SQL (wszystkie obsługiwane wersje) hostowanych na platformie Azure, w innych środowiskach w chmurze, a nawet na maszynach lokalnych


## <a name="what-are-the-benefits-of-azure-defender-for-sql"></a>Jakie korzyści zapewnia usługa Azure Defender dla programu SQL?

Te dwa plany obejmują funkcje służące do identyfikowania i ograniczania potencjalnych luk w zabezpieczeniach bazy danych oraz wykrywania nietypowych działań, które mogą wskazywać na zagrożenia dla baz danych:

- [Ocena luk w zabezpieczeniach](../azure-sql/database/sql-vulnerability-assessment.md) — Usługa skanowania w celu odnajdywania, śledzenia i rozwiązywania problemów dotyczących potencjalnych luk w zabezpieczeniach bazy danych. Przeglądy oceny zawierają omówienie stanu zabezpieczeń maszyn SQL i szczegółowe informacje o wszelkich wynikach związanych z bezpieczeństwem.

- [Zaawansowana ochrona przed zagrożeniami](../azure-sql/database/threat-detection-overview.md) — usługa wykrywania, która stale monitoruje serwery SQL pod kątem zagrożeń, takich jak iniekcja SQL, ataki z wymuszeniem i nadużycie uprawnień. Ta usługa udostępnia alerty zabezpieczeń zorientowane na działania w Azure Security Center z szczegółowymi informacjami o podejrzanych działaniach, wskazówkami dotyczącymi sposobu łagodzenia zagrożeń oraz opcjami do kontynuowania badań za pomocą platformy Azure.


## <a name="what-kind-of-alerts-does-azure-defender-for-sql-provide"></a>Jakiego rodzaju alerty zapewniają usługa Azure Defender dla programu SQL?

Alerty zabezpieczeń są wyzwalane w przypadku:

- **Potencjalne ataki z iniekcją SQL** — w tym luki wykryte w przypadku wygenerowania błędnej instrukcji SQL w bazie danych
- **Nietypowego dostępu do bazy danych i wzorców zapytań** — na przykład nietypowo duża liczba nieudanych prób logowania z różnymi poświadczeniami (próba nałożenia siły)
- **Podejrzana aktywność bazy danych** — na przykład zmiana w docelowym magazynie eksportu dla operacji importu i eksportu SQL

Alerty obejmują szczegółowe informacje o zdarzeniu, które je wywołały, a także zalecenia dotyczące sposobu badania i korygowania zagrożeń.



## <a name="next-steps"></a>Następne kroki

W tym artykule przedstawiono informacje o usłudze Azure Defender dla programu SQL Server.

W przypadku pokrewnego materiału zapoznaj się z następującymi artykułami: 

- [Jak włączyć usługę Azure Defender dla serwerów SQL na maszynach](defender-for-sql-usage.md)
- [Jak włączyć usługę Azure Defender dla serwerów baz danych SQL](../azure-sql/database/azure-defender-for-sql.md)
- [Lista alertów usługi Azure Defender dla programu SQL](alerts-reference.md#alerts-sql-db-and-warehouse)
