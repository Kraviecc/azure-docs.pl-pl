---
title: Plik dyrektywy include
description: Plik dyrektywy include
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 08/14/2019
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 089ad704a466590a9649107fef245a88d6a4d6e3
ms.sourcegitcommit: f7eda3db606407f94c6dc6c3316e0651ee5ca37c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/05/2021
ms.locfileid: "102245019"
---
Następująca konfiguracja została użyta w poniższych krokach:

- Komputer: Ubuntu Server 18,04
- Zależności: klient strongswan


Użyj następujących poleceń, aby zainstalować wymaganą konfigurację klient strongswan:

```
sudo apt install strongswan
```

```
sudo apt install strongswan-pki
```

```
sudo apt install libstrongswan-extra-plugins
```

Użyj następującego polecenia, aby zainstalować interfejs wiersza polecenia platformy Azure:

```
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

[Dodatkowe instrukcje dotyczące instalowania interfejsu wiersza polecenia platformy Azure](/cli/azure/install-azure-cli-apt)