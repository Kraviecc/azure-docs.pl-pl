---
title: Azure Defender for SQL
description: Dowiedz się więcej o funkcji zarządzania lukami w bazie danych i wykrywaniu nietypowych działań, które mogą wskazywać na zagrożenie dla bazy danych w Azure SQL Database, wystąpieniu zarządzanym Azure SQL lub Azure Synapse.
services: sql-database
ms.service: sql-db-mi
ms.subservice: security
ms.devlang: ''
ms.custom: sqldbrb=2
ms.topic: conceptual
ms.author: memildin
manager: rkarlin
author: memildin
ms.date: 02/02/2021
ms.openlocfilehash: 48df96373554f6e474c3835bf81e38a9aea5450c
ms.sourcegitcommit: b85ce02785edc13d7fb8eba29ea8027e614c52a2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/03/2021
ms.locfileid: "99508815"
---
# <a name="azure-defender-for-sql"></a>Azure Defender for SQL
[!INCLUDE[appliesto-sqldb-sqlmi-asa](../includes/appliesto-sqldb-sqlmi-asa.md)]

Usługa Azure Defender for SQL to ujednolicony pakiet na potrzeby zaawansowanych funkcji zabezpieczeń SQL. Usługa Azure Defender jest dostępna do Azure SQL Database, wystąpienia zarządzanego usługi Azure SQL i usługi Azure Synapse Analytics. Obejmuje to funkcję wykrywania i klasyfikowania danych poufnych, uwidacznianie i korygowanie potencjalnych luk w zabezpieczeniach bazy danych oraz wykrywanie nietypowych działań, które mogą wskazywać, że baza danych jest zagrożona. Zapewnia ona pojedynczą lokalizację, w której można włączać te możliwości i zarządzać nimi.

## <a name="what-are-the-benefits-of-azure-defender-for-sql"></a>Jakie korzyści zapewnia usługa Azure Defender dla programu SQL?

Usługa Azure Defender oferuje zestaw zaawansowanych funkcji zabezpieczeń SQL, w tym ocenę luk w zabezpieczeniach SQL i zaawansowaną ochronę przed zagrożeniami.
- [Ocena luk w zabezpieczeniach](sql-vulnerability-assessment.md) to prosta w konfiguracji usługa, która umożliwia odnajdywanie, śledzenie i rozwiązywanie problemów z potencjalnymi lukami w zabezpieczeniach bazy danych. Zapewnia wgląd w stan zabezpieczeń i obejmuje czynności do wykonania w celu rozwiązywania problemów z zabezpieczeniami i ulepszania bazy danych FORTIFICATIONS.
- Usługa [Advanced Threat Protection](threat-detection-overview.md) wykrywa nietypowe działania wskazujące na nieprawidłowe i potencjalnie szkodliwe próby uzyskania dostępu do bazy danych lub wykorzystania jej. Ciągle monitoruje bazę danych pod kątem podejrzanych działań i zapewnia natychmiastowe alerty zabezpieczeń dotyczące potencjalnych luk w zabezpieczeniach, ataki iniekcji SQL Azure oraz nietypowe wzorce dostępu do bazy danych. Alerty usługi Advanced Threat Protection zawierają szczegółowe informacje o podejrzanych działaniach i zalecane czynności dotyczące sposobu badania i ograniczenia zagrożenia.

Włącz usługę Azure Defender dla SQL raz, aby włączyć wszystkie te funkcje. Po jednym kliknięciu można włączyć usługę Azure Defender dla wszystkich baz danych na [serwerze](logical-servers.md) na platformie Azure lub w wystąpieniu zarządzanym SQL. Włączanie ustawień usługi Azure Defender lub zarządzanie nimi wymaga przynależności do roli [programu SQL Security Manager](../../role-based-access-control/built-in-roles.md#sql-security-manager) lub jednej z ról administratora bazy danych lub serwera.

Aby uzyskać więcej informacji na temat cennika usługi Azure Defender for SQL, zobacz [stronę z cennikiem Azure Security Center](https://azure.microsoft.com/pricing/details/security-center/).

## <a name="enable-azure-defender"></a>Włączanie usługi Azure Defender

Dostęp do usługi Azure Defender można uzyskać za pomocą [Azure Portal](https://portal.azure.com). Włącz usługę Azure Defender, przechodząc do **Security Center** w obszarze nagłówka **zabezpieczenia** serwera lub wystąpienia zarządzanego.

> [!NOTE]
> Konto magazynu jest automatycznie tworzone i konfigurowane do przechowywania wyników skanowania **oceny luk w zabezpieczeniach** . Jeśli usługa Azure Defender została już włączona dla innego serwera w tej samej grupie zasobów i regionie, używane jest istniejące konto magazynu.
>
> Koszt usługi Azure Defender jest wyrównany przy Azure Security Center użyciu cen warstwy Standardowa na węzeł, gdzie węzeł jest całym serwerem lub wystąpieniem zarządzanym. W ten sposób płacisz tylko raz na ochronę wszystkich baz danych na serwerze lub w wystąpieniu zarządzanym za pomocą usługi Azure Defender. Możesz wstępnie wypróbować usługę Azure Defender, korzystając z bezpłatnej wersji próbnej.

:::image type="content" source="media/azure-defender-for-sql/enable-azure-defender.png" alt-text="Włączanie usługi Azure Defender dla języka SQL z poziomu baz danych Azure SQL Database":::

## <a name="track-vulnerabilities-and-investigate-threat-alerts"></a>Śledzenie luk w zabezpieczeniach i badanie alertów dotyczących zagrożeń

Kliknij kartę **Ocena luk w zabezpieczeniach** , aby wyświetlić i zarządzać skanowaniem i raportami luk w zabezpieczeniach oraz śledzić schemacie zabezpieczeń. Jeśli alerty zabezpieczeń zostały odebrane, kliknij kartę **Zaawansowana ochrona przed zagrożeniami** , aby wyświetlić szczegóły alertów i wyświetlić skonsolidowany raport dotyczący wszystkich alertów w ramach subskrypcji platformy Azure za pośrednictwem strony alerty zabezpieczeń Azure Security Center.

## <a name="manage-azure-defender-settings"></a>Zarządzanie ustawieniami usługi Azure Defender

Aby wyświetlić ustawienia usługi Azure Defender i zarządzać nimi:

1. W obszarze **zabezpieczenia** serwera lub wystąpienia zarządzanego wybierz pozycję **Security Center**.

    Na tej stronie zostanie wyświetlony stan usługi Azure Defender dla programu SQL:

    :::image type="content" source="media/azure-defender-for-sql/status-of-defender-for-sql.png" alt-text="Sprawdzanie stanu usługi Azure Defender for SQL w bazach danych Azure SQL":::

1. Jeśli usługa Azure Defender dla programu SQL jest włączona, zostanie wyświetlony link **Konfiguruj** , jak pokazano na poprzedniej ilustracji. Aby edytować ustawienia usługi Azure Defender dla programu SQL, wybierz pozycję **Konfiguruj**.

    :::image type="content" source="media/azure-defender-for-sql/security-server-settings.png" alt-text="Ustawienia serwera zabezpieczeń":::

1. Wprowadź niezbędne zmiany i wybierz pozycję **Zapisz**.


## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej na temat [oceny luk w zabezpieczeniach](sql-vulnerability-assessment.md)
- Dowiedz się więcej na temat [zaawansowanej ochrony przed zagrożeniami](threat-detection-configure.md)
- Dowiedz się więcej o [Azure Security Center](../../security-center/security-center-introduction.md)