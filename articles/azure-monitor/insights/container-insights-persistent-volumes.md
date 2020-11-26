---
title: Konfigurowanie monitorowania PV przy użyciu Azure Monitor dla kontenerów | Microsoft Docs
description: W tym artykule opisano, jak można skonfigurować monitorowanie klastrów Kubernetes z woluminami trwałymi przy użyciu Azure Monitor dla kontenerów.
ms.topic: conceptual
ms.date: 10/20/2020
ms.openlocfilehash: e7c547c137fc84e6e6dfb2807b871ef0329a3c13
ms.sourcegitcommit: d22a86a1329be8fd1913ce4d1bfbd2a125b2bcae
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96186851"
---
# <a name="configure-pv-monitoring-with-azure-monitor-for-containers"></a>Konfigurowanie monitorowania PV przy użyciu Azure Monitor dla kontenerów

Począwszy od wersji agenta *ciprod10052020*, usługa Azure monitor dla kontenerów Integrated Agent obsługuje teraz użycie funkcji monitorowania PV (trwałego woluminu).

## <a name="pv-metrics"></a>Metryki PV

Azure Monitor kontenerów automatycznie zaczyna monitorować PV przez zbieranie następujących metryk w interwałach 60sec i przechowywanie ich w tabeli **InsightMetrics** .

|Nazwa metryki |Wymiar metryki (Tagi) |Opis |
|------------|------------------------|------------|
| `pvUsedBytes`|`container.azm.ms/pv`|Zajęte miejsce w bajtach dla określonego woluminu trwałego z wnioskiem używanym przez określony element. `pvCapacityBytes` jest składany jako wymiar w polu Tagi, aby zmniejszyć koszty pozyskiwania danych i uprościć zapytania.|

## <a name="monitor-persistent-volumes"></a>Monitorowanie woluminów trwałych

Azure Monitor kontenerów zawiera wstępnie skonfigurowane wykresy dla tej metryki w skoroszycie dla każdego klastra. Wykresy można znaleźć na karcie trwały wolumin skoroszytu **szczegóły obciążenia** bezpośrednio z klastra AKS, wybierając pozycję skoroszyty z okienka po lewej stronie, a następnie z listy rozwijanej **Wyświetl skoroszyty** w szczegółowe informacje. Możesz również włączyć zalecany alert do użycia PV, a także zbadać te metryki w Log Analytics.  

![Przykładowy skoroszyt obciążenia Azure Monitor PV](./media/container-insights-persistent-volumes/pv-workload-example.PNG)

## <a name="next-steps"></a>Następne kroki

- Więcej informacji na temat zebranych metryk PV [znajdziesz tutaj](./container-insights-agent-config.md).