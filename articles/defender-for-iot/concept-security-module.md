---
title: Moduł zabezpieczeń i bliźniaczych reprezentacji urządzeń
description: Dowiedz się więcej o koncepcji bliźniaczych reprezentacji modułów zabezpieczeń i sposobach ich użycia w usłudze Defender for IoT.
services: defender-for-iot
ms.service: defender-for-iot
documentationcenter: na
author: mlottner
manager: rkarlin
editor: ''
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2019
ms.author: mlottner
ms.openlocfilehash: feb84a1261e37600c68d8e372162033d4021f564
ms.sourcegitcommit: 27d616319a4f57eb8188d1b9d9d793a14baadbc3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/15/2021
ms.locfileid: "100522924"
---
# <a name="security-module"></a>Moduł zabezpieczeń

W tym artykule wyjaśniono, jak usługa Defender for IoT używa urządzeń bliźniaczych reprezentacji i modułów.

## <a name="device-twins"></a>Bliźniaczych reprezentacji urządzenia

W przypadku rozwiązań IoT utworzonych na platformie Azure bliźniaczych reprezentacji urządzeń odgrywa kluczową rolę w zarządzaniu urządzeniami i automatyzacją procesów.

Usługa Defender for IoT oferuje pełną integrację z istniejącą platformą zarządzania urządzeniami IoT, umożliwiając zarządzanie stanem zabezpieczeń urządzeń oraz korzystanie z istniejących możliwości sterowania urządzeniami. Integrację uzyskuje się, korzystając z mechanizmu IoT Hubej przędzy.

Dowiedz się więcej o koncepcji [bliźniaczych reprezentacji urządzeń](../iot-hub/iot-hub-devguide-device-twins.md) na platformie Azure IoT Hub.

## <a name="security-module-twins"></a>Bliźniaczych reprezentacji modułu zabezpieczeń

Usługa Defender for IoT utrzymuje dwuosiowy moduł zabezpieczeń dla każdego urządzenia w usłudze.
Sznury modułowe zabezpieczeń zawiera wszystkie informacje dotyczące zabezpieczeń urządzeń dla każdego konkretnego urządzenia w rozwiązaniu.
Właściwości zabezpieczeń urządzeń są utrzymywane w dedykowanym module zabezpieczeń, w celu zapewnienia bezpieczniejszej komunikacji oraz do włączania aktualizacji i konserwacji, które wymagają mniejszej ilości zasobów.

Zobacz [Tworzenie sznurka modułu zabezpieczeń](quickstart-create-security-twin.md) i [Konfigurowanie agentów zabezpieczeń](how-to-agent-configuration.md) , aby dowiedzieć się, jak tworzyć, dostosowywać i konfigurować sznurek. Zobacz [Opis modułu bliźniaczych reprezentacji](../iot-hub/iot-hub-devguide-module-twins.md) , aby dowiedzieć się więcej o koncepcji modułu bliźniaczych reprezentacji w IoT Hub.

## <a name="next-steps"></a>Następne kroki

- [Omówienie usługi Defender for IoT](overview.md)
- [Wdrażanie agentów zabezpieczeń](how-to-deploy-agent.md)
- [Metody uwierzytelniania agenta zabezpieczeń](concept-security-agent-authentication-methods.md)