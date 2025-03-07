---
title: Azure Monitor rozszerzenie maszyny wirtualnej dla systemu Linux
description: Wdróż agenta zależności Azure Monitor na maszynie wirtualnej z systemem Linux przy użyciu rozszerzenia maszyny wirtualnej.
ms.topic: article
ms.service: virtual-machines
ms.subservice: extensions
author: mgoedtel
ms.author: magoedte
ms.collection: linux
ms.date: 03/29/2019
ms.openlocfilehash: d28f0a34f47942bba8776a0acd0bfe3aaf25df12
ms.sourcegitcommit: 7edadd4bf8f354abca0b253b3af98836212edd93
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/10/2021
ms.locfileid: "102566311"
---
# <a name="azure-monitor-dependency-virtual-machine-extension-for-linux"></a>Azure Monitor rozszerzenie maszyny wirtualnej dla systemu Linux

Funkcja mapy Azure Monitor dla maszyn wirtualnych pobiera swoje dane z programu Microsoft Dependency Agent. Rozszerzenie maszyny wirtualnej agenta zależności maszyny wirtualnej platformy Azure jest publikowane i obsługiwane przez firmę Microsoft. Rozszerzenie instaluje agenta zależności na maszynach wirtualnych platformy Azure. Ten dokument zawiera szczegółowe informacje o obsługiwanych platformach, konfiguracjach i opcjach wdrażania dla rozszerzenia maszyny wirtualnej agenta zależności maszyny wirtualnej platformy Azure dla systemu Linux.

## <a name="prerequisites"></a>Wymagania wstępne

### <a name="operating-system"></a>System operacyjny

Rozszerzenie agenta zależności maszyny wirtualnej platformy Azure dla systemu Linux można uruchomić w odniesieniu do obsługiwanych systemów operacyjnych wymienionych w sekcji [obsługiwane systemy operacyjne](../../azure-monitor/vm/vminsights-enable-overview.md#supported-operating-systems) w artykule Wdrażanie Azure monitor dla maszyn wirtualnych.

## <a name="extension-schema"></a>Schemat rozszerzenia

Poniższy kod JSON przedstawia schemat rozszerzenia agenta zależności maszyny wirtualnej platformy Azure na maszynie wirtualnej platformy Azure z systemem Linux. 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
  "parameters": {
    "vmName": {
      "type": "string",
      "metadata": {
        "description": "The name of existing Linux Azure VM."
      }
    }
  },
  "variables": {
    "vmExtensionsApiVersion": "2017-03-30"
  },
  "resources": [
    {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "[concat(parameters('vmName'),'/DAExtension')]",
      "apiVersion": "[variables('vmExtensionsApiVersion')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
      ],
      "properties": {
        "publisher": "Microsoft.Azure.Monitoring.DependencyAgent",
        "type": "DependencyAgentLinux",
        "typeHandlerVersion": "9.5",
        "autoUpgradeMinorVersion": true
      }
    }
  ],
    "outputs": {
    }
}
```

### <a name="property-values"></a>Wartości właściwości

| Nazwa | Wartość/przykład |
| ---- | ---- |
| apiVersion | 2015-01-01 |
| publisher | Microsoft. Azure. Monitoring. DependencyAgent |
| typ | DependencyAgentLinux |
| typeHandlerVersion | 9,5 |

## <a name="template-deployment"></a>Wdrażanie na podstawie szablonu

Rozszerzenia maszyny wirtualnej platformy Azure można wdrażać za pomocą szablonów Azure Resource Manager. Można użyć schematu JSON szczegółowego w poprzedniej sekcji w szablonie Azure Resource Manager, aby uruchomić rozszerzenie agenta zależności maszyny wirtualnej platformy Azure podczas wdrażania szablonu Azure Resource Manager.

Plik JSON rozszerzenia maszyny wirtualnej może być zagnieżdżony w ramach zasobu maszyny wirtualnej. Lub można ją umieścić na głównym lub najwyższego poziomu szablonu JSON Menedżer zasobów. Położenie pliku JSON wpływa na wartość nazwy zasobu i typu. Aby uzyskać więcej informacji, zobacz [Ustawianie nazwy i typu dla zasobów podrzędnych](../../azure-resource-manager/templates/child-resource-name-type.md).

W poniższym przykładzie przyjęto założenie, że rozszerzenie agenta zależności jest zagnieżdżone w ramach zasobu maszyny wirtualnej. W przypadku zagnieżdżania zasobu rozszerzenia kod JSON zostanie umieszczony w `"resources": []` obiekcie maszyny wirtualnej.


```json
{
    "type": "extensions",
    "name": "DAExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.Monitoring.DependencyAgent",
        "type": "DependencyAgentLinux",
        "typeHandlerVersion": "9.5",
        "autoUpgradeMinorVersion": true
    }
}
```

Gdy umieścisz kod JSON rozszerzenia w katalogu głównym szablonu, nazwa zasobu zawiera odwołanie do nadrzędnej maszyny wirtualnej. Typ odzwierciedla zagnieżdżoną konfigurację. 

```json
{
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "<parentVmResource>/DAExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.Monitoring.DependencyAgent",
        "type": "DependencyAgentLinux",
        "typeHandlerVersion": "9.5",
        "autoUpgradeMinorVersion": true
    }
}
```

## <a name="azure-cli-deployment"></a>Wdrożenie interfejsu wiersza polecenia platformy Azure

Możesz użyć interfejsu wiersza polecenia platformy Azure, aby wdrożyć rozszerzenie maszyny wirtualnej agenta zależności do istniejącej maszyny wirtualnej.  

```azurecli

az vm extension set \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --name DependencyAgentLinux \
    --publisher Microsoft.Azure.Monitoring.DependencyAgent \
    --version 9.5 
```

## <a name="troubleshoot-and-support"></a>Rozwiązywanie problemów i pomoc techniczna

### <a name="troubleshoot"></a>Rozwiązywanie problemów

Dane dotyczące stanu wdrożeń rozszerzeń można pobrać z Azure Portal i przy użyciu interfejsu wiersza polecenia platformy Azure. Aby wyświetlić stan wdrożenia dla danej maszyny wirtualnej, uruchom następujące polecenie przy użyciu interfejsu wiersza polecenia platformy Azure:

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

Dane wyjściowe wykonania rozszerzenia są rejestrowane w następującym pliku:

```
/opt/microsoft/dependency-agent/log/install.log 
```

### <a name="support"></a>Pomoc techniczna

Jeśli potrzebujesz więcej pomocy w dowolnym punkcie tego artykułu, skontaktuj się z ekspertami platformy Azure na [forach MSDN i Stack Overflow](https://azure.microsoft.com/support/forums/). Możesz też zaplikować zdarzenie pomocy technicznej platformy Azure. Przejdź do [witryny pomocy technicznej systemu Azure](https://azure.microsoft.com/support/options/) i wybierz pozycję **Uzyskaj pomoc techniczną**. Aby uzyskać informacje o sposobach korzystania z pomocy technicznej systemu Azure, przeczytaj temat [Microsoft Azure support — często zadawane pytania](https://azure.microsoft.com/support/faq/).
