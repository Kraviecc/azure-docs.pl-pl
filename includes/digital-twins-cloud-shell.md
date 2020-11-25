---
author: baanders
description: plik dołączany dla usługi Azure Digital bliźniaczych reprezentacji — konfiguracja Cloud Shell i rozszerzenie IoT
ms.service: digital-twins
ms.topic: include
ms.date: 7/17/2020
ms.author: baanders
ms.openlocfilehash: c1d1efce656bea02385cb20ac11ab90ca5664e60
ms.sourcegitcommit: a43a59e44c14d349d597c3d2fd2bc779989c71d7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/25/2020
ms.locfileid: "96026041"
---
Aby rozpocząć pracę z usługą Azure Digital bliźniaczych reprezentacji w otwartym oknie [Azure Cloud Shell](https://shell.azure.com) , najpierw należy się zalogować i ustawić kontekst powłoki dla tej sesji. Uruchom następujące polecenia w Cloud Shell:

```azurecli-interactive
az login
az account set --subscription "<your-Azure-subscription-ID>"
```
> [!TIP]
> Możesz również użyć nazwy subskrypcji zamiast identyfikatora w powyższym poleceniu. 

Jeśli korzystasz z tej subskrypcji po raz pierwszy przy użyciu usługi Azure Digital bliźniaczych reprezentacji, Uruchom to polecenie, aby zarejestrować się w przestrzeni nazw usługi Azure Digital bliźniaczych reprezentacji. (Jeśli nie masz pewności, możesz go uruchomić ponownie nawet wtedy, gdy kiedyś upłynął czas w przeszłości).

```azurecli-interactive
az provider register --namespace 'Microsoft.DigitalTwins'
```

Następnie dodasz do Cloud Shell [**Microsoft Azure IoT Extension dla interfejsu wiersza polecenia platformy Azure**](/cli/azure/ext/azure-iot/iot?preserve-view=true&view=azure-cli-latest) , aby włączyć obsługę komunikacji z usługą Azure Digital bliźniaczych reprezentacji i innymi usługami IoT. 

[!INCLUDE [digital-twins-cloud-shell-extensions.md](digital-twins-cloud-shell-extensions.md)]

Teraz możesz przystąpić do pracy z usługą Azure Digital bliźniaczych reprezentacji w Cloud Shell.

Możesz to sprawdzić, uruchamiając `az dt -h` w dowolnym momencie, aby wyświetlić listę dostępnych poleceń usługi Azure Digital bliźniaczych reprezentacji.