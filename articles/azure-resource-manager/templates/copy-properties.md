---
title: Definiowanie wielu wystąpień właściwości
description: Użyj operacji kopiowania w szablonie Azure Resource Manager (szablon ARM) do wielokrotnego iteracji podczas tworzenia właściwości w zasobie.
ms.topic: conceptual
ms.date: 09/15/2020
ms.openlocfilehash: 958deba6152ffa3bcb1d2d79cd026c0cb2eebcbe
ms.sourcegitcommit: 956dec4650e551bdede45d96507c95ecd7a01ec9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/09/2021
ms.locfileid: "102521665"
---
# <a name="property-iteration-in-arm-templates"></a>Iteracja właściwości w szablonach ARM

W tym artykule pokazano, jak utworzyć więcej niż jedno wystąpienie właściwości w szablonie Azure Resource Manager (szablon ARM). Poprzez dodanie `copy` elementu do sekcji Właściwości zasobu w szablonie, można dynamicznie ustawić liczbę elementów dla właściwości podczas wdrażania. Należy również unikać powtarzania składni szablonu.

Można używać tylko `copy` z zasobami najwyższego poziomu, nawet gdy mają zastosowanie `copy` do właściwości. Aby dowiedzieć się więcej na temat zmiany zasobu podrzędnego z zasobem najwyższego poziomu, zobacz [iteracja zasobu podrzędnego](copy-resources.md#iteration-for-a-child-resource).

Możesz również używać kopiowania z [zasobami](copy-resources.md), [zmiennymi](copy-variables.md)i [wyjściami](copy-outputs.md).

## <a name="syntax"></a>Składnia

Element Copy ma następujący format ogólny:

```json
"copy": [
  {
    "name": "<name-of-loop>",
    "count": <number-of-iterations>,
    "input": <values-for-the-property>
  }
]
```

W polu `name` Podaj nazwę właściwości zasobu, którą chcesz utworzyć.

`count`Właściwość określa liczbę iteracji dla właściwości.

`input`Właściwość określa właściwości, które chcesz powtórzyć. Tworzysz tablicę elementów skonstruowanych na podstawie wartości we `input` właściwości.

## <a name="copy-limits"></a>Limity kopiowania

Liczba nie może przekraczać 800.

Liczba nie może być liczbą ujemną. Może to być zero, jeśli szablon zostanie wdrożony przy użyciu najnowszej wersji interfejsu wiersza polecenia platformy Azure, programu PowerShell lub API REST. W tym celu należy użyć:

* Azure PowerShell **2,6** lub nowszy
* Interfejs wiersza polecenia platformy Azure **2.0.74** lub nowszy
* Interfejs API REST w wersji **2019-05-10** lub nowszej
* [Połączone wdrożenia](linked-templates.md) muszą używać interfejsu API w wersji **2019-05-10** lub nowszej dla typu zasobu wdrożenia

We wcześniejszych wersjach programu PowerShell, interfejsu wiersza polecenia i interfejsie API REST nie są obsługiwane wartości zerowe.

## <a name="property-iteration"></a>Iteracja właściwości

Poniższy przykład pokazuje, jak zastosować `copy` do `dataDisks` właściwości na maszynie wirtualnej:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "numberOfDataDisks": {
      "type": "int",
      "minValue": 0,
      "maxValue": 16,
      "defaultValue": 3,
      "metadata": {
        "description": "The number of dataDisks to create."
      }
    },
    ...
  },
  "resources": [
    {
      "type": "Microsoft.Compute/virtualMachines",
      "apiVersion": "2017-03-30",
      ...
      "properties": {
        "storageProfile": {
          ...
          "copy": [
            {
              "name": "dataDisks",
              "count": "[parameters('numberOfDataDisks')]",
              "input": {
                "diskSizeGB": 1023,
                "lun": "[copyIndex('dataDisks')]",
                "createOption": "Empty"
              }
            }
          ]
        }
      }
    }
  ]
}
```

Należy zauważyć, że `copyIndex` w przypadku użycia wewnątrz iteracji właściwości należy podać nazwę iteracji. Iteracja właściwości obsługuje również argument przesunięcia. Przesunięcie musi następować po nazwie iteracji, takiej jak `copyIndex('dataDisks', 1)` .

Menedżer zasobów rozszerza `copy` tablicę podczas wdrażania. Nazwa tablicy zmieni się na nazwę właściwości. Wartości wejściowe stają się właściwościami obiektu. Wdrożony szablon zostanie:

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "dataDisks": [
        {
          "lun": 0,
          "createOption": "Empty",
          "diskSizeGB": 1023
        },
        {
          "lun": 1,
          "createOption": "Empty",
          "diskSizeGB": 1023
        },
        {
          "lun": 2,
          "createOption": "Empty",
          "diskSizeGB": 1023
        }
      ],
      ...
```

Operacja kopiowania jest przydatna podczas pracy z tablicami, ponieważ można wykonać iterację każdego elementu w tablicy. Użyj `length` funkcji w tablicy, aby określić liczbę iteracji i `copyIndex` pobrać bieżący indeks tablicy.

Poniższy przykładowy szablon tworzy grupę trybu failover dla baz danych, które są przenoszone jako tablica.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "primaryServerName": {
            "type": "string"
        },
        "secondaryServerName": {
            "type": "string"
        },
        "databaseNames": {
            "type": "array",
            "defaultValue": [
                "mydb1",
                "mydb2",
                "mydb3"
            ]
        }
    },
    "variables": {
        "failoverName": "[concat(parameters('primaryServerName'),'/', parameters('primaryServerName'),'failovergroups')]"
    },
    "resources": [
        {
            "type": "Microsoft.Sql/servers/failoverGroups",
            "apiVersion": "2015-05-01-preview",
            "name": "[variables('failoverName')]",
            "properties": {
                "readWriteEndpoint": {
                    "failoverPolicy": "Automatic",
                    "failoverWithDataLossGracePeriodMinutes": 60
                },
                "readOnlyEndpoint": {
                    "failoverPolicy": "Disabled"
                },
                "partnerServers": [
                    {
                        "id": "[resourceId('Microsoft.Sql/servers', parameters('secondaryServerName'))]"
                    }
                ],
                "copy": [
                    {
                        "name": "databases",
                        "count": "[length(parameters('databaseNames'))]",
                        "input": "[resourceId('Microsoft.Sql/servers/databases', parameters('primaryServerName'), parameters('databaseNames')[copyIndex('databases')])]"
                    }
                ]
            }
        }
    ],
    "outputs": {
    }
}
```

`copy`Element jest tablicą, aby można było określić więcej niż jedną właściwość zasobu.

```json
{
  "type": "Microsoft.Network/loadBalancers",
  "apiVersion": "2017-10-01",
  "name": "exampleLB",
  "properties": {
    "copy": [
      {
        "name": "loadBalancingRules",
        "count": "[length(parameters('loadBalancingRules'))]",
        "input": {
          ...
        }
      },
      {
        "name": "probes",
        "count": "[length(parameters('loadBalancingRules'))]",
        "input": {
          ...
        }
      }
    ]
  }
}
```

Iteracji zasobów i właściwości można używać razem. Odwołuje się do iteracji właściwości według nazwy.

```json
{
  "type": "Microsoft.Network/virtualNetworks",
  "apiVersion": "2018-04-01",
  "name": "[concat(parameters('vnetname'), copyIndex())]",
  "copy":{
    "count": 2,
    "name": "vnetloop"
  },
  "location": "[resourceGroup().location]",
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "[parameters('addressPrefix')]"
      ]
    },
    "copy": [
      {
        "name": "subnets",
        "count": 2,
        "input": {
          "name": "[concat('subnet-', copyIndex('subnets'))]",
          "properties": {
            "addressPrefix": "[variables('subnetAddressPrefix')[copyIndex('subnets')]]"
          }
        }
      }
    ]
  }
}
```

## <a name="example-templates"></a>Przykładowe szablony

Poniższy przykład przedstawia typowy scenariusz tworzenia więcej niż jednej wartości właściwości.

|Template  |Opis  |
|---------|---------|
|[Wdrożenie maszyny wirtualnej z zmienną liczbą dysków z danymi](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-windows-copy-datadisks) |Wdraża kilka dysków danych z maszyną wirtualną. |

## <a name="next-steps"></a>Następne kroki

* Aby przejść przez samouczek, zobacz [Samouczek: Tworzenie wielu wystąpień zasobów przy użyciu szablonów ARM](template-tutorial-create-multiple-instances.md).
* Aby poznać inne zastosowania elementu Copy, zobacz:
  * [Iteracja zasobów w szablonach ARM](copy-resources.md)
  * [Iteracja zmiennej w szablonach ARM](copy-variables.md)
  * [Iteracja danych wyjściowych w szablonach ARM](copy-outputs.md)
* Jeśli chcesz dowiedzieć się więcej na temat sekcji szablonu, zobacz [Omówienie struktury i składni szablonów ARM](template-syntax.md).
* Aby dowiedzieć się, jak wdrożyć szablon, zobacz [wdrażanie zasobów przy użyciu szablonów ARM i Azure PowerShell](deploy-powershell.md).
