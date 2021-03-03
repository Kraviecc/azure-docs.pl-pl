---
title: Uzyskiwanie szczegółowych informacji przy użyciu centrum kopii zapasowych
description: Dowiedz się, jak analizować trendy historyczne i uzyskiwać dokładniejsze informacje o kopiach zapasowych przy użyciu centrum kopii zapasowych.
ms.topic: conceptual
ms.date: 09/01/2020
ms.openlocfilehash: 47158e53e6248b2b9cef4ff6fd6b5da5972786eb
ms.sourcegitcommit: c27a20b278f2ac758447418ea4c8c61e27927d6a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/03/2021
ms.locfileid: "101719461"
---
# <a name="obtain-insights-using-backup-center"></a>Uzyskiwanie szczegółowych informacji przy użyciu centrum kopii zapasowych

Aby analizować trendy historyczne i uzyskiwać dokładniejsze informacje o kopiach zapasowych, usługa Backup Center udostępnia interfejs do [raportów kopii zapasowych](configure-reports.md), który używa [dzienników Azure monitor](../azure-monitor/logs/data-platform-logs.md) i [skoroszytów platformy Azure](../azure-monitor/visualize/workbooks-overview.md). Raporty kopii zapasowych oferują następujące możliwości:

- Przydzielanie i prognozowanie zużytego magazynu w chmurze.

- Inspekcja kopii zapasowych i przywracania.

- Identyfikowanie kluczowych trendów na różnych poziomach szczegółowości.

- Zyskaj wgląd i wgląd w możliwości optymalizacji kosztów dla kopii zapasowych.

## <a name="supported-scenarios"></a>Obsługiwane scenariusze

- Raporty kopii zapasowych nie są obecnie dostępne dla Azure Database for PostgreSQL kopii zapasowej serwera.

- Zapoznaj się z [matrycą pomocy technicznej](backup-center-support-matrix.md) , aby uzyskać szczegółową listę obsługiwanych i nieobsługiwanych scenariuszy.

## <a name="get-started"></a>Rozpoczęcie pracy

### <a name="configure-your-vaults-to-send-data-to-a-log-analytics-workspace"></a>Konfigurowanie magazynów w celu wysyłania danych do obszaru roboczego Log Analytics

[Informacje na temat konfigurowania ustawień diagnostycznych w skali dla magazynów](./configure-reports.md#get-started)

### <a name="view-backup-reports-in-the-backup-center-portal"></a>Wyświetlanie raportów dotyczących kopii zapasowych w portalu centrum kopii zapasowych

Wybranie elementu menu **raporty kopii zapasowej** w centrum kopii zapasowych spowoduje otwarcie raportu. Wybierz co najmniej jeden obszar roboczy Log Analytics, aby wyświetlić i analizować kluczowe informacje o kopiach zapasowych.

![Tworzenie kopii zapasowych raportów w centrum kopii zapasowych](./media/backup-center-obtain-insights/backup-center-backup-reports.png)

Dostępne są następujące widoki:

1. **Podsumowanie** — Użyj tej karty, aby uzyskać ogólne omówienie funkcji tworzenia kopii zapasowych. [Dowiedz się więcej](./configure-reports.md#summary)

1. **Elementy kopii zapasowej** — ta karta służy do wyświetlania informacji i trendów w magazynie w chmurze zużywanych na poziomie elementu kopii zapasowej. [Dowiedz się więcej](./configure-reports.md#backup-items)

1. **Użycie** — ta karta służy do wyświetlania kluczowych parametrów rozliczania dla kopii zapasowych. [Dowiedz się więcej](./configure-reports.md#usage)

1. **Zadania** — Użyj tej karty, aby wyświetlić długotrwałe trendy na zadaniach, takie jak liczba zadań zakończonych niepowodzeniem dziennie i Najczęstsze przyczyny niepowodzenia zadania. [Dowiedz się więcej](./configure-reports.md#jobs)

1. **Zasady** — Użyj tej karty, aby wyświetlić informacje dotyczące wszystkich aktywnych zasad, takich jak liczba skojarzonych elementów i łączny magazyn w chmurze zużyty przez elementy, których kopia zapasowa jest wykonywana w ramach danej zasady. [Dowiedz się więcej](./configure-reports.md#policies)

1. **Optymalizacja** — Użyj tej karty, aby uzyskać wgląd w potencjalne możliwości optymalizacji kosztów dla kopii zapasowych. [Dowiedz się więcej](./configure-reports.md#optimize)

1. **Przestrzeganie zasad** — Użyj tej karty, aby uzyskać wgląd w to, czy każde wystąpienie kopii zapasowej miało co najmniej jedną pomyślną kopię zapasową dziennie.

## <a name="next-steps"></a>Następne kroki

- [Monitorowanie i wykonywanie kopii zapasowych](backup-center-monitor-operate.md)
- [Zarządzanie brakiem kopii zapasowej](backup-center-govern-environment.md)
- [Wykonywanie akcji przy użyciu centrum kopii zapasowych](backup-center-actions.md)