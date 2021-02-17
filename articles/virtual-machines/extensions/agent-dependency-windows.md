---
title: Azure Monitor rozszerzenie maszyny wirtualnej zależności dla systemu Windows
description: Wdróż agenta zależności Azure Monitor na maszynie wirtualnej z systemem Windows przy użyciu rozszerzenia maszyny wirtualnej.
services: virtual-machines-windows
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.subservice: extensions
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2019
ms.author: magoedte
ms.openlocfilehash: 0151e7b3a30cd4b00dba75b7490563923cd5b8ff
ms.sourcegitcommit: e559daa1f7115d703bfa1b87da1cf267bf6ae9e8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/17/2021
ms.locfileid: "100580296"
---
# <a name="azure-monitor-dependency-virtual-machine-extension-for-windows"></a>Azure Monitor rozszerzenie maszyny wirtualnej zależności dla systemu Windows

Funkcja mapy Azure Monitor dla maszyn wirtualnych pobiera swoje dane z programu Microsoft Dependency Agent. Rozszerzenie maszyny wirtualnej agenta zależności maszyny wirtualnej platformy Azure jest publikowane i obsługiwane przez firmę Microsoft. Rozszerzenie instaluje agenta zależności na maszynach wirtualnych platformy Azure. Ten dokument zawiera szczegółowe informacje o obsługiwanych platformach, konfiguracjach i opcjach wdrażania dla rozszerzenia maszyny wirtualnej agenta zależności maszyny wirtualnej platformy Azure dla systemu Windows.

## <a name="operating-system"></a>System operacyjny

Rozszerzenie agenta zależności maszyny wirtualnej platformy Azure dla systemu Windows można uruchomić w odniesieniu do obsługiwanych systemów operacyjnych wymienionych w sekcji [obsługiwane systemy operacyjne](../../azure-monitor/vm/vminsights-enable-overview.md#supported-operating-systems) w artykule Wdrażanie Azure monitor dla maszyn wirtualnych.

## <a name="extension-schema"></a>Schemat rozszerzenia

Poniższy kod JSON przedstawia schemat rozszerzenia agenta zależności maszyny wirtualnej platformy Azure na maszynie wirtualnej z systemem Windows Azure.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
  "parameters": {
    "vmName": {
      "type": "string",
      "metadata": {
        "description": "The name of existing Azure VM. Supported Windows Server versions:  2008 R2 and above (x64)."
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
        "type": "DependencyAgentWindows",
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
| typ | DependencyAgentWindows |
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
        "type": "DependencyAgentWindows",
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
        "type": "DependencyAgentWindows",
        "typeHandlerVersion": "9.5",
        "autoUpgradeMinorVersion": true
    }
}
```

## <a name="powershell-deployment"></a>Wdrażanie przy użyciu programu PowerShell

Za pomocą polecenia można `Set-AzVMExtension` wdrożyć rozszerzenie maszyny wirtualnej agenta zależności do istniejącej maszyny wirtualnej. Przed uruchomieniem polecenia należy zapisać konfigurację publiczną i prywatną w tabeli skrótów programu PowerShell.

```powershell

Set-AzVMExtension -ExtensionName "Microsoft.Azure.Monitoring.DependencyAgent" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.Azure.Monitoring.DependencyAgent" `
    -ExtensionType "DependencyAgentWindows" `
    -TypeHandlerVersion 9.5 `
    -Location WestUS 
```

## <a name="troubleshoot-and-support"></a>Rozwiązywanie problemów i pomoc techniczna

### <a name="troubleshoot"></a>Rozwiązywanie problemów

Dane dotyczące stanu wdrożeń rozszerzeń można pobrać z Azure Portal i przy użyciu modułu Azure PowerShell. Aby wyświetlić stan wdrożenia dla danej maszyny wirtualnej, uruchom następujące polecenie przy użyciu modułu Azure PowerShell:

```powershell
Get-AzVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Dane wyjściowe wykonania rozszerzenia są rejestrowane w plikach znalezionych w następującym katalogu:

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Monitoring.DependencyAgent\
```

### <a name="support"></a>Pomoc techniczna

Jeśli potrzebujesz więcej pomocy w dowolnym punkcie tego artykułu, możesz skontaktować się z ekspertami platformy Azure na [forach MSDN i Stack Overflow](https://azure.microsoft.com/support/forums/). Możesz też zaplikować zdarzenie pomocy technicznej platformy Azure. Przejdź do [witryny pomocy technicznej systemu Azure](https://azure.microsoft.com/support/options/) i wybierz pozycję **Uzyskaj pomoc techniczną**. Aby uzyskać informacje o sposobach korzystania z pomocy technicznej systemu Azure, przeczytaj temat [Microsoft Azure support — często zadawane pytania](https://azure.microsoft.com/support/faq/).
