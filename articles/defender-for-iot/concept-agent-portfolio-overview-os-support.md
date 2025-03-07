---
title: Omówienie portfolio agentów i obsługa systemu operacyjnego
description: Usługa Azure Defender for IoT oferuje duży portfolio agentów na podstawie typu urządzenia.
author: shhazam-ms
manager: rkarlin
ms.author: shhazam
ms.date: 1/20/2021
ms.topic: quickstart
ms.service: azure
ms.openlocfilehash: e2897018d1695bde665e1d1aca180e5268851a0b
ms.sourcegitcommit: dac05f662ac353c1c7c5294399fca2a99b4f89c8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/04/2021
ms.locfileid: "102120151"
---
# <a name="agent-portfolio-overview-and-os-support"></a>Omówienie portfolio agentów i obsługa systemu operacyjnego 

Usługa Azure Defender for IoT oferuje duży portfolio agentów na podstawie typu urządzenia. 

## <a name="standalone-agent"></a>Autonomiczny Agent

Agent autonomiczny obejmuje większość systemów operacyjnych Linux, które można wdrożyć jako pakiet binarny lub jako kod źródłowy, który można włączyć jako część oprogramowania układowego i zezwolić na modyfikację i dostosowanie w zależności od potrzeb klientów. Przykład obsługi systemu operacyjnego: 

| System operacyjny | Procesor | ARM32v7 |
|--|--|--|
| Debian 9 | ✓ | ✓ |
| Ubuntu 18.04 | ✓ |  |
| Ubuntu 20.04 | ✓ |  |

Aby uzyskać szczegółowe informacje, obsługę systemu operacyjnego lub zażądać dostępu do kodu źródłowego, aby można było je dołączyć do oprogramowania układowego urządzenia, skontaktuj się z kierownikiem ds. klientów lub Wyślij wiadomość e-mail na adres <defender_micro_agent@microsoft.com> . 

## <a name="azure-rtos-micro-agent"></a>Usługa Azure RTO Micro Agent

Usługa Azure Defender dla programu IoT Micro Agent oferuje kompleksowe i lekkie rozwiązanie zabezpieczeń dla urządzeń korzystających z usługi Azure RTO. Usługa Azure Defender dla programu IoT Micro Agent zapewnia ochronę typowych zagrożeń oraz potencjalne złośliwe działania na urządzeniach z systemem operacyjnym (RTO) w czasie rzeczywistym. Micro Agent jest wbudowany jako część składnika Azure RTO NetX Duo i monitoruje aktywność sieci urządzenia. 

Usługa Azure Defender for IoT Micro jest wbudowana w ramach składnika Azure RTO NetX Duo i monitoruje aktywność sieciową urządzenia. Micro Agent składa się z kompleksowego i lekkiego rozwiązania zabezpieczeń, które zapewnia pokrycie typowych zagrożeń i potencjalnie złośliwych działań na urządzeniach z systemem operacyjnym (RTO) w czasie rzeczywistym.

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej na temat [omówienia autonomicznej usługi Micro Agent ](concept-standalone-micro-agent-overview.md).