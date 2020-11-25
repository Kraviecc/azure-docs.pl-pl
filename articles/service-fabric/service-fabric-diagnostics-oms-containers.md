---
title: Monitorowanie kontenerów za pomocą dzienników Azure Monitor
description: Użyj dzienników Azure Monitor na potrzeby monitorowania kontenerów działających w klastrach Service Fabric platformy Azure.
author: srrengar
ms.topic: conceptual
ms.date: 02/25/2019
ms.author: srrengar
ms.openlocfilehash: c1d118fa1fb65663f37e33f739bf4a72a14e1c52
ms.sourcegitcommit: a43a59e44c14d349d597c3d2fd2bc779989c71d7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/25/2020
ms.locfileid: "95998225"
---
# <a name="monitor-containers-with-azure-monitor-logs"></a>Monitorowanie kontenerów za pomocą dzienników Azure Monitor
 
W tym artykule opisano kroki wymagane do skonfigurowania Azure Monitor dzienniki rozwiązania do monitorowania kontenerów w celu wyświetlenia zdarzeń kontenera. Aby skonfigurować klaster do zbierania zdarzeń kontenera, zapoznaj się z tym [samouczkiem krok po kroku](service-fabric-tutorial-monitoring-wincontainers.md). 

[!INCLUDE [log-analytics-agent-note.md](../../includes/log-analytics-agent-note.md)]

[!INCLUDE [azure-monitor-log-analytics-rebrand](../../includes/azure-monitor-log-analytics-rebrand.md)]

## <a name="set-up-the-container-monitoring-solution"></a>Skonfiguruj rozwiązanie do monitorowania kontenerów

> [!NOTE]
> Konieczne jest skonfigurowanie dzienników Azure Monitor dla klastra, a także wdrożenie agenta Log Analytics w węzłach. Jeśli nie, wykonaj kroki opisane w temacie [konfigurowanie Azure monitor dzienników](service-fabric-diagnostics-oms-setup.md) i najpierw [Dodaj agenta log Analytics do klastra](service-fabric-diagnostics-oms-agent.md) .

1. Po skonfigurowaniu klastra z dziennikami Azure Monitor i agentem Log Analytics należy wdrożyć kontenery. Przed przejściem do następnego kroku poczekaj na wdrożenie kontenerów.

2. W witrynie Azure Marketplace Wyszukaj *rozwiązanie do monitorowania kontenerów* i kliknij zasób **rozwiązanie do monitorowania** kontenerów, który jest wyświetlany w kategorii Monitorowanie + zarządzanie.

    ![Dodawanie rozwiązania kontenerów](./media/service-fabric-diagnostics-event-analysis-oms/containers-solution.png)

3. Utwórz rozwiązanie w tym samym obszarze roboczym, który został już utworzony dla klastra. Ta zmiana powoduje automatyczne wyzwolenie agenta, aby rozpocząć zbieranie danych platformy Docker w kontenerach. W ciągu około 15 minut, powinno być widoczne rozwiązanie z uwzględnieniem dzienników przychodzących i statystyk, jak pokazano na poniższej ilustracji.

    ![Pulpit nawigacyjny podstawowej Log Analytics](./media/service-fabric-diagnostics-event-analysis-oms/oms-containers-dashboard.png)

Agent umożliwia zbieranie kilku dzienników specyficznych dla kontenera, które mogą być badane w dziennikach Azure Monitor lub używane do wizualizacji wskaźników wydajności. Zbierane są następujące typy dzienników:

* ContainerInventory: wyświetla informacje o lokalizacji kontenera, nazwie i obrazach
* ContainerImageInventory: informacje o wdrożonych obrazach, w tym o identyfikatorach lub rozmiarach
* ContainerLog: konkretne dzienniki błędów, dzienniki platformy Docker (stdout itp.) i inne wpisy
* ContainerServiceLog: polecenia demona platformy Docker, które zostały uruchomione
* Wydajność: Liczniki wydajności, takie jak procesor CPU, pamięć, ruch sieciowy, we/wy dysku i metryki niestandardowe z komputerów-hostów



## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [Azure monitor rozwiązaniu kontenerów dzienników](../azure-monitor/insights/containers.md).
* Przeczytaj więcej na temat aranżacji kontenerów na Service Fabric- [Service Fabric i kontenerach](service-fabric-containers-overview.md)
* Zapoznaj się z funkcjami [przeszukiwania dzienników i wykonywania zapytań](../azure-monitor/log-query/log-query-overview.md) , które są oferowane w ramach dzienników Azure monitor
* Konfigurowanie dzienników Azure Monitor w celu skonfigurowania [zautomatyzowanych reguł alertów](../azure-monitor/platform/alerts-overview.md) w celu ułatwienia wykrywania i diagnostyki
