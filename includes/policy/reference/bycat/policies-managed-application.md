---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 03/10/2021
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: f58d527e5877247f7fdcc49117ce85cdd933e3c9
ms.sourcegitcommit: d135e9a267fe26fbb5be98d2b5fd4327d355fe97
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/10/2021
ms.locfileid: "102607814"
---
|Nazwa<br /><sub>(Azure Portal)</sub> |Opis |Efekt (s) |Wersja<br /><sub>GitHub</sub> |
|---|---|---|---|
|[Definicja aplikacji dla aplikacji zarządzanej powinna korzystać z konta magazynu dostarczonego przez klienta](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F9db7917b-1607-4e7d-a689-bca978dd0633) |Użyj własnego konta magazynu, aby kontrolować dane definicji aplikacji, gdy jest to wymaganie prawne lub zgodne. Możesz zdecydować się na przechowywanie definicji aplikacji zarządzanej w ramach konta magazynu dostarczonego przez użytkownika podczas tworzenia, tak aby jego lokalizacja i dostęp mogły być w pełni zarządzane przez użytkownika w celu spełnienia wymagań dotyczących zgodności z przepisami. |Inspekcja, Odmów, wyłączone |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Managed%20Application/ApplicationDefinition_Missing_StorageAccount_Deny.json) |
|[Wdróż skojarzenia dla aplikacji zarządzanej](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F17763ad9-70c0-4794-9397-53d765932634) |Wdraża zasób skojarzenia, który kojarzy wybrane typy zasobów z określoną aplikacją zarządzaną.  To wdrożenie zasad nie obsługuje zagnieżdżonych typów zasobów. |deployIfNotExists |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Managed%20Application/AssociationForManagedApplication_Deploy.json) |
